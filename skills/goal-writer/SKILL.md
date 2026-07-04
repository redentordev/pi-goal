---
name: goal-writer
description: Draft or review strong /goal objectives for pi-goal. Use when the user wants a pasteable long-running goal with concrete completion criteria, verification, constraints, boundaries, and blocked-stop behavior.
---

# Goal Writer

Write `/goal` prompts as durable completion contracts, not broad wishes. The agent will reuse the objective across continuations, so the goal must say what done means and what evidence proves it.

A strong goal includes:

1. **Outcome** — the end state that must be true.
2. **Verification** — files, tests, commands, screenshots, logs, reports, PR checks, or other evidence to inspect.
3. **Constraints** — behavior, APIs, data, UX, performance, or security properties that must not regress.
4. **Boundaries** — allowed and forbidden files, tools, systems, credentials, generated artifacts, or scope.
5. **Iteration policy** — how to choose the next action and what to re-check between attempts.
6. **Blocked stop condition** — when to stop honestly with evidence, attempts, blocker, and needed input.

## Workflow

- Prefer a single pasteable Pi command: `/goal ...` or `/goal --tokens 50k ...`.
- Read relevant repo/docs/issues when the verification surface depends on them; do not invent commands or gates.
- Ask clarifying questions only when missing facts materially change outcome, verification, or boundaries.
- Make safe assumptions explicit when speed matters.
- After drafting, briefly show how the six parts are covered.

## Template

```text
/goal <desired end state>, verified by <specific evidence>, while preserving <constraints>. Use <allowed scope/tools> and avoid <forbidden scope>. Between iterations, <next-action policy and what to re-check>. If blocked or no defensible path remains, stop with <evidence gathered, attempted paths, blocker, and next input needed>.
```

## Completion-audit contract

Require the agent to map each explicit requirement to concrete evidence before completion. Tests, green checks, manifests, or heavy implementation effort are proxy signals; they prove completion only when they cover every requirement. If evidence is missing or uncertain, the goal is not complete.

## Checklist

Before returning a goal, confirm it is pasteable and answers:

- Can the agent tell when all work is done?
- Can the user independently audit the completion claim?
- Are important regressions and forbidden approaches named?
- Does the goal permit iteration without unlimited drift?
- Does it define what to do when tests, credentials, product decisions, or external data block progress?
