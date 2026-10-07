# Recon Methodology

How I approach reconnaissance on a new target. The goal is coverage of the
attack surface before spending time on any single bug class.

## Scope first

Everything starts with the program scope. I build two lists: in-scope assets
(wildcards, apex domains, specific apps) and the hard out-of-scope list. Burp's
target scope gets configured to match so I don't accidentally probe anything I
shouldn't.

## Passive enumeration

Passive sources first, because they're quiet and often enough:

```
subfinder -d target.com -all -silent -o subs.txt
```

Then historical URLs for endpoints that aren't linked anywhere anymore:

```
gau target.com | tee urls.txt
```

JS files are worth a careful read — they frequently reveal API routes, internal
endpoints, feature flags, and the occasional reference to a staging host.

## Resolution and probing

Resolve and find what's actually alive:

```
cat subs.txt | httpx -silent -title -status-code -tech-detect -o live.txt
```

I pay attention to:

- Non-production hosts (`dev-`, `staging-`, `test-`, `uat-`)
- Odd ports and admin panels
- Hosts with unusual tech stacks vs the rest of the estate

## Takeover candidates

Dangling DNS pointing at unclaimed services:

```
cat subs.txt | subzy run --targets -
```

## Prioritization

Not all surface is equal. I rank what to dig into by:

1. Authenticated application functionality (richest authz surface)
2. APIs backing the main app
3. Anything handling money, files, or other users' data
4. Non-prod environments (often weaker controls)

Only after mapping do I start on specific bug classes — context from recon
usually tells me where the interesting logic lives.

