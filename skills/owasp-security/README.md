# OWASP Security

## Download Source
`npx skills add https://github.com/hoodini/ai-agents-skills --skill owasp-security`

## What This Skill Does
OWASP Security provides secure coding practices based on the OWASP Top 10. It helps agents prevent common web vulnerabilities in authentication, authorization, cryptography, injection handling, configuration, dependency hygiene, logging, and SSRF protections.

## Features
- OWASP Top 10 risk overview with prevention patterns.
- Concrete TypeScript/Node examples for access control, password hashing, headers, and injection prevention.
- Security-review trigger guidance for common vulnerability classes.

## Typical Use Cases
- Reviewing an API or web application for OWASP Top 10 risks.
- Hardening authentication, authorization, sessions, and sensitive data handling.
- Adding input validation, safe database access, secure headers, or dependency checks.

## Files Included
- `SKILL.md` - OWASP-oriented secure coding guide with examples.

## Notes
Use this for broad web security concerns. For Next.js-specific audit checks, use `security-nextjs` alongside it.
