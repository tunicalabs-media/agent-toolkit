# Reusable Production Deployment CI/CD

This single file contains:

- the explanation of this repo's production deployment flow
- a reusable Dockerfile template
- a reusable deployment script
- a reusable GitHub Actions deployment workflow
- a reusable quality gate workflow
- a Codex prompt you can use in another project

Use the production pattern from this repo as the base. It is safer than the staging workflow because it includes rollback and health verification.

## Current production flow in this repo

1. A push lands on the `production` branch.
2. GitHub Actions runs `.github/workflows/deploy-production.yml`.
3. The workflow SSHes into the VM.
4. The VM updates the repo to `origin/production`.
5. The workflow exports deployment variables and runs `scripts/deploy.sh`.
6. `scripts/deploy.sh`:
   - renames the current container to a `previous-stable` backup
   - builds a new Docker image
   - starts the new container on the target port
   - checks container and HTTP health
   - rolls back automatically if the deployment fails
   - removes old containers and old images after success

## What to reuse in another project

Copy the code blocks below into the new project as:

1. `Dockerfile`
2. `scripts/deploy.sh`
3. `.github/workflows/deploy-production.yml`
4. `.github/workflows/quality-gate.yml`

Then adjust:

- app name
- repo path on the VM
- deployment branch
- host port and container port
- health check path
- build args or runtime env vars
- start command if the app is not a standalone Next.js server

## Required GitHub secrets

The production workflow expects:

- `SSH_HOST_PROD`
- `SSH_PORT_PROD`
- `SSH_USER_PROD`
- `SSH_PASSWORD_PROD`

If you prefer SSH keys, replace the SSH step with an SSH-agent-based action.

## Required VM setup

The target VM needs:

- Docker installed and usable by the SSH user
- Git installed
- Curl installed
- The project already cloned on the VM
- The deploy branch available on the remote repository

Recommended repo path on the VM:

- `~/apps/<project-name>`

## Deployment variables

Set these values before running `scripts/deploy.sh`:

- `APP_NAME`
- `DOCKERFILE`
- `DEPLOY_BRANCH`
- `PROJECT_DIR`
- `HOST_PORT`
- `CONTAINER_PORT`
- `HEALTH_PATH`
- `NEXT_PUBLIC_PROJECT_ENV` if your app needs it

Optional variables:

- `IMAGE_REPO`
- `HEALTH_TIMEOUT_SECONDS`
- `PORT_RELEASE_TIMEOUT_SECONDS`
- `NEXT_PUBLIC_EXPORT`
- `GITHUB_SHA`

Example:

```bash
export APP_NAME="acme-web-production"
export DOCKERFILE="Dockerfile"
export DEPLOY_BRANCH="production"
export PROJECT_DIR="$HOME/apps/acme-web"
export HOST_PORT="3000"
export CONTAINER_PORT="3000"
export HEALTH_PATH="/health"
```

## Reusable Dockerfile

```dockerfile
# Reusable production Dockerfile for a standalone Next.js app

FROM node:24-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .

ARG NEXT_PUBLIC_PROJECT_ENV=production
ENV NEXT_PUBLIC_PROJECT_ENV=$NEXT_PUBLIC_PROJECT_ENV

ARG NEXT_PUBLIC_EXPORT=yes
ENV NEXT_PUBLIC_EXPORT=$NEXT_PUBLIC_EXPORT

ARG NEXT_BUILD_ID=local
ENV NEXT_BUILD_ID=$NEXT_BUILD_ID

RUN npm run build

FROM node:24-alpine AS runner

WORKDIR /app

ENV NODE_ENV=production
ENV NEXT_PUBLIC_PROJECT_ENV=production
ENV NEXT_PUBLIC_EXPORT=yes
ENV PORT=3000

COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public

EXPOSE 3000

HEALTHCHECK --interval=10s --timeout=5s --start-period=15s --retries=12 \
  CMD wget -q --spider "http://127.0.0.1:${PORT}/" || exit 1

CMD ["node", "server.js"]
```

## Reusable Deployment Script

Save as `scripts/deploy.sh`.

