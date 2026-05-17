# Frontend React Best Practices

## Download Source
`npx skills add https://github.com/sergiodxa/agent-skills --skill frontend-react-best-practices`

## What This Skill Does
Frontend React Best Practices provides React performance and composition guidance for agents writing, reviewing, or refactoring components. It covers bundle size, re-render behavior, hydration, hooks, client patterns, and component composition.

## Features
- Rule index for bundle optimization, re-render reduction, and rendering performance.
- Hooks and composition guidance for maintainable React component APIs.
- Focused rule files with concrete bad/good examples.

## Typical Use Cases
- Reviewing React components for avoidable re-renders or bundle bloat.
- Refactoring hook usage, memoization, or client-only rendering behavior.
- Improving component composition without over-abstracting APIs.

## Files Included
- `SKILL.md` - Skill trigger rules and summarized rule catalog.
- `rules/` - Detailed React best-practice rule files.

## Notes
This skill overlaps with `react-best-practices` and `vercel-react-best-practices`, but is more compact and includes explicit composition and hook rules.
