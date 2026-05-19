---
name: launchpad-state
description: "Shared rules for reading and writing STATE.md. Every skill follows these at start and end. Never invoked directly."
disable-model-invocation: true
user-invocable: false
---

# State Rules

Not a standalone skill. Shared ruleset every skill must follow at start and end of execution.

## Phase Order

```
discover → brain → architect → implement → test → done
```

Each phase must be completed in order. No skipping.

## On Skill Start: Read STATE.md

1. Check if `.launchpad/features/[feature]/STATE.md` exists.
   - If not: only `brain` may initialize a new feature. Any other skill → stop and say: "Feature not set up yet. Run `/launchpad-brain` first."
2. Read `## Current Phase`.
3. Verify the phase allows this skill. Allowed transitions:
   - `discover` → `/launchpad-brain` only
   - `brain` → `/launchpad-architect` only
   - `architect` → `/launchpad-implement` only
   - `implement` → `/launchpad-test` only
   - `test` → done (handled inside test skill)
   - `done` → no further skills allowed
4. Wrong phase → stop and tell the user exactly what to run next.
   Example: "The 'login' feature is in the **brain** phase. Run `/launchpad-architect` next."

## On Skill End: Write STATE.md

After the skill successfully completes:

1. Open `.launchpad/features/[feature]/STATE.md`.
2. Update `## Current Phase` to the completed phase.
3. In `## Phases` table, update the completed row:
   - **Status**: `not started` → `completed`
   - **Date**: today in `YYYY-MM-DD` format
   - **Summary**: one sentence — what was done or decided
4. Edit only that row. Nothing else.

## Initializing STATE.md (brain only)

When `/launchpad-brain` starts a new feature:

1. Copy `templates/STATE.md` exactly — do not change structure.
2. Replace `{{feature-name}}` with the actual name.
3. All rows: `not started`, date `—`, summary `—`.
4. Save to `.launchpad/features/[feature-name]/STATE.md`.
