# Agent Toolkit Skill Library

A curated Skill / Prompt Library for reusable agent workflows, frontend engineering guidance, security reviews, testing flows, framework-specific implementation patterns, and standalone prompts.

This repository is documentation-only. It does not contain a runnable application; instead, it organizes skills as portable instruction packs that developers and coding agents can browse, reuse, install, or adapt into other projects.

## Overview

Skills live under [`skills/`](skills). Each skill folder contains a `SKILL.md` definition and, where useful, supporting rule files, references, scripts, or assets. Standalone reusable prompts live under [`prompts/`](prompts). The root catalog helps you discover the right asset quickly, while each skill-level `README.md` provides a short documentation page with source, purpose, features, use cases, and included files.

Use this library when you want repeatable agent behavior for:

- React, Next.js, Tailwind, and frontend implementation work
- Web application testing and UI verification
- Security audits and secure coding workflows
- React Native and Remotion domain guidance
- Skill discovery, context setup, and prompt reuse

## Structure

```text
.
├── README.md
├── reference.md
├── prompts/
│   └── <prompt-name>.md
└── skills/
    ├── <skill-name>/
    │   ├── README.md
    │   ├── SKILL.md
    │   └── optional supporting files
    └── ...
```

Common supporting files include:

- `rules/` for granular best-practice documents.
- `references/` for deeper examples, images, or implementation notes.
- `AGENTS.md` for compiled agent-facing rule sets.
- `scripts/` for helper checks or scans.
- `assets/` for test helpers and reusable fixtures.

## When To Use What

Use this table when you are choosing the best skill or prompt for a task.

| Situation | Use | Type | Why |
| --- | --- | --- | --- |
| Reducing token/context waste during agent work | [AGENT_CONTEXT_EFFICIENCY.md](prompts/AGENT_CONTEXT_EFFICIENCY.md) | Prompt | Portable rules for targeted search, compact working memory, concise tool output, and context checkpoints. |
| Starting work in an unfamiliar repo | [context-engineering](skills/context-engineering/README.md) | Skill | Helps pack project context, rules, constraints, and task state before coding. |
| Implementing production Next.js features | [NEXTJS_PRODUCTION_ENGINEER.md](prompts/NEXTJS_PRODUCTION_ENGINEER.md) | Prompt | Best default prompt for App Router, UI quality, secure defaults, and performance basics. |
| Building or polishing user-facing UI | [frontend-ui-engineering](skills/frontend-ui-engineering/README.md) | Skill | Improves layout, accessibility, responsive behavior, state, and interaction polish. |
| Creating a distinctive visual direction | [frontend-design](skills/frontend-design/README.md) | Skill | Useful when the UI needs stronger visual design, not just correct implementation. |
| Reviewing React performance or rendering | [vercel-react-best-practices](skills/vercel-react-best-practices/README.md) | Skill | Broad React/Next.js performance rule pack for bundles, rendering, server work, and hydration. |
| Reviewing component architecture | [vercel-composition-patterns](skills/vercel-composition-patterns/README.md) | Skill | Helps avoid boolean prop sprawl and design better compound/component APIs. |
| Reviewing a PR or local diff | [code-review-excellence](skills/code-review-excellence/README.md) | Skill | Structured review process for correctness, tests, security, performance, and feedback quality. |
| Doing a repo-wide engineering review | [ENGINEERING_REVIEW_CHECKLIST.md](prompts/ENGINEERING_REVIEW_CHECKLIST.md) | Prompt | Looks beyond code style into architecture, reliability, maintainability, tests, and operations. |
| Debugging a failing feature or test | [SYSTEMATIC_DEBUGGING.md](prompts/SYSTEMATIC_DEBUGGING.md) | Prompt | Forces reproduction, localization, hypotheses, root cause, narrow fix, and verification. |
| Planning test coverage | [TEST_STRATEGY.md](prompts/TEST_STRATEGY.md) | Prompt | Chooses unit, integration, component, E2E, and contract tests based on risk. |
| Auditing Next.js security with CMS/commerce | [NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md](prompts/NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md) | Prompt | Deep audit flow for Strapi, Contentful, WordPress, WooCommerce, webhooks, rich content, and checkout/order risks. |
| Checking broad web security basics | [owasp-security](skills/owasp-security/README.md) | Skill | Covers OWASP Top 10 risks and secure coding patterns. |
| Checking Next.js-specific security | [security-nextjs](skills/security-nextjs/README.md) | Skill | Focused checks for env exposure, Server Actions, middleware, API routes, and headers. |
| Validating a local web app in browser | [webapp-testing](skills/webapp-testing/README.md) | Skill | Playwright-style browser verification, screenshots, console logs, and UI debugging. |
| Documenting a major technical decision | [ARCHITECTURE_DECISION_RECORD.md](prompts/ARCHITECTURE_DECISION_RECORD.md) | Prompt | Captures decision context, alternatives, tradeoffs, consequences, and revisit triggers. |
| Building a Tailwind design system | [tailwind-design-system](skills/tailwind-design-system/README.md) | Skill | Tailwind v4 tokens, theming, component variants, and design-system conventions. |
| Working on React Native performance | [react-native-best-practices](skills/react-native-best-practices/README.md) | Skill | Mobile FPS, TTI, memory, bundle, native, and animation performance guidance. |
| Working on Remotion video code | [remotion-best-practices](skills/remotion-best-practices/README.md) | Skill | Frame-based animation, media assets, captions, audio, sequencing, and render checks. |
| Looking for a missing capability | [find-skills](skills/find-skills/README.md) | Skill | Discovers external skills when this library does not cover a workflow. |

