# [Vulnerability Title]

> **Status:** Resolved / Disclosure approved
> **Severity:** Critical / High / Medium / Low
> **CVSS:** `0.0` — `CVSS:3.1/...`
> **Class:** e.g. IDOR, XSS, Info Disclosure
> **Date:** YYYY-MM

> Sanitization note: target names, endpoints, and identifiers are redacted.
> Only publish writeups for findings that are resolved and where the program
> permits disclosure.

## Summary

One or two sentences: what the bug is and why it matters.

## Impact

What an attacker can actually do. Tie it to real consequences (data exposure,
account takeover, financial loss), not theoretical risk.

## Steps to Reproduce

1. ...
2. ...
3. ...

Include minimal request/response evidence with sensitive values redacted.

```http
GET /api/REDACTED/12345 HTTP/2
Host: REDACTED
Authorization: Bearer REDACTED
```

## Root Cause

Why the vulnerability exists (missing authorization check, trusting client
input, etc.).

## Remediation

What fixes it.

## Timeline

- YYYY-MM-DD — Reported
- YYYY-MM-DD — Triaged
- YYYY-MM-DD — Resolved
- YYYY-MM-DD — Disclosure approved
