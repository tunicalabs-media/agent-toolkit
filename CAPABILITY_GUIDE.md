# Skill and Prompt Capability Guide

This guide explains what each skill or prompt is capable of and what kind of improvement you should expect when using it. Use it as a practical companion to the indexes in [`README.md`](README.md).

## How To Read This Guide

- **Use when** tells you the situation where the asset fits best.
- **Improves** describes the engineering outcome it is designed to create.
- **Best paired with** suggests complementary assets for stronger results.

## Core Engineering Prompts

| Prompt | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`AGENT_CONTEXT_EFFICIENCY.md`](prompts/AGENT_CONTEXT_EFFICIENCY.md) | The agent is working in a large repo, producing too much output, or burning context on broad reads. | Lower token use, cleaner investigation, fewer repeated file reads, better summaries, and more focused edits. | `context-engineering`, `SYSTEMATIC_DEBUGGING.md` |
| [`NEXTJS_PRODUCTION_ENGINEER.md`](prompts/NEXTJS_PRODUCTION_ENGINEER.md) | You want a strong default prompt for implementing or refactoring production Next.js features. | Better App Router boundaries, UI quality, accessibility, secure defaults, performance awareness, and verification discipline. | `frontend-ui-engineering`, `vercel-react-best-practices`, `webapp-testing` |
| [`ENGINEERING_REVIEW_CHECKLIST.md`](prompts/ENGINEERING_REVIEW_CHECKLIST.md) | You want a repo-wide or feature-level review beyond syntax and style. | Better architecture, maintainability, reliability, testing, observability, and long-term cost decisions. | `code-review-excellence`, `context-engineering` |
| [`SYSTEMATIC_DEBUGGING.md`](prompts/SYSTEMATIC_DEBUGGING.md) | A bug, failing test, broken build, or production issue needs careful diagnosis. | Less guessing, clearer reproduction, stronger root-cause analysis, smaller fixes, and better verification. | `AGENT_CONTEXT_EFFICIENCY.md`, `webapp-testing` |
| [`TEST_STRATEGY.md`](prompts/TEST_STRATEGY.md) | You need to decide what tests to add or how much coverage is useful. | Better risk-based test selection across unit, integration, component, E2E, and contract tests. | `webapp-testing`, `code-review-excellence` |
| [`ARCHITECTURE_DECISION_RECORD.md`](prompts/ARCHITECTURE_DECISION_RECORD.md) | A decision affects architecture, vendors, data contracts, caching, deployment, or security posture. | Clearer tradeoffs, decision history, future maintainability, and fewer repeated debates. | `ENGINEERING_REVIEW_CHECKLIST.md` |
| [`NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md`](prompts/NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md) | You need a deep security audit of a Next.js app with Strapi, Contentful, WordPress, WooCommerce, CMS content, webhooks, or checkout flows. | Stronger security findings with evidence, better coverage of CMS/commerce trust boundaries, and prioritized remediation. | `security-nextjs`, `owasp-security` |

## Workflow and Context Skills

| Skill | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`context-engineering`](skills/context-engineering/README.md) | Starting a new agent session, switching tasks, or recovering from context confusion. | Better project context, clearer constraints, fewer hallucinations, cleaner handoffs, and stronger task continuity. | `AGENT_CONTEXT_EFFICIENCY.md` |
| [`find-skills`](skills/find-skills/README.md) | The library does not cover a domain and you want to discover an external skill. | Faster capability discovery and better skill selection instead of inventing workflows from scratch. | `reference.md` |
| [`code-review-excellence`](skills/code-review-excellence/README.md) | Reviewing code, pull requests, architecture changes, or test quality. | More useful review comments, better severity labeling, stronger bug/security/performance detection, and healthier review culture. | `ENGINEERING_REVIEW_CHECKLIST.md`, `TEST_STRATEGY.md` |

## Frontend and UI Skills

| Skill | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`frontend-ui-engineering`](skills/frontend-ui-engineering/README.md) | Building or polishing user-facing frontend interfaces. | Better layout, responsive behavior, accessibility, state handling, loading/error states, and interaction quality. | `NEXTJS_PRODUCTION_ENGINEER.md`, `webapp-testing` |
| [`frontend-design`](skills/frontend-design/README.md) | A page or component needs stronger visual direction and less generic styling. | Better visual hierarchy, typography, composition, aesthetic differentiation, and product feel. | `frontend-ui-engineering`, `tailwind-design-system` |
| [`component-quality-check`](skills/component-quality-check/README.md) | Reviewing a React/Tailwind component for readiness. | Better accessibility, composability, API design, styling consistency, and final UI checks. | `code-review-excellence` |
| [`animation-best-practices`](skills/animation-best-practices/README.md) | Adding hover states, button feedback, tooltips, transitions, or fixing flickery motion. | Smoother motion, better timing/easing, fewer animation bugs, and improved accessibility on touch/keyboard interactions. | `frontend-ui-engineering` |
| [`tailwind-design-system`](skills/tailwind-design-system/README.md) | Creating or standardizing a Tailwind CSS v4 design system. | Better token design, theming, component variants, dark mode, and scalable Tailwind conventions. | `frontend-design`, `component-quality-check` |

## React and Next.js Skills