```bash
#!/usr/bin/env bash

set -Eeuo pipefail

APP_NAME="${APP_NAME:?APP_NAME is required}"
DOCKERFILE="${DOCKERFILE:?DOCKERFILE is required}"

DEPLOY_BRANCH="${DEPLOY_BRANCH:-}"
PROJECT_DIR="${PROJECT_DIR:-$PWD}"
CONTAINER_PORT="${CONTAINER_PORT:-3000}"
HOST_PORT="${HOST_PORT:-3000}"
HEALTH_PATH="${HEALTH_PATH:-/}"
HEALTH_TIMEOUT_SECONDS="${HEALTH_TIMEOUT_SECONDS:-240}"
PORT_RELEASE_TIMEOUT_SECONDS="${PORT_RELEASE_TIMEOUT_SECONDS:-30}"
IMAGE_REPO="${IMAGE_REPO:-$APP_NAME}"
IMAGE_TAG="${GITHUB_SHA:-$(git -C "$PROJECT_DIR" rev-parse --short HEAD)}-$(date +%Y%m%d%H%M%S)"
NEW_IMAGE="${IMAGE_REPO}:${IMAGE_TAG}"
CURRENT_CONTAINER="${APP_NAME}"
PREVIOUS_STABLE_CONTAINER="${APP_NAME}-previous-stable"

ROLLBACK_REQUIRED=0
DEPLOYMENT_SUCCEEDED=0
PREVIOUS_STABLE_AVAILABLE=0
PREVIOUS_STABLE_IMAGE=""

log() {
  printf '[deploy][%s] %s\n' "$APP_NAME" "$1"
}

require_cmd() {
  command -v "$1" >/dev/null 2>&1 || {
    echo "Missing required command: $1" >&2
    exit 1
  }
}

container_exists() {
  docker container inspect "$1" >/dev/null 2>&1
}

container_is_running() {
  [ "$(docker inspect --format '{{.State.Running}}' "$1" 2>/dev/null || printf 'false')" = "true" ]
}

remove_container() {
  local container_name="$1"

  if container_exists "$container_name"; then
    docker rm -f "$container_name" >/dev/null 2>&1 || true
  fi
}

port_has_listener() {
  local host_port="$1"

  if command -v lsof >/dev/null 2>&1; then
    lsof -nP -iTCP:"$host_port" -sTCP:LISTEN >/dev/null 2>&1
    return
  fi

  if command -v ss >/dev/null 2>&1; then
    ss -ltn "( sport = :${host_port} )" | tail -n +2 | grep -q .
    return
  fi

  return 1
}

describe_port_owner() {
  local host_port="$1"

  if command -v lsof >/dev/null 2>&1; then
    lsof -nP -iTCP:"$host_port" -sTCP:LISTEN || true
    return
  fi

  if command -v ss >/dev/null 2>&1; then
    ss -ltnp "( sport = :${host_port} )" || true
    return
  fi

  echo "Unable to inspect port owner; neither lsof nor ss is available." >&2
}

wait_for_port_release() {
  local host_port="$1"
  local deadline=$((SECONDS + PORT_RELEASE_TIMEOUT_SECONDS))

  while [ "$SECONDS" -lt "$deadline" ]; do
    if ! port_has_listener "$host_port"; then
      return 0
    fi

    sleep 1
  done

  return 1
}

prepare_previous_stable() {
  remove_container "$PREVIOUS_STABLE_CONTAINER"

  if ! container_exists "$CURRENT_CONTAINER"; then
    log "No currently deployed container found"
    return 0
  fi

  PREVIOUS_STABLE_IMAGE="$(docker inspect --format '{{.Config.Image}}' "$CURRENT_CONTAINER")"
  PREVIOUS_STABLE_AVAILABLE=1

  log "Preserving current container as previous stable"
  docker rename "$CURRENT_CONTAINER" "$PREVIOUS_STABLE_CONTAINER"

  if container_is_running "$PREVIOUS_STABLE_CONTAINER"; then
    log "Stopping current container on port ${HOST_PORT}"
    docker stop "$PREVIOUS_STABLE_CONTAINER" >/dev/null
  fi

  if ! wait_for_port_release "$HOST_PORT"; then
    log "Port ${HOST_PORT} did not release after stopping current container"
    describe_port_owner "$HOST_PORT" >&2 || true
    exit 1
  fi
}

build_image() {
  log "Building image ${NEW_IMAGE}"

  docker build \
    --label "app=${APP_NAME}" \
    --label "managed-by=github-actions" \
    --label "deploy-branch=${DEPLOY_BRANCH}" \
    --build-arg "NEXT_PUBLIC_PROJECT_ENV=${NEXT_PUBLIC_PROJECT_ENV:-production}" \
    --build-arg "NEXT_PUBLIC_EXPORT=${NEXT_PUBLIC_EXPORT:-yes}" \
    --build-arg "NEXT_BUILD_ID=${IMAGE_TAG}" \
    -f "$DOCKERFILE" \
    -t "$NEW_IMAGE" \
    .
}

run_new_container() {
  log "Starting new container on port ${HOST_PORT}"

  remove_container "$CURRENT_CONTAINER"

  docker run -d \
    --restart unless-stopped \
    --name "$CURRENT_CONTAINER" \
    --label "app=${APP_NAME}" \
    --label "managed-by=github-actions" \
    -p "127.0.0.1:${HOST_PORT}:${CONTAINER_PORT}" \
    "$NEW_IMAGE" >/dev/null
}

wait_for_container_health() {
  local container_name="$1"
  local host_port="$2"
  local deadline=$((SECONDS + HEALTH_TIMEOUT_SECONDS))

  while [ "$SECONDS" -lt "$deadline" ]; do
    local container_status
    local health_status

    container_status="$(docker inspect --format '{{.State.Status}}' "$container_name")"
    health_status="$(docker inspect --format '{{if .State.Health}}{{.State.Health.Status}}{{else}}none{{end}}' "$container_name")"

    if [ "$container_status" = "running" ] && curl -fsS -L "http://127.0.0.1:${host_port}${HEALTH_PATH}" >/dev/null; then
      return 0
    fi

    if [ "$container_status" = "exited" ] || [ "$container_status" = "dead" ]; then
      docker logs "$container_name" || true
      return 1
    fi

    if [ "$health_status" = "unhealthy" ]; then
      log "Container healthcheck reported unhealthy; continuing HTTP probe until timeout"
    fi

    sleep 5
  done

  docker inspect --format '{{json .State.Health}}' "$container_name" 2>/dev/null || true
  docker logs "$container_name" || true
  return 1
}

rollback() {
  local exit_code="$1"

  trap - ERR

  if [ "$ROLLBACK_REQUIRED" -eq 0 ] || [ "$DEPLOYMENT_SUCCEEDED" -eq 1 ]; then
    exit "$exit_code"
  fi

  log "Deployment failure detected"
  log "Rollback triggered"

  remove_container "$CURRENT_CONTAINER"

  if [ "$PREVIOUS_STABLE_AVAILABLE" -eq 1 ] && container_exists "$PREVIOUS_STABLE_CONTAINER"; then
    log "Restoring previous stable container on port ${HOST_PORT}"
    docker rename "$PREVIOUS_STABLE_CONTAINER" "$CURRENT_CONTAINER"
    docker start "$CURRENT_CONTAINER" >/dev/null
    wait_for_container_health "$CURRENT_CONTAINER" "$HOST_PORT"
    log "Rollback completed successfully"
  else
    log "No previous stable container is available for rollback"
  fi

  if docker image inspect "$NEW_IMAGE" >/dev/null 2>&1; then
    docker image rm "$NEW_IMAGE" >/dev/null 2>&1 || true
  fi

  exit "$exit_code"
}

cleanup_deployment_artifacts() {
  local image
  local -a images
  local -a protected_images=()

  log "Cleanup actions: removing old containers and unused images"

  if container_exists "$PREVIOUS_STABLE_CONTAINER"; then
    docker rm -f "$PREVIOUS_STABLE_CONTAINER" >/dev/null 2>&1 || true
  fi

  docker container prune -f --filter "label=app=${APP_NAME}" >/dev/null || true
  docker image prune -f --filter "dangling=true" >/dev/null || true

  protected_images+=("$NEW_IMAGE")

  if [ -n "$PREVIOUS_STABLE_IMAGE" ]; then
    protected_images+=("$PREVIOUS_STABLE_IMAGE")
  fi

  mapfile -t images < <(docker image ls "$IMAGE_REPO" --format '{{.Repository}}:{{.Tag}}' | awk '$0 !~ /<none>/' | sort -u)

  for image in "${images[@]}"; do
    if printf '%s\n' "${protected_images[@]}" | grep -Fxq "$image"; then
      continue
    fi

    log "Cleanup actions: removing image ${image}"
    docker image rm "$image" >/dev/null 2>&1 || true
  done
}

on_error() {
  local exit_code="$?"
  rollback "$exit_code"
}

trap on_error ERR

require_cmd docker
require_cmd git
require_cmd curl

cd "$PROJECT_DIR"

log "Deployment start"
log "Branch: ${DEPLOY_BRANCH:-unknown}"
log "Dockerfile: ${DOCKERFILE}"
log "Application port: ${HOST_PORT}"

ROLLBACK_REQUIRED=1
prepare_previous_stable
build_image
run_new_container

log "Running health check against http://127.0.0.1:${HOST_PORT}${HEALTH_PATH}"
if ! wait_for_container_health "$CURRENT_CONTAINER" "$HOST_PORT"; then
  log "Health check failed for ${CURRENT_CONTAINER}"
  exit 1
fi

DEPLOYMENT_SUCCEEDED=1
cleanup_deployment_artifacts

log "Deployment success"
```

