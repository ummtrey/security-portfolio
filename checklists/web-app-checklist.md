# Web Application Bug Bounty Checklist

A working checklist I run through on web targets. Not every item applies to
every program — always read the scope and rules first.

## 0. Pre-engagement

- [ ] Read the program policy, scope, and out-of-scope list end to end
- [ ] Note what's explicitly forbidden (automated scanning, rate limits, PII, social engineering)
- [ ] Record in-scope domains, apps, and asset types
- [ ] Set up a dedicated test account (and a second one for IDOR/authz testing)
- [ ] Configure Burp scope so nothing out-of-scope is touched

## 1. Recon & asset discovery

- [ ] Enumerate subdomains (subfinder, passive sources)
- [ ] Resolve and probe live hosts (httpx)
- [ ] Capture historical URLs (gau / wayback)
- [ ] Check for subdomain takeover candidates (subzy)
- [ ] Identify tech stack, frameworks, versions
- [ ] Find staging/dev/test hosts and non-prod environments
- [ ] Review JS files for endpoints, API routes, hardcoded values

## 2. Authentication

- [ ] Username enumeration via login/reset/registration responses
- [ ] Password policy and rate limiting on login
- [ ] Account lockout behavior
- [ ] Password reset token: predictability, expiry, reuse, host-header poisoning
- [ ] Session fixation after login
- [ ] MFA bypass paths (if present)
- [ ] OAuth: redirect_uri validation, state parameter, token leakage via Referer

## 3. Session management

- [ ] Session cookie flags (HttpOnly, Secure, SameSite)
- [ ] Session invalidation on logout / password change
- [ ] Token entropy and scope
- [ ] JWT: algorithm confusion, `none` alg, weak secret, missing signature check
- [ ] JWT: inspect claims for over-broad permissions

## 4. Authorization (the high-value area)

- [ ] IDOR on every object reference (IDs, UUIDs, filenames)
- [ ] Horizontal: access another user's data with your session
- [ ] Vertical: access admin/privileged functions as a normal user
- [ ] Forced browsing to hidden endpoints
- [ ] Mass assignment / parameter pollution to elevate role
- [ ] API: method tampering (GET vs POST vs PUT on same resource)

## 5. Input handling

- [ ] Reflected / stored / DOM XSS across inputs and sinks
- [ ] SQL injection (error-based, boolean/time blind, second-order)
- [ ] SSTI in templated responses
- [ ] Command injection in anything that touches the OS
- [ ] SSRF in URL/fetch/webhook parameters
- [ ] XXE where XML is parsed
- [ ] Open redirect in redirect/next/return params
- [ ] Path traversal in file parameters

## 6. Business logic

- [ ] Price / quantity manipulation in cart or checkout flows
- [ ] Negative numbers, overflow, type confusion
- [ ] Race conditions on limited actions (coupons, transfers, redemptions)
- [ ] Workflow step skipping / out-of-order requests
- [ ] Replay of one-time actions

## 7. Information disclosure

- [ ] Sensitive data in responses (`__NEXT_DATA__`, inline JSON, HTML comments)
- [ ] Verbose errors and stack traces
- [ ] Internal hostnames, IPs, infra metadata
- [ ] Exposed `.git`, backup files, config files
- [ ] API responses returning more fields than the UI shows

## 8. Reporting

- [ ] Reproduce from a clean session to confirm
- [ ] Capture minimal, clear steps + request/response evidence
- [ ] Assess real impact (not just theoretical)
- [ ] Assign CVSS with justified vector
- [ ] Write up per the program's required format
- [ ] Remove any collateral test data you created

