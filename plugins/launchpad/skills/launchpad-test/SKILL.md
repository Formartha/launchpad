---
name: launchpad-test
description: "Tests the implemented feature against scenarios in FEATURE.md. Reports results, offers to fix failures, and offers to archive when complete."
---

# Test

Write and run tests for each scenario in FEATURE.md. Report what passed and what failed. Offer to fix failures. Offer to archive when done.

## Steps

### 1. Ask which feature
Ask: "Which feature are we testing?" Wait for the answer. Use that as `[feature-name]`.

### 2. State — start
Follow On Skill Start rules in `skills/launchpad-state/SKILL.md`. Verify `implement` phase is complete.
If not: stop and tell the user what to run first.

### 3. Show scenarios
Read `## Test Scenarios` in `.launchpad/features/[feature-name]/FEATURE.md`.
"I'll verify these scenarios — ready?"

### 4. Write and run tests
For each scenario:
- Write a test that verifies it.
- Run it.
- Report: `✓ [scenario]` or `✗ [scenario] — [what went wrong]`

### 5. Handle failures
If a test fails:
- Explain what failed in plain language.
- Follow the elicitation protocol in `skills/launchpad-elicit/SKILL.md` to ask: "Want me to fix this, or note it for later review?"
- Fix → fix, re-run, confirm pass.
- Note → add note to FEATURE.md under that scenario.

### 6. Update FEATURE.md
In `## Test Scenarios`, mark each result:
- `✓` for passing
- `✗` for failing (with short note)

### 7. State — end
Follow On Skill End rules in `skills/launchpad-state/SKILL.md`. Mark `test` complete in STATE.md.

### 8. Offer to archive
Ask: "All done with '[feature-name]'. Want to mark it complete and archive it?"

If yes:
- Follow On Skill End rules → mark `done` in STATE.md.
- Create `.launchpad/completed/` if it does not exist.
- Move `.launchpad/features/[feature-name]/` → `.launchpad/completed/[feature-name]/`.
- "'[feature-name]' is archived. What are you building next?"

If no: "The feature stays in active features. Come back anytime."
