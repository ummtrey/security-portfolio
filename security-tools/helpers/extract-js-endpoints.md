# Reviewing JavaScript for Endpoints

JavaScript files on a target frequently reveal API routes, internal endpoints,
feature flags, and occasional references to staging hosts. Reading them is a
high-value, low-noise recon step. This is how I approach it.

## Why it matters

The front-end has to know where to send its requests, so those paths are
written into the JS - including endpoints that aren't linked anywhere in the
visible UI. Finding them expands the attack surface without touching the target
beyond loading pages a normal user would.

## What I look for

- **API routes** - anything starting with `/api`, `/v1`, `/v2`, `/graphql`
- **Absolute URLs** - `https://...` references, especially to other hosts
- **Path-like strings** - string literals that look like routes (`/admin/...`,
  `/internal/...`, `/user/...`)
- **Feature flags and config** - values that hint at hidden or gated features
- **Hardcoded values** - keys, tokens, or IDs that shouldn't be client-side

## How to collect the JS

Save the JS files served by the target (via the browser's dev tools Network
tab, or by requesting them directly), then read through them. For minified
bundles, a quick way to surface candidates is to grep for path- and URL-like
strings rather than reading line by line.

Useful patterns to search for:

- `https?://[^"'` + "`" + `\s]+` - full URLs
- `"/[A-Za-z0-9_\-./]+"` - quoted path-like strings
- `/(api|v\d|graphql)/` - likely API routes

## Turning leads into findings

Every path found this way is a **lead, not a confirmed endpoint**. The next
step is to request each one (within scope) and see:

- Does it exist and respond?
- Does it require authentication that it should?
- Does it expose data or actions the current role shouldn't have?

That's where endpoints found in JS often turn into IDOR, broken access control,
or information-disclosure findings.

