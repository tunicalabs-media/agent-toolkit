# Security Next.js

## Download Source
`npx skills add https://github.com/igorwarzocha/opencode-workflows --skill security-nextjs`

## What This Skill Does
Security Next.js is a targeted audit skill for Next.js applications. It focuses on App Router and Server Action risks, including `NEXT_PUBLIC_*` exposure, `next.config.js` environment leaks, missing auth in Server Actions and API routes, middleware matcher gaps, and security headers.

## Features
- Next.js-specific checks for environment variable exposure and bundled secrets.
- Server Action, API route, middleware, and header audit patterns.
- Helper scan script for fast security-oriented searches.

## Typical Use Cases
- Auditing a Next.js app before launch.
- Checking whether secrets are accidentally exposed to the browser.
- Reviewing Server Actions, API routes, middleware, and `next.config.js` security posture.

## Files Included
- `SKILL.md` - Next.js security audit rules and examples.
- `scripts/scan.sh` - Helper script for scanning common Next.js security issues.

## Notes
Use this for framework-specific checks. Pair with `owasp-security` for broader application security review.