| Skill | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`vercel-react-best-practices`](skills/vercel-react-best-practices/README.md) | Reviewing React/Next.js performance, rendering, server/client behavior, or bundle size. | Better performance decisions, fewer render regressions, leaner bundles, safer server behavior, and stronger hydration patterns. | `NEXTJS_PRODUCTION_ENGINEER.md` |
| [`react-best-practices`](skills/react-best-practices/README.md) | You want a general React performance and maintainability rule pack. | Better async flows, rendering behavior, JavaScript performance, and client/server data-fetching patterns. | `code-review-excellence` |
| [`frontend-react-best-practices`](skills/frontend-react-best-practices/README.md) | You need a compact React rule set for components, hooks, re-renders, and composition. | Better component performance, fewer hook mistakes, and cleaner composition patterns. | `component-quality-check` |
| [`vercel-composition-patterns`](skills/vercel-composition-patterns/README.md) | Component APIs are becoming overloaded with flags or hard-to-maintain state. | Better compound components, provider-driven state, explicit variants, and long-term API maintainability. | `ENGINEERING_REVIEW_CHECKLIST.md` |
| [`next-best-practices`](skills/next-best-practices/README.md) | You need focused Next.js reference rules for files, RSC, async APIs, metadata, images, scripts, or self-hosting. | Fewer framework mistakes, better App Router correctness, and more accurate implementation choices. | `NEXTJS_PRODUCTION_ENGINEER.md` |
| [`nextjs-app-router-patterns`](skills/nextjs-app-router-patterns/README.md) | Building or migrating App Router features with Server Components, streaming, parallel routes, and route handlers. | Better App Router architecture, streaming patterns, routing decisions, and data-fetching structure. | `next-best-practices` |

## Data, API, and Fetching Skills

| Skill or Prompt | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`api-and-data-patterns`](skills/api-and-data-patterns/README.md) | Adding route handlers, service functions, typed responses, or data-driven pages. | Cleaner API boundaries, stronger typing, better server/client separation, and more resilient data access. | `FETCH_PATTERN.md`, `NEXTJS_PRODUCTION_ENGINEER.md` |
| [`fetch-pattern`](skills/fetch-pattern/README.md) | Implementing fetch, ISR, metadata, or API integration work in a Next.js App Router project. | More consistent data fetching, cache/revalidation choices, metadata composition, and typed helper patterns. | `api-and-data-patterns` |
| [`FETCH_PATTERN.md`](prompts/FETCH_PATTERN.md) | You want a standalone copyable prompt for server-first data fetching patterns. | Faster reuse of canonical fetch, ISR, metadata, and API-layer conventions. | `fetch-pattern` |

## Security Skills and Prompts

| Skill or Prompt | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`security-nextjs`](skills/security-nextjs/README.md) | Auditing Next.js env vars, Server Actions, middleware/proxy, API routes, and headers. | Fewer Next.js-specific security footguns and better protection of server-only behavior. | `NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md` |
| [`owasp-security`](skills/owasp-security/README.md) | Reviewing broad web security concerns. | Better protection against OWASP Top 10 risks such as broken access control, injection, auth failures, SSRF, and misconfiguration. | `security-nextjs` |
| [`mobile-security-coder.md`](prompts/mobile-security-coder.md) | Implementing or reviewing mobile security patterns. | Better secure storage, WebView hardening, mobile auth, device API handling, and client-side privacy controls. | `owasp-security` |

## Testing, Verification, and Mobile

| Skill or Prompt | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`webapp-testing`](skills/webapp-testing/README.md) | You need browser verification of local web app behavior. | Better UI confidence through Playwright-style navigation, screenshots, console logs, and interaction checks. | `TEST_STRATEGY.md`, `SYSTEMATIC_DEBUGGING.md` |
| [`react-native-best-practices`](skills/react-native-best-practices/README.md) | Working on React Native performance or native/mobile bottlenecks. | Better FPS, TTI, memory use, bundle size, native profiling, and animation performance. | `mobile-security-coder.md` |

## Deployment and Platform Prompts

| Prompt | Use When | Improves | Best Paired With |
| --- | --- | --- | --- |
| [`DEPLOYMENT_CICD_REUSE.md`](prompts/DEPLOYMENT_CICD_REUSE.md) | You need reusable Docker + VM deployment and GitHub Actions guidance. | Better deployment repeatability, health checks, rollback flow, and CI/CD structure. | `ENGINEERING_REVIEW_CHECKLIST.md` |
| [`ROBOTS_SITEMAP_PATTERN.md`](prompts/ROBOTS_SITEMAP_PATTERN.md) | Implementing App Router robots.txt and sitemap patterns. | Better SEO file generation, route coverage, and reusable implementation steps. | `next-best-practices` |

## Recommended Default Stack

For most serious Next.js projects, start with:

1. [`AGENT_CONTEXT_EFFICIENCY.md`](prompts/AGENT_CONTEXT_EFFICIENCY.md)
2. [`context-engineering`](skills/context-engineering/README.md)
3. [`NEXTJS_PRODUCTION_ENGINEER.md`](prompts/NEXTJS_PRODUCTION_ENGINEER.md)
4. [`code-review-excellence`](skills/code-review-excellence/README.md)
5. [`TEST_STRATEGY.md`](prompts/TEST_STRATEGY.md)
6. [`webapp-testing`](skills/webapp-testing/README.md)
7. [`security-nextjs`](skills/security-nextjs/README.md)
8. [`NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md`](prompts/NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md) when CMS, commerce, auth, checkout, or webhooks are involved.

This combination improves how the agent thinks, what it reads, what it builds, how it verifies, and how it reviews the result.
