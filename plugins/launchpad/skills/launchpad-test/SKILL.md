---
name: launchpad-test
description: "Tests feature against scenarios in FEATURE.md. Reports results, fixes failures, offers to archive when complete."
---

# Test

Run tests for each scenario in FEATURE.md. Report pass/fail. Fix failures. Offer archive when done.

## Steps

### 1. Ask feature name
"Which feature are we testing?" Wait. Use as `[feature-name]`.

### 2. Orchestrator — start
Follow On Skill Start in `skills/launchpad-orchestrator/SKILL.md`. Verify `implement` complete.
Blocked → tell user what to run first.

### 3. Show scenarios
Read `## Test Scenarios` in `.launchpad/features/[feature-name]/FEATURE.md`.
"I'll verify these — ready?"

### 4. Run tests
Each scenario:
- Write test. Run. Report: `✓ [scenario]` or `✗ [scenario] — [what failed]`

### 5. Handle failures
Failure → explain in plain language.
"Fix this, or note for later?"
- Fix → fix, re-run, confirm pass.
- Note → add note to FEATURE.md under scenario.

### 6. Update FEATURE.md
Mark each scenario `✓` or `✗` (with note if failed).

### 7. Orchestrator — end
Follow On Skill End in `skills/launchpad-orchestrator/SKILL.md`. Mark `test` complete.

### 8. Archive offer
"All done with '[feature-name]'. Mark complete and archive?"

Yes:
- Follow On Skill End → mark `done` in STATE.md.
- Create `.launchpad/completed/` if missing.
- Move `.launchpad/features/[feature-name]/` → `.launchpad/completed/[feature-name]/`.
- "'[feature-name]' archived. What's next?"

No: "Feature stays active. Come back anytime."