## Prompt Index

Standalone prompts are reusable, copyable workflows that do not need the full skill folder structure.

| Prompt | Focus |
| --- | --- |
| [AGENT_CONTEXT_EFFICIENCY.md](prompts/AGENT_CONTEXT_EFFICIENCY.md) | Portable prompt for reducing token usage and context bloat in Codex, Copilot, Cursor, Antigravity, and similar coding agents. |
| [DEPLOYMENT_CICD_REUSE.md](prompts/DEPLOYMENT_CICD_REUSE.md) | Docker + VM deployment workflow with GitHub Actions, health checks, rollback flow, and reusable templates. |
| [ARCHITECTURE_DECISION_RECORD.md](prompts/ARCHITECTURE_DECISION_RECORD.md) | ADR prompt/template for documenting significant technical choices, tradeoffs, consequences, and revisit triggers. |
| [ENGINEERING_REVIEW_CHECKLIST.md](prompts/ENGINEERING_REVIEW_CHECKLIST.md) | Senior engineering review prompt for maintainability, architecture, reliability, testing, observability, and long-term cost. |
| [FETCH_PATTERN.md](prompts/FETCH_PATTERN.md) | Server-first data fetching, ISR/revalidation, shared layout fetches, typed helpers, and metadata mapping. |
| [NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md](prompts/NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md) | Repo-wide Next.js security audit prompt for Strapi, Contentful, WordPress, WooCommerce, webhooks, rich content, and commerce flows. |
| [NEXTJS_PRODUCTION_ENGINEER.md](prompts/NEXTJS_PRODUCTION_ENGINEER.md) | Consolidated Next.js production implementation prompt covering App Router, frontend quality, accessibility, secure defaults, and performance basics. |
| [ROBOTS_SITEMAP_PATTERN.md](prompts/ROBOTS_SITEMAP_PATTERN.md) | App Router robots.txt and sitemap pattern with routes, dependencies, and a copyable prompt. |
| [SYSTEMATIC_DEBUGGING.md](prompts/SYSTEMATIC_DEBUGGING.md) | Debugging prompt that forces reproduction, localization, hypotheses, root-cause fixes, and verification. |
| [TEST_STRATEGY.md](prompts/TEST_STRATEGY.md) | Risk-based test planning prompt for choosing unit, integration, component, E2E, and contract coverage. |
| [mobile-security-coder.md](prompts/mobile-security-coder.md) | Mobile security prompt for secure storage, WebView hardening, and mobile auth flows. |