## Reusable GitHub Actions Production Workflow

Save as `.github/workflows/deploy-production.yml`.

```yaml
name: Deploy to Production

on:
  push:
    branches:
      - production

concurrency:
  group: deploy-production
  cancel-in-progress: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      PROD_SSH_USER: ${{ secrets.SSH_USER_PROD }}
      PROD_SSH_PASSWORD: ${{ secrets.SSH_PASSWORD_PROD }}
      PROD_SSH_HOST: ${{ secrets.SSH_HOST_PROD }}
      PROD_SSH_PORT: ${{ secrets.SSH_PORT_PROD || '22' }}

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Install SSH tools
        run: |
          sudo apt-get update
          sudo apt-get install -y sshpass

      - name: Deploy to VM via SSH
        env:
          SSHPASS: ${{ env.PROD_SSH_PASSWORD }}
        run: |
          SUDO_PASSWORD_B64="$(printf '%s' "$PROD_SSH_PASSWORD" | base64 | tr -d '\n')"
          sshpass -e ssh -p "$PROD_SSH_PORT" -o StrictHostKeyChecking=no "$PROD_SSH_USER@$PROD_SSH_HOST" "SUDO_PASSWORD_B64='$SUDO_PASSWORD_B64' bash -s" << 'EOF'
            set -Eeuo pipefail

            cd ~/apps/your-project

            git fetch origin
            git checkout -B production origin/production
            git reset --hard origin/production

            export SUDO_PASSWORD="$(printf '%s' "$SUDO_PASSWORD_B64" | base64 -d)"
            export APP_NAME="your-project-production"
            export DEPLOY_BRANCH="production"
            export DOCKERFILE="Dockerfile"
            export PROJECT_DIR="$HOME/apps/your-project"
            export NEXT_PUBLIC_PROJECT_ENV="production"
            export HOST_PORT="3000"
            export CONTAINER_PORT="3000"
            export HEALTH_PATH="/"

            bash ./scripts/deploy.sh
          EOF
```

