---
name: launchpad-test
description: "Tests the implemented feature. Runs functional, non-functional, and security tests against scenarios in FEATURE.md. Reports results, fixes failures, archives when complete."
when_to_use: "Use after /launchpad-implement has built the feature and the user is ready to verify it."
allowed-tools:
  - Bash
  - Read
  - Write
---

# Test

Three testing agents run in sequence: Functional, Non-Functional, Security.
Each has its own scope and pass criteria. All results written to FEATURE.md.

## Steps

### 1. Ask which feature
Ask: "Which feature are we testing?" Wait for the answer. Use that as `[feature-name]`.

### 2. State — start
Read `.launchpad/features/[feature-name]/STATE.md`. Verify `implement` phase is complete.
If not: stop. Tell the user to run `/launchpad-implement` first.

### 3. Choose test scope
Use the ask tool: "Which tests do you want to run?"
→ All three (Functional + Non-Functional + Security) — recommended
→ Functional only
→ Non-Functional only
→ Security only

Run only the selected agents. Always in order: Functional → Non-Functional → Security.

---

## Agent 1: Functional
Follow all checks defined in the `launchpad-test-functional` skill.
Read `## Test Scenarios` from FEATURE.md as the baseline scenario list.

## Agent 2: Non-Functional
Follow all checks defined in the `launchpad-test-nonfunctional` skill.
Skip checks that don't apply to this feature's context.

## Agent 3: Security
Follow all checks defined in the `launchpad-test-security` skill.
Skip checks that don't apply to this feature's stack.
**Critical findings block archiving — fix before proceeding.**

---

## After All Agents

### Update FEATURE.md
Add a `## Test Results` section with three subsections:
```
### Functional
[results]

### Non-Functional
[results]

### Security
[results]
```

### State — mark test complete
In `.launchpad/features/[feature-name]/STATE.md`:
- Update `## Current Phase` → `test`.
- Update test row: Status → `completed`, Date → today `YYYY-MM-DD`, Summary → overall result (e.g. "All functional pass. 1 non-functional medium. 0 security issues.").

### Archive offer
Ask: "All done with '[feature-name]'. Want to mark it complete and archive it?"

If yes:
- Update STATE.md: Current Phase → `done`, done row Status → `completed`, Date → today.
- Create `.launchpad/completed/` if it does not exist.
- Move `.launchpad/features/[feature-name]/` → `.launchpad/completed/[feature-name]/`.
- "'[feature-name]' is archived. What are you building next?"

If no: "Feature stays active. Come back anytime."
