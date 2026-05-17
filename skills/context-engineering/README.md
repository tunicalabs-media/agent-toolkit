# Context Engineering

## Download Source
`npx skills add https://github.com/addyosmani/agent-skills --skill context-engineering`

## What This Skill Does
Context Engineering helps set up and maintain high-quality agent context. It covers project rule files, specs, architecture summaries, relevant source inclusion, error-output handling, conversation hygiene, and recovery strategies when requirements or context become unclear.

## Features
- Context hierarchy for rules, specs, source files, errors, and conversation state.
- Strategies for packing context without overwhelming the agent.
- Anti-patterns, red flags, and verification guidance for long-running sessions.

## Typical Use Cases
- Starting a new coding-agent session on a large project.
- Preparing focused context for a bug fix, feature, or migration.
- Recovering when an agent starts hallucinating, contradicting requirements, or losing task state.

## Files Included
- `SKILL.md` - Complete context setup and session-management workflow.

## Notes
This is a meta-skill: it improves how other skills and prompts are applied rather than targeting one framework.
