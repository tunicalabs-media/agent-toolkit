# Agent Toolkit

A lightweight repository of reusable prompts and agent skills for Next.js and frontend engineering. This is documentation-only and intended as an internal toolkit for repeatable implementation work, not a runnable app.

## What Is In This Repo

### Prompts

- [prompts/DEPLOYMENT_CICD_REUSE.md](prompts/DEPLOYMENT_CICD_REUSE.md) - Docker + VM deployment workflow with GitHub Actions, health checks, rollback flow, and reusable templates.
- [prompts/FETCH_PATTERN.md](prompts/FETCH_PATTERN.md) - Server-first data fetching, ISR/revalidation, shared layout fetches, typed helpers, and metadata mapping.
- [prompts/ROBOTS_SITEMAP_PATTERN.md](prompts/ROBOTS_SITEMAP_PATTERN.md) - App Router robots.txt + sitemap pattern with routes, dependencies, and a copyable prompt.

### Skills

Agent skill packs live in the skills folder. Each skill has a definition document that describes scope and usage rules.

| Skill                       | Focus                                                                                                          | Use Cases                                                                      | Definition                                                                                 |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| api-and-data-patterns       | Data fetching, API layering, and typed responses                                                               | Add route handlers, service fetches, and typed response shapes.                | [skills/api-and-data-patterns/SKILL.md](skills/api-and-data-patterns/SKILL.md)             |
| component-quality-check     | Accessibility and component quality checks for React/Tailwind UI                                               | Review UI changes for a11y, composability, and styling consistency.            | [skills/component-quality-check/SKILL.md](skills/component-quality-check/SKILL.md)         |
| fetch-pattern               | Canonical data-layer rules; see [skills/fetch-pattern/fetch_pattern.md](skills/fetch-pattern/fetch_pattern.md) | Any data fetching, metadata, ISR, or API integration work.                     | [skills/fetch-pattern/SKILL.md](skills/fetch-pattern/SKILL.md)                             |
| find-skills                 | Discover and install skills using the Skills CLI                                                               | Find new skills for a domain or workflow and install them.                     | [skills/find-skills/SKILL.md](skills/find-skills/SKILL.md)                                 |
| frontend-implementation     | Feature implementation workflow with RSC boundaries and checks                                                 | Build new pages, layouts, and shared components with project conventions.      | [skills/frontend-implementation/SKILL.md](skills/frontend-implementation/SKILL.md)         |
| frontend-ui-engineering     | Production-quality UI engineering guidance                                                                     | Refine UI layout, accessibility, and interaction polish to production quality. | [skills/frontend-ui-engineering/SKILL.md](skills/frontend-ui-engineering/SKILL.md)         |
| next-best-practices         | Next.js best practices and rule index                                                                          | Validate file conventions, RSC boundaries, and runtime rules for Next.js.      | [skills/next-best-practices/SKILL.md](skills/next-best-practices/SKILL.md)                 |
| ui-ux-pro-max               | UI/UX design intelligence across styles and stacks                                                             | Pick visual style, typography, color systems, and UX guidelines for a UI.      | [skills/ui-ux-pro-max/SKILL.md](skills/ui-ux-pro-max/SKILL.md)                             |
| vercel-react-best-practices | Performance guidelines from Vercel Engineering                                                                 | Performance refactors, bundle optimization, and rendering improvements.        | [skills/vercel-react-best-practices/SKILL.md](skills/vercel-react-best-practices/SKILL.md) |

### References

- [reference.md](reference.md) - External skill references and sources.

## How To Use

1. Pick the prompt or skill that matches the task.
2. Read the scope and non-negotiable rules in the linked document.
3. Apply the pattern in your target project and adjust routes, endpoints, and environment variables as needed.

## Getting Started With Skills (Copilot)

1. Start with the skill that best matches the task in the table above.
2. Read the definition document and follow its scope and mandatory rules.
3. Apply the guidance in the target codebase and keep changes focused.
4. If you need a missing capability, use the Skills CLI to discover and install new skills:

```bash
npx skills find <topic>
npx skills add <owner/repo@skill>
```

For curated sources, see [reference.md](reference.md).

## Current Scope

This repository is documentation-only:

- No application source code
- No package manager files
- No test suite
- No build or runtime entrypoint

## Contributing

When adding a new prompt or skill:

- Prefer concrete, project-tested guidance over generic advice
- Include the real files, routes, or APIs involved
- Call out project-specific constraints or cleanup steps
- End with a reusable checklist or prompt when possible

## Status

Minimal internal knowledge base for reusable engineering patterns and agent skills.
