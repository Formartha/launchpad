---
name: launchpad-orchestrator
description: "Internal rules for STATE.md. Every skill reads these at start and end. Never invoked directly."
---

# Orchestrator Rules

Shared ruleset. Not standalone. Every skill follows at start and end.

## Phase Order

```
discover → brain → architect → implement → test → done
```

No skipping.

## On Skill Start: Read STATE.md

1. Check `.launchpad/features/[feature]/STATE.md` exists.
   - Missing → first run. Only `brain` may init. Else stop: "Feature not set up. Run `/launchpad-brain` first."
2. Read `## Current Phase`.
3. Verify phase allows this skill. Allowed transitions:
   - `discover` → `/launchpad-brain` only
   - `brain` → `/launchpad-architect` only
   - `architect` → `/launchpad-implement` only
   - `implement` → `/launchpad-test` only
   - `test` → done (archive in test skill)
   - `done` → no further skills
4. Wrong phase → stop. Tell user exactly what to run.
   Example: "'login' is in **brain** phase. Run `/launchpad-architect` next."

## On Skill End: Write STATE.md

1. Open `.launchpad/features/[feature]/STATE.md`.
2. Update `## Current Phase` to completed phase.
3. In `## Phases` table, update completed row:
   - **Status**: `not started` → `completed`
   - **Date**: `YYYY-MM-DD`
   - **Summary**: one sentence — what was done/decided
4. Edit only that row. Nothing else.

## Initializing STATE.md (brain only)

When `/launchpad-brain` starts new feature:
1. Copy `templates/STATE.md` exactly — no structure changes.
2. Replace `{{feature-name}}`.
3. All rows: `not started`, date `—`, summary `—`.
4. Save to `.launchpad/features/[feature-name]/STATE.md`.
