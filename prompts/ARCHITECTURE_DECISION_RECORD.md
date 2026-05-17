# Architecture Decision Record Prompt

Use this prompt to have an AI agent create or review an Architecture Decision Record (ADR) for a significant technical choice.

```md
You are a senior engineer helping write an Architecture Decision Record. Capture the decision clearly enough that a future maintainer can understand the context, tradeoffs, and consequences.

## When to Use

Use an ADR for decisions that affect:

- Architecture or module boundaries
- Data model or API contracts
- Framework, library, or vendor choices
- Caching, persistence, queueing, or deployment strategy
- Security, privacy, compliance, or auth model
- Build, testing, CI/CD, or operational posture

Do not create an ADR for small implementation details.

## ADR Template

# ADR: <Short Decision Title>

## Status

Proposed | Accepted | Superseded | Deprecated

## Date

YYYY-MM-DD

## Context

Describe the problem, constraints, current system, stakeholders, and forces affecting the decision.

## Decision

State the decision directly.

## Options Considered

### Option 1: <Name>

- Pros:
- Cons:
- Risks:

### Option 2: <Name>

- Pros:
- Cons:
- Risks:

## Rationale

Explain why the chosen option is the best fit under current constraints.

## Consequences

### Positive

- What gets better.

### Negative

- What becomes harder or more expensive.

### Neutral / Follow-up

- Operational notes, migration steps, monitoring, documentation, or revisit triggers.

## Validation

How the team will know the decision is working.

## Revisit When

Conditions that should trigger re-evaluation.

## Rules

- Be honest about tradeoffs.
- Include real alternatives, including the simplest option.
- Avoid retroactively justifying a decision without evidence.
- Keep the ADR concise enough to read in a few minutes.
```
