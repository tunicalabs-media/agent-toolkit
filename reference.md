# Skill Download Sources

This file tracks the original install commands for skills in this library.

Skills marked with `🌟` are recommended baseline additions because they help agents work better across most projects: better context, better discovery, better frontend implementation quality, stronger testing, and safer security review.

## Quick Decision Table

| Need | Recommended Skill or Prompt |
| --- | --- |
| Lower token/context usage for coding agents | `prompts/AGENT_CONTEXT_EFFICIENCY.md` |
| Better task setup and repo context | 🌟 `context-engineering` |
| Better code review and engineering judgment | 🌟 `code-review-excellence` |
| Production Next.js implementation | `prompts/NEXTJS_PRODUCTION_ENGINEER.md` |
| Repo-wide engineering review | `prompts/ENGINEERING_REVIEW_CHECKLIST.md` |
| Systematic debugging | `prompts/SYSTEMATIC_DEBUGGING.md` |
| Test planning | `prompts/TEST_STRATEGY.md` |
| Architecture decision records | `prompts/ARCHITECTURE_DECISION_RECORD.md` |
| Next.js CMS/commerce security audit | `prompts/NEXTJS_CMS_COMMERCE_SECURITY_AUDIT.md` |
| Browser/UI verification | 🌟 `webapp-testing` |
| Broad web security | 🌟 `owasp-security` |
| Next.js-specific security | 🌟 `security-nextjs` |
| React/Next.js performance review | 🌟 `vercel-react-best-practices` |
| UI implementation quality | 🌟 `frontend-ui-engineering` |

## Recommended Baseline Skills

| Skill | Install Command | Why It Is Useful |
| --- | --- | --- |
| 🌟 find-skills | `npx skills add https://github.com/vercel-labs/skills --skill find-skills` | Helps discover and install the right missing skill instead of guessing. |
| 🌟 context-engineering | `npx skills add https://github.com/addyosmani/agent-skills --skill context-engineering` | Improves project context, session setup, and task handoffs for agent work. |
| 🌟 code-review-excellence | `npx skills add https://github.com/wshobson/agents --skill code-review-excellence` | Improves review quality, catches bugs earlier, and raises engineering judgment across teams. |
| 🌟 frontend-ui-engineering | `npx skills add https://github.com/addyosmani/agent-skills --skill frontend-ui-engineering` | Raises baseline UI quality, accessibility, responsiveness, and implementation polish. |
| 🌟 vercel-react-best-practices | `npx skills add https://github.com/vercel-labs/agent-skills --skill vercel-react-best-practices` | Provides comprehensive React and Next.js performance review guidance. |
| 🌟 webapp-testing | `npx skills add https://github.com/anthropics/skills --skill webapp-testing` | Enables browser-based verification, screenshots, logs, and local UI debugging. |
| 🌟 owasp-security | `npx skills add https://github.com/hoodini/ai-agents-skills --skill owasp-security` | Adds broad secure-coding coverage for common web application risks. |
| 🌟 security-nextjs | `npx skills add https://github.com/igorwarzocha/opencode-workflows --skill security-nextjs` | Adds Next.js-specific security audit checks for env vars, Server Actions, middleware, and headers. |

## Frontend and UI Skills

| Skill | Install Command |
| --- | --- |
| frontend-design | `npx skills add https://github.com/anthropics/skills --skill frontend-design` |
| frontend-react-best-practices | `npx skills add https://github.com/sergiodxa/agent-skills --skill frontend-react-best-practices` |
| animation-best-practices | `npx skills add https://github.com/millionco/react-doctor --skill animation-best-practices` |

## React and Next.js Skills

| Skill | Install Command |
| --- | --- |
| react-best-practices | `npx skills add https://github.com/vercel/vercel-plugin --skill react-best-practices` |
| react-best-practices | `npx skills add https://github.com/0xbigboss/claude-code --skill react-best-practices` |
| react-best-practices | `npx skills add https://github.com/sickn33/antigravity-awesome-skills --skill react-best-practices` |
| nextjs-app-router-patterns | `npx skills add https://github.com/wshobson/agents --skill nextjs-app-router-patterns` |

## Testing and Mobile Skills

| Skill | Install Command |
| --- | --- |
| webapp-testing | `npx skills add https://github.com/github/awesome-copilot --skill webapp-testing` |
| react-native-best-practices | `npx skills add https://github.com/callstackincubator/agent-skills --skill react-native-best-practices` |

## Notes

- Some skills appear more than once because multiple repositories publish a skill with the same name.
- Local skills that do not have an original download source are documented in the root `README.md` and their own skill `README.md` files.
