# Testing Workflow

My general flow once recon is done and I have a mapped target.

## Account setup

- Two test accounts minimum, so I can test cross-account authorization
- A low-privilege and (where possible) a higher-privilege account for vertical checks
- Clean browser profile + Burp with scoped traffic only

## Pass 1 — walk the app as a user

Use every feature the way a normal user would, with Burp capturing everything.
This builds the request map and surfaces object references, state transitions,
and anything that looks like it trusts the client.

## Pass 2 — authorization

This is usually where the value is, so it gets dedicated attention:

- Replay account A's object references using account B's session (IDOR)
- Try privileged endpoints with a normal-user token (vertical)
- Swap identifiers in API calls, including UUIDs (don't assume they're safe)
- Look for mass assignment by adding fields the UI never sends

## Pass 3 — input and injection

Systematically hit inputs for XSS, SQLi, SSTI, SSRF, etc. — guided by where
recon and Pass 1 suggested the app does interesting server-side work.

## Pass 4 — business logic

The bugs no scanner finds. Price/quantity tampering, race conditions on
limited actions, skipping workflow steps, replaying one-time operations.

## Confirm before reporting

Every finding gets reproduced from a clean session before I write it up. A bug
I can't reproduce deterministically isn't ready to submit.

## Notes discipline

I keep per-target notes: what I tested, what was negative, and what's still
open. Negative results matter — they stop me re-testing the same thing and they
show coverage.

