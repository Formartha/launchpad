---
name: launchpad-implement
description: "Builds the feature following FEATURE.md. Narrates progress as it works."
---

# Implement

Build feature step by step per FEATURE.md. Narrate each step clearly.

## Steps

### 1. Ask feature name
"Which feature are we building?" Wait. Use as `[feature-name]`.

### 2. Orchestrator — start
Follow On Skill Start in `skills/launchpad-orchestrator/SKILL.md`. Verify `architect` complete.
Blocked → tell user what to run first.

### 3. Show plan
Read `.launchpad/features/[feature-name]/FEATURE.md`.
Show Steps list. "I'll follow these — want to change anything before I start?"
Changes requested → update FEATURE.md, confirm.

### 4. Build
Each step in order:
- Say what you're doing (plain language).
- Write code.
- "Done." when step complete.

Only create files listed in FEATURE.md.

### 5. Orchestrator — end
Follow On Skill End in `skills/launchpad-orchestrator/SKILL.md`. Mark `implement` complete.

### 6. Close
"All steps done. Run `/launchpad-test` to verify."