## Skill Index

### Frontend and Design

| Skill | Description | Source |
| --- | --- | --- |
| [animation-best-practices](skills/animation-best-practices/README.md) | Practical CSS and UI animation guidance for smooth, accessible interactions. | `npx skills add https://github.com/millionco/react-doctor --skill animation-best-practices` |
| [component-quality-check](skills/component-quality-check/README.md) | Review checklist for accessible, composable React/Tailwind components. | Not listed in [`reference.md`](reference.md). |
| [frontend-design](skills/frontend-design/README.md) | High-quality visual design guidance for distinctive production web interfaces. | `npx skills add https://github.com/anthropics/skills --skill frontend-design` |
| [frontend-implementation](skills/frontend-implementation/README.md) | Next.js frontend implementation workflow with RSC boundaries and quality gates. | Not listed in [`reference.md`](reference.md). |
| [frontend-ui-engineering](skills/frontend-ui-engineering/README.md) | Production UI engineering guidance for layout, accessibility, state, and polish. | `npx skills add https://github.com/addyosmani/agent-skills --skill frontend-ui-engineering` |
| [tailwind-design-system](skills/tailwind-design-system/README.md) | Tailwind CSS v4 design-system patterns for tokens, theming, variants, and responsive UI. | Not listed in [`reference.md`](reference.md). |

### React and Next.js

| Skill | Description | Source |
| --- | --- | --- |
| [frontend-react-best-practices](skills/frontend-react-best-practices/README.md) | React performance and composition rules covering rendering, hooks, bundles, and client patterns. | `npx skills add https://github.com/sergiodxa/agent-skills --skill frontend-react-best-practices` |
| [next-best-practices](skills/next-best-practices/README.md) | Modular Next.js best-practice references for App Router, RSC, async APIs, metadata, images, and deployment concerns. | Not listed in [`reference.md`](reference.md). |
| [nextjs-app-router-patterns](skills/nextjs-app-router-patterns/README.md) | Next.js 14+ App Router patterns for Server Components, streaming, routes, and data fetching. | `npx skills add https://github.com/wshobson/agents --skill nextjs-app-router-patterns` |
| [react-best-practices](skills/react-best-practices/README.md) | Agent-optimized React performance rules across async work, bundles, server behavior, rendering, and JavaScript patterns. | See [`reference.md`](reference.md) for multiple source commands. |
| [vercel-composition-patterns](skills/vercel-composition-patterns/README.md) | Scalable React composition rules for compound components, explicit variants, and provider-driven state. | Not listed in [`reference.md`](reference.md). |
| [vercel-react-best-practices](skills/vercel-react-best-practices/README.md) | Vercel-flavored React and Next.js performance rules with a large compiled `AGENTS.md`. | `npx skills add https://github.com/vercel-labs/agent-skills --skill vercel-react-best-practices` |

### Data and APIs

| Skill | Description | Source |
| --- | --- | --- |
| [api-and-data-patterns](skills/api-and-data-patterns/README.md) | Next.js App Router data and API layering guidance with typed responses and server/client separation. | Not listed in [`reference.md`](reference.md). |
| [fetch-pattern](skills/fetch-pattern/README.md) | Canonical server-first fetch, ISR, metadata, and API integration rules. | Not listed in [`reference.md`](reference.md). |

### Security

