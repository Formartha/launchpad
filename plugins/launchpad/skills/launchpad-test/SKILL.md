---
name: launchpad-test
description: "Tests the implemented feature against the scenarios defined in FEATURE.md. Reports results, offers to fix failures, and offers to archive the feature when complete."
---

# Test

Write and run tests for each scenario in FEATURE.md. Report clearly what passed and what failed. Offer to fix failures. When all is done, offer to archive the feature.

---

## Steps

### 1. Ask which feature
Ask: "Which feature are we testing?"

Wait for the answer. Use that as `[feature-name]`.

### 2. Orchestrator — start
Follow the On Skill Start rules in `skills/orchestrator/SKILL.md`. Verify `implement` phase is complete.
If not: stop and tell the user what to run first.

### 3. Show scenarios
Read the `## Test Scenarios` section of `.launchpad/features/[feature-name]/FEATURE.md`.
Show the list and say: "I'll verify these scenarios — ready?"

### 4. Write and run tests
For each scenario:
- Write a test that verifies it.
- Run it.
- Report the result: `✓ [scenario]` or `✗ [scenario] — [what went wrong]`

### 5. Handle failures
If any test fails:
- Explain what failed in plain language.
- Ask: "Want me to fix this, or note it for later review?"
- If fix: fix it, re-run the test, confirm it passes.
- If note: add a note to FEATURE.md under that scenario.

### 6. Update FEATURE.md
In the `## Test Scenarios` section, mark each scenario with its result:
- `✓` for passing
- `✗` for failing (with a short note)

### 7. Orchestrator — end
Follow the On Skill End rules in `skills/orchestrator/SKILL.md`. Mark `test` as completed in STATE.md.

### 8. Offer to archive
Ask: "All done with '[feature-name]'. Want to mark it as complete and archive it?"

If yes — archive the feature:
- Follow the On Skill End rules in `skills/orchestrator/SKILL.md`. Mark `done` as completed in STATE.md.
- Create `.launchpad/completed/` if it does not exist.
- Move `.launchpad/features/[feature-name]/` → `.launchpad/completed/[feature-name]/`.
- Tell the user: "'[feature-name]' is archived. What are you building next?"

If no — tell the user: "No problem. The feature stays in active features. You can come back anytime."
