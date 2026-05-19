---
name: launchpad-test-security
description: "Security testing rulebook. Defines checks across OWASP top 10, auth, data exposure, dependencies. Referenced by launchpad-test. Never invoked directly."
disable-model-invocation: true
user-invocable: false
---

# Security Testing Rules

Identify vulnerabilities before they reach production. Skip checks that don't apply to the feature's stack or context.

## Input Validation
- All user inputs validated server-side (not only client-side).
- No raw user input passed to shell commands, SQL queries, eval(), or template engines.
- File uploads (if any): type, size, and content validated. Stored outside web root.
- URL parameters and headers treated as untrusted.

## Injection
- SQL: parameterized queries or ORM used. No string concatenation into queries.
- Command injection: no shell exec with user-controlled input.
- XSS: output encoded for the correct context (HTML, JS, URL, CSS). No innerHTML with user data.
- Template injection: no user input rendered in server-side templates unescaped.
- Path traversal: file paths sanitized, no `../` sequences escape intended directory.

## Authentication
- Protected endpoints require valid auth token/session.
- No auth bypass via URL manipulation, missing checks, or default credentials.
- Tokens expire and are invalidated on logout.
- Brute force not trivially possible (rate limiting or lockout exists or is noted as needed).

## Authorization
- Users can only access/modify resources they own.
- Role checks enforced server-side, not only in UI.
- Horizontal privilege escalation tested (user A accessing user B's data).
- Vertical privilege escalation tested (regular user accessing admin functions).

## Sensitive Data
- Passwords stored hashed (bcrypt, argon2) — never plaintext.
- Secrets and API keys not hardcoded in source, not logged, not returned in responses.
- PII not logged unnecessarily.
- Sensitive data not exposed in URLs (query params, path segments).
- HTTP responses don't leak stack traces, internal paths, or server versions.

## Session Management
- Session tokens are random, long, and unpredictable.
- CSRF protection on state-changing requests (if applicable).
- Session invalidated on logout and on password change.

## Dependencies
- No packages with known critical CVEs used (flag if detectable from package files).
- No unnecessary permissions requested (mobile/desktop apps).

## Transport
- All external calls use HTTPS.
- No mixed content (HTTPS page loading HTTP resources).
- Cookies have Secure, HttpOnly, and SameSite flags where applicable.

## Error Handling
- Error messages shown to users don't reveal implementation details.
- 404 vs 403 used correctly (don't confirm existence of resources to unauthorized users).

## Reporting Format

For each check:
```
✓ [check] — [note]
✗ [check] — [vulnerability] [severity: low | medium | critical]
```

**Critical:** Stop all other testing. Fix before proceeding. Do NOT archive with a critical open.
**Medium:** Flag, ask user whether to fix now or log as known issue.
**Low:** Log in results, continue.
