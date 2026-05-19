---
name: launchpad-implement
description: "Builds the feature by following the architecture plan in FEATURE.md. Narrates progress as it works."
---

# Implement

Build the feature step by step, following FEATURE.md. Narrate each step clearly.

## Steps

### 1. Ask which feature
Ask: "Which feature are we building?" Wait for the answer. Use that as `[feature-name]`.

### 2. Orchestrator — start
Follow On Skill Start rules in `skills/launchpad-orchestrator/SKILL.md`. Verify `architect` phase is complete.
If not: stop and tell the user what to run first.

### 3. Show the plan
Read `.launchpad/features/[feature-name]/FEATURE.md`.
Show the Steps list and ask: "I'll follow these steps — want to change anything before I start?"
If yes: update FEATURE.md steps, then confirm.

### 4. Implement
Work through each step in order:
- Say what you are doing in plain language before doing it.
- Write the code.
- Say "Done." when the step is complete.

Only create files listed in FEATURE.md.

### 5. Orchestrator — end
Follow On Skill End rules in `skills/launchpad-orchestrator/SKILL.md`. Mark `implement` complete in STATE.md.

### 6. Close
"All steps done. Want me to run the tests now, or would you prefer to review the code first?"

- Yes / now → continue directly into the `/launchpad-test` skill steps.
- No / later → "Run `/launchpad-test` when you're ready."
