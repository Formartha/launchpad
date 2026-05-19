---
name: orchestrator
description: "Internal rules for reading and writing STATE.md. Every skill follows these rules at start and end. Never invoked directly by the user."
---

# Orchestrator Rules

The orchestrator is not a standalone skill. It is a shared ruleset that every skill must follow at the start and end of its execution.

---

## Phase Order

```
discover → brain → architect → implement → test → done
```

Each phase must be completed in order. No skipping.

---

## On Skill Start: Read STATE.md

1. Check if `.launchpad/features/[feature]/STATE.md` exists.
   - If not: this is the first skill run for this feature. Only `brain` is allowed to initialize a new feature. If a different skill is running, stop and say: "This feature has not been set up yet. Run `/brain` first."
2. Read the `## Current Phase` value.
3. Check the phase is correct for the skill about to run. Allowed transitions:
   - `discover` phase → only `/brain` may proceed next
   - `brain` phase → only `/architect` may proceed next
   - `architect` phase → only `/implement` may proceed next
   - `implement` phase → only `/test` may proceed next
   - `test` phase → only `/done` may proceed next
   - `done` phase → feature is complete, no further skills allowed
4. If the skill is not allowed: stop immediately and tell the user exactly which skill to run next.
   Example: "The 'login' feature is in the **brain** phase. Run `/architect` next."

---

## On Skill End: Write STATE.md

After the skill successfully completes its work:

1. Open `.launchpad/features/[feature]/STATE.md`.
2. Update `## Current Phase` to the phase just completed.
3. In the `## Phases` table, find the row for the completed phase and update:
   - **Status**: `not started` → `completed`
   - **Date**: today's date in `YYYY-MM-DD` format
   - **Summary**: one sentence describing what was done or decided in this phase
4. Do not edit any other row or any other part of the file.

---

## Initializing STATE.md (brain only)

When `/brain` starts a new feature:

1. Copy `templates/STATE.md` exactly — do not change the structure.
2. Replace `{{feature-name}}` with the actual feature name.
3. Leave all rows as `not started` with `—` for date and summary.
4. Save to `.launchpad/features/[feature-name]/STATE.md`.
