# Pi Goal

Minimal goal tracking and auto-continuation for Pi: start a goal, pause/resume it, check progress, and let the agent continue until it calls the completion tool.

Published npm package: `@redentor_dev/pi-goal`.

## Install

From npm:

```bash
pi install npm:@redentor_dev/pi-goal
```

## Commands

- `/goal <objective>` — start a new goal and immediately kick off work.
- `/goal --tokens 50k <objective>` — start with a token budget (`k` and `m` suffixes supported).
- `/goal` or `/goal status` — show objective, status, iteration, token use, and active time.
- `/goal pause` — pause the active goal and stop auto-continuation.
- `/goal resume` — resume a paused or budget-limited goal and queue the next continuation.
- `/goal clear` or `/goal stop` — clear the current goal and remove the footer status.

## How it works

- Goal state is persisted only as Pi session custom entries (`pi-goal`); no external state files are written.
- When the agent finishes a turn while a goal is active, the extension queues one follow-up user message to continue work.
- Optional token budgets stop continuation with `budget_limited` status. Budget exhaustion never marks the goal complete.
- Reloading, resuming, or otherwise starting a session with an active stored goal pauses it first. Use `/goal resume` to continue intentionally.
- The footer shows compact status such as `goal: active 18k/100k`, `goal: paused`, or `goal: budget-limited`.

## `complete_goal` tool

The package registers one tool: `complete_goal`.

The agent should call it with `{ "summary": "..." }` only after an evidence-backed audit proves the objective is fully satisfied. The prompt contract tells the agent not to use passing tests, elapsed effort, low budget, or partial progress as completion by themselves.

## Compatibility

Works alongside `@redentor_dev/pi-orchestrator`. The packages have no shared dependency, and this package uses only `/goal` and `complete_goal`, avoiding `/team`, `delegate_researcher`, `delegate_implementor`, `delegate_design`, and `review_diff`.

## Credits

Prior art and design references:

- Michaelliv/pi-goal
- @narumitw/pi-goal
- pi-codex-goal

## License

MIT © 2026 Redentor Valerio
