---
name: launchpad-test-nonfunctional
description: "Non-functional testing rulebook. Defines checks for performance, usability, accessibility, reliability, compatibility. Referenced by launchpad-test. Never invoked directly."
disable-model-invocation: true
user-invocable: false
---

# Non-Functional Testing Rules

Verify HOW the feature behaves, not just what it does. Skip checks that don't apply to the feature's context.

## Performance
- Response time is acceptable under normal conditions (flag anything over 2s for UI, 500ms for API).
- No unnecessary blocking operations on the main thread.
- No N+1 query patterns or unbounded loops visible in implementation.
- Memory usage doesn't grow unbounded over repeated use.

## Usability
- A non-developer can complete the feature's core flow without instructions.
- Error messages explain what went wrong AND what to do next.
- No dead ends — user always has a path forward.
- Confirmation shown after destructive or important actions.
- Loading states shown for anything over ~300ms.

## Accessibility (a11y)
- Interactive elements reachable by keyboard (Tab, Enter, Escape).
- Form inputs have visible labels (not just placeholder text).
- Color is not the only way to convey information.
- Images have alt text.
- ARIA roles used where semantic HTML isn't sufficient.
- Focus order is logical.

## Reliability
- Same action produces same result across repeated runs.
- No flaky behavior tied to timing or order of operations.
- Feature degrades gracefully when a dependency is slow or unavailable.

## Compatibility
- Works in the target environments listed in PROJECT.md (browsers, OS, runtime versions).
- No hard-coded paths or environment-specific assumptions.
- Locale/timezone — does the feature break for non-default settings?

## Maintainability
- No hardcoded magic numbers or strings that should be constants.
- No dead code left behind in modified files.

## Reporting Format

For each check:
```
✓ [check] — [note]
✗ [check] — [issue] [severity: low | medium | high]
```

High severity: flag to user before moving on.
