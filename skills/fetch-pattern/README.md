# Fetch Pattern

## Download Source
Not listed in `reference.md`; local repository skill.

## What This Skill Does
Fetch Pattern captures this repository’s canonical approach to data fetching, metadata composition, ISR/revalidation, and API-layer work in Next.js App Router projects. It directs agents to use a shared reference document before changing fetch logic.

## Features
- Server-first fetch guidance for App Router workflows.
- Rules for metadata, ISR, revalidation, and typed helper functions.
- Shared reference pattern for consistent data integration across projects.

## Typical Use Cases
- Implementing a new data-backed page or layout.
- Adding metadata generation based on fetched content.
- Normalizing API calls around a consistent fetch helper pattern.

## Files Included
- `SKILL.md` - Trigger rules and non-negotiable fetch-pattern requirements.
- `fetch_pattern.md` - Detailed canonical pattern and reusable implementation guidance.

## Notes
This local skill is project-opinionated. Read `fetch_pattern.md` before applying it to a new codebase.