| Skill | Description | Source |
| --- | --- | --- |
| [owasp-security](skills/owasp-security/README.md) | OWASP Top 10 secure coding patterns for authentication, access control, injection, SSRF, and configuration risks. | `npx skills add https://github.com/hoodini/ai-agents-skills --skill owasp-security` |
| [security-nextjs](skills/security-nextjs/README.md) | Next.js-specific security audit patterns for environment variables, Server Actions, middleware, API routes, and headers. | `npx skills add https://github.com/igorwarzocha/opencode-workflows --skill security-nextjs` |

### Testing, Media, and Mobile

| Skill | Description | Source |
| --- | --- | --- |
| [react-native-best-practices](skills/react-native-best-practices/README.md) | React Native performance guidance for FPS, TTI, memory, native bottlenecks, bundles, and animations. | `npx skills add https://github.com/callstackincubator/agent-skills --skill react-native-best-practices` |
| [remotion-best-practices](skills/remotion-best-practices/README.md) | Remotion video creation guidance for React-based compositions, assets, sequencing, captions, audio, and rendering. | `npx skills add https://github.com/remotion-dev/skills --skill remotion-best-practices` |
| [webapp-testing](skills/webapp-testing/README.md) | Playwright-oriented workflow for testing local web apps, inspecting browser behavior, and capturing screenshots. | See [`reference.md`](reference.md) for multiple source commands. |

### Agent Workflow

| Skill | Description | Source |
| --- | --- | --- |
| [code-review-excellence](skills/code-review-excellence/README.md) | Systematic code review skill for correctness, maintainability, security, performance, tests, and constructive feedback. | `npx skills add https://github.com/wshobson/agents --skill code-review-excellence` |
| [context-engineering](skills/context-engineering/README.md) | Agent context setup, context packing, rule-file strategy, and session hygiene. | `npx skills add https://github.com/addyosmani/agent-skills --skill context-engineering` |
| [find-skills](skills/find-skills/README.md) | Workflow for discovering, evaluating, and installing external agent skills with the Skills CLI. | `npx skills add https://github.com/vercel-labs/skills --skill find-skills` |

## Usage

### Install Skills

Use the source commands in [`reference.md`](reference.md) or in each skill README:

```bash
npx skills add <repo-url> --skill <skill-name>
```

Some skills in this repository are local/internal and do not currently have a source command in `reference.md`.

### Browse Skills

Start with the index above, then open the skill README for a quick overview. Read `SKILL.md` when you need the exact activation rules, workflow, or agent instructions.

### Browse Prompts

Use [`prompts/`](prompts) for lightweight reusable workflows that do not need supporting files. Prompts are useful for role setup, one-off implementation patterns, and repeatable review checklists.

### Reuse Prompts and Workflows

Copy or adapt skill folders into projects that support agent skills. Keep supporting files with the skill when they are referenced by `SKILL.md`, especially `rules/`, `references/`, `assets/`, and `scripts/`.

### Contribute New Skills

1. Create a new folder under `skills/` using kebab-case.
2. Add a `SKILL.md` with frontmatter, trigger guidance, and workflow instructions.
3. Add a skill-level `README.md` using the convention below.
4. Add supporting references, rules, scripts, or assets only when they make the skill easier to apply.
5. Update this root README and [`reference.md`](reference.md) with the new skill and source.

## Conventions

Each skill README should use this structure:

```md
# <Skill Name>

## Download Source
<original download/install command or GitHub link from reference.md>

## What This Skill Does
...

## Features
...

## Typical Use Cases
...

## Files Included
...

## Notes
...
```

Naming and organization rules:

- Use kebab-case folder names, matching the skill name where possible.
- Keep `SKILL.md` as the canonical agent instruction file.
- Keep standalone prompts in `prompts/` as one Markdown file per prompt.
- Put detailed rule documents in `rules/`.
- Put extended examples, images, and background material in `references/`.
- Keep helper scripts in `scripts/` and reusable browser/test files in `assets/`.
- Prefer concise, specific skill documentation over generic descriptions.

## References

- [`reference.md`](reference.md) tracks original download/install commands collected for this library.
