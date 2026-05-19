---
name: implement
description: "Builds the feature by following the architecture plan in FEATURE.md. Narrates progress as it works."
---

# Implement

Build the feature step by step, following FEATURE.md. Narrate progress clearly so the user knows what is happening.

---

## Steps

### 1. Ask which feature
Ask: "Which feature are we building?"

Wait for the answer. Use that as `[feature-name]`.

### 2. Orchestrator — start
Follow the On Skill Start rules in `skills/orchestrator/SKILL.md`. Verify `architect` phase is complete.
If not: stop and tell the user what to run first.

### 3. Show the plan
Read `.launchpad/features/[feature-name]/FEATURE.md`.
Show the Steps list to the user and ask: "I'll follow these steps — want to change anything before I start?"

If the user wants changes: update FEATURE.md steps accordingly, then confirm.

### 4. Implement
Work through each step in order. For each step:
- Say what you are doing in plain language before doing it.
- Write the code.
- Say "Done." when the step is complete.

Stay strictly within the files listed in FEATURE.md. Do not create files not listed there.

### 5. Orchestrator — end
Follow the On Skill End rules in `skills/orchestrator/SKILL.md`. Mark `implement` as completed in STATE.md.

### 6. Close
Tell the user: "All steps done. Run `/launchpad:test` to verify everything works."
