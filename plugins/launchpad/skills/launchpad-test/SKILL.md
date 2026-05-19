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

**What it tests:** Does the feature do what FEATURE.md says it should?

Read `## Test Scenarios` in `.launchpad/features/[feature-name]/FEATURE.md`.

For each scenario:
- Write a test that directly verifies it.
- Run it.
- Report: `✓ [scenario]` or `✗ [scenario] — [what failed]`

**On failure:**
- Explain in plain language what broke.
- Ask: "Fix it now, or note for later?"
- Fix → fix, re-run, confirm pass.
- Note → add note to FEATURE.md under that scenario.

---

## Agent 2: Non-Functional

**What it tests:** How the feature performs, feels, and behaves under real conditions.

Run checks across these dimensions — skip any that don't apply to the feature:

| Check | What to verify |
|---|---|
| **Performance** | Response time under normal load. Flag anything obviously slow. |
| **Usability** | Is the flow clear to a non-developer? Any confusing steps or dead ends? |
| **Accessibility** | Basic a11y: keyboard nav, labels, contrast, screen reader hints. |
| **Reliability** | Does it behave consistently across repeated runs? |
| **Error handling** | What happens on bad input, missing data, network failure? Is the error clear? |

For each check:
- State what you tested.
- Report: `✓ [check]` or `✗ [check] — [issue found]`
- Flag severity: low / medium / high.

**On high-severity failure:** Ask user whether to fix now or continue.

---

## Agent 3: Security

**What it tests:** Common vulnerabilities and unsafe patterns in the implementation.

Run checks relevant to the feature's stack and inputs — skip any that don't apply:

| Check | What to verify |
|---|---|
| **Input validation** | All user inputs sanitized. No raw input passed to commands, queries, or eval. |
| **Authentication** | Protected routes/functions require auth. No auth bypass possible. |
| **Authorization** | Users can only access/modify their own data. No privilege escalation. |
| **Injection** | No SQL, shell, or template injection vectors. Parameterized queries used. |
| **Sensitive data** | No secrets, tokens, or PII logged or exposed in responses. |
| **Dependencies** | No known vulnerable packages used (flag if detectable). |
| **HTTPS / transport** | External calls use HTTPS. No mixed content. |

For each check:
- State what you tested.
- Report: `✓ [check]` or `✗ [check] — [vulnerability found]`
- Flag severity: low / medium / **critical**.

**On critical:** Stop and fix immediately before continuing. Do not archive a feature with a critical security issue open.

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