## Reusable Quality Gate Workflow

Save as `.github/workflows/quality-gate.yml`.

```yaml
name: Quality Gate

on:
  pull_request:
    branches:
      - main
      - develop

jobs:
  quality-gate:
    name: Lint -> Typecheck -> Build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"
          cache: "npm"

      - name: Install dependencies
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Type check
        run: npm run typecheck

      - name: Build
        run: npm run build
```

## Codex Prompt For Another Project

Use this prompt in Codex if you want it to generate the same structure in a different repository.

```text
Inspect this repository and set up a reusable production deployment pipeline modeled on a Docker-based GitHub Actions + VM SSH deployment.

Requirements:
- Add or update a production Dockerfile appropriate for this project.
- Add a deployment script at scripts/deploy.sh.
- The deployment script must:
  - fail fast
  - build a Docker image
  - preserve the currently running container as a previous-stable backup
  - start the new container
  - verify health with both container state and HTTP checks
  - automatically roll back if the deployment fails
  - clean up old containers and images after success
- Add a GitHub Actions workflow at .github/workflows/deploy-production.yml triggered by pushes to production.
- Add a quality gate workflow that runs lint, typecheck, and build if those commands exist in the repo.
- Document the full setup in docs/.
- Use the actual commands and runtime entrypoints from this repository instead of assuming a generic app.
- Keep secrets in GitHub Actions secrets, not in committed files.
- Prefer a reusable, template-friendly setup with env vars for APP_NAME, PROJECT_DIR, HOST_PORT, CONTAINER_PORT, DOCKERFILE, DEPLOY_BRANCH, and HEALTH_PATH.

Before editing, inspect:
- package.json or equivalent manifest
- Docker-related files
- app start command
- build command
- health endpoint or best available path

After editing:
- summarize what you created
- list required GitHub secrets
- call out any assumptions that still need user confirmation
```

## Validation checklist after reuse

Before relying on the new pipeline, verify:

1. `npm run build` works locally.
2. `docker build -t <app-name> .` works locally.
3. `docker run -p 3000:3000 <app-name>` starts correctly.
4. The health endpoint returns `200`.
5. The VM path in the workflow is correct.
6. The GitHub secrets are present.
7. A test push to the deploy branch completes successfully.
