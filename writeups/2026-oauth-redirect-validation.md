# OAuth2 redirect_uri Validation Testing

> **Status:** Closed (sanitized for portfolio)
> **Severity:** Informational / Low (as triaged)
> **Class:** OAuth / Open Redirect surface
> **Date:** 2026

> Target names and endpoints redacted. Documented as a methodology example.

## Summary

Testing of an OAuth2 authorization flow's `redirect_uri` validation. The
objective was to determine whether the authorization server strictly matched
the registered redirect URI or allowed variations that could leak the
authorization code.

## What I tested

The `redirect_uri` parameter against common validation weaknesses:

- Exact-match vs prefix-match registration
- Appended paths and query strings on an allowed origin
- Subdomain and lookalike-domain variations
- Path traversal and encoded characters in the URI
- `redirect_uri` omission and parameter pollution

```http
GET /authorize?client_id=REDACTED
    &redirect_uri=https://REDACTED/callback/../attacker-controlled
    &response_type=code&state=REDACTED HTTP/2
Host: REDACTED
```

## Outcome

The behavior was reported and triaged. In this case it resolved as a
duplicate/informative  -  the validation gap was already known to the program.

## Lessons

- `redirect_uri` handling is one of the highest-value areas in any OAuth flow,
  because a leak of the authorization code can lead to account takeover.
- Always check the `state` parameter alongside `redirect_uri`  -  a missing or
  unvalidated `state` is a CSRF problem in its own right.
- Duplicates are part of the process; the methodology is still worth
  documenting even when the specific bug was already known.

