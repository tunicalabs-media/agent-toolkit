# Vercel React Best Practices

## Download Source
`npx skills add https://github.com/vercel-labs/agent-skills --skill vercel-react-best-practices`

## What This Skill Does
Vercel React Best Practices is a comprehensive React and Next.js performance rule pack optimized for agents. It covers async waterfalls, bundle analysis, Server Component behavior, Server Actions, client data fetching, re-render optimization, hydration, scripts, resource hints, JavaScript performance, and advanced React patterns.

## Features
- Large categorized rule set with critical, high, and medium-impact guidance.
- Compiled `AGENTS.md` for full agent-facing documentation.
- Metadata and granular rule files for maintaining or consuming the rule catalog.

## Typical Use Cases
- Auditing a React or Next.js app for performance and rendering issues.
- Refactoring server/client data flow, bundle imports, or expensive renders.
- Loading a comprehensive rule pack during agent-driven frontend reviews.

## Files Included
- `SKILL.md` - Skill trigger rules and summarized catalog.
- `AGENTS.md` - Compiled full rule document.
- `metadata.json` - Metadata for the rule pack.
- `rules/` - Individual rule files and templates.

## Notes
This is the broadest React performance skill in the library. Use the smaller `frontend-react-best-practices` skill when a more compact rule set is enough.
