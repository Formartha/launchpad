---
name: launchpad-test-functional
description: "Functional testing rulebook. Defines all checks for verifying a feature does what it claims. Referenced by launchpad-test. Never invoked directly."
disable-model-invocation: true
user-invocable: false
---

# Functional Testing Rules

Verify the feature behaves exactly as described in FEATURE.md. Cover happy paths, edge cases, and failure paths.

## Check Categories

### Happy Path
- Each scenario in `## Test Scenarios` passes end-to-end.
- Output matches expected result for valid inputs.
- State changes correctly (data saved, UI updates, redirects fire).

### Edge Cases
- Empty input — what happens with nothing?
- Minimum valid input — does it work at the boundary?
- Maximum valid input — does it work at the other boundary?
- Repeated actions — what if the user does the same thing twice?
- Out-of-order actions — what if steps happen in wrong order?

### Failure Paths
- Invalid input — error is shown, not a crash.
- Missing required data — handled gracefully.
- Action fails mid-way — system left in consistent state, not partial.

### Integration
- Feature works with adjacent features (if any listed in FEATURE.md Files section).
- No regressions in existing functionality touched by new files.

### Data
- Data written is readable back correctly.
- Data deleted is actually gone.
- Data not meant to change is unchanged.

## Reporting Format

For each check:
```
✓ [check name] — [brief note if noteworthy]
✗ [check name] — [what failed] [severity: low | medium | high]
```

On failure: explain in plain language. Ask user: fix now or note for later?
