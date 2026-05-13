# Agent Toolkit

A small pattern library for reusable implementation prompts and project notes.

This repository currently stores markdown guides that capture working patterns from a Next.js App Router codebase and turn them into reusable instructions for future projects. It is best treated as an internal toolkit for engineering reuse, not as a runnable application.

## What Is In This Repo

- `prompts/ROBOTS_SITEMAP_PATTERN.md`
  Captures a `robots.txt` and sitemap implementation pattern for a Next.js App Router project, including route structure, API dependencies, reuse notes, and a copyable implementation prompt.

- `prompts/FETCH_PATTERN.md`
  Documents a server-side data-fetching architecture using `React.cache()`, shared layout fetches, ISR/revalidation, typed fetch helpers, and metadata mapping patterns.

- `prompts/DEPLOYMENT_CICD_REUSE.md`
  Describes a production deployment workflow with Docker, a VM-based deploy script, GitHub Actions, rollback behavior, health checks, and reusable workflow templates.

## Purpose

Use this repository to:

- preserve implementation patterns that are worth repeating
- convert working code structure into reusable engineering prompts
- give agents and developers a stable place to copy from when setting up similar projects

## Repository Structure

```text
agent-toolkit/
  prompts/
    DEPLOYMENT_CICD_REUSE.md
    FETCH_PATTERN.md
    ROBOTS_SITEMAP_PATTERN.md
```

## How To Use

1. Open the relevant file in `prompts/`.
2. Read the documented pattern and its project-specific caveats.
3. Reuse the included prompt, code structure, or deployment template in the target codebase.
4. Adjust route names, environment variables, endpoints, ports, and app-specific behavior before applying it elsewhere.

## Current Scope

Right now this repo is documentation-only:

- no application source code
- no package manager files
- no test suite
- no build or runtime entrypoint

If the toolkit grows, a future structure could include categorized prompts, example implementations, and validation checklists.

## Contributing

When adding a new pattern:

- prefer concrete implementation notes over generic advice
- include the real files, routes, or APIs involved
- call out any project-specific mismatches or cleanup needed before reuse
- end with a reusable prompt or template when possible

## Status

This repository is currently a minimal internal knowledge base for reusable engineering patterns.
