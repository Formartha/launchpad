---
name: launchpad-implement
description: "Builds the feature by following the architecture plan in FEATURE.md. Narrates progress as it works."
when_to_use: "Use after /launchpad-architect has written FEATURE.md and the user is ready to build."
allowed-tools:
  - Bash
  - Read
  - Write
---

# Implement

Build the feature step by step, following FEATURE.md. Narrate each step clearly.

## Steps

### 1. Ask which feature
Ask: "Which feature are we building?" Wait for the answer. Use that as `[feature-name]`.

### 2. State — start
Read `.launchpad/features/[feature-name]/STATE.md`. Verify `architect` phase is complete.
If not: stop. Tell the user to run `/launchpad-architect` first.

### 3. Show the plan
Read `.launchpad/features/[feature-name]/FEATURE.md`.
Show the Steps list. Ask: "I'll follow these steps — want to change anything before I start?"
If yes: reflect the requested change, confirm, update FEATURE.md.

### 4. Implement
Work through each step in order:
- Say what you are doing in plain language before doing it.
- Write the code.
- Say "Done." when the step is complete.

Only create files listed in FEATURE.md.

### 5. State — mark implement complete
In `.launchpad/features/[feature-name]/STATE.md`:
- Update `## Current Phase` → `implement`.
- Update implement row: Status → `completed`, Date → today `YYYY-MM-DD`, Summary → one sentence of what was built.

### 6. Close
Use the ask tool: "All steps done. What's next?"
→ Run tests now (continue into `/launchpad-test`)
→ Review the code first (stop here)
