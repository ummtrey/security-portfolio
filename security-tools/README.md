# security-tools

Small helper scripts I use to speed up the repetitive parts of recon and
triage during authorized bug bounty and pentest work.

These are convenience wrappers around well-known open-source tools
(subfinder, httpx, subzy, gau). They don't do anything a person couldn't do by
hand  -  they just chain the standard steps and keep output organized per target.

## Contents

- **[`recon/recon.md`](./recon/recon.md)**  -  passive subdomain enum -> live-host
  probing -> takeover check -> historical URLs, into a per-target folder
- **[`helpers/extract-js-endpoints.md`](./helpers/extract-js-endpoints.md)**  - 
  pull candidate endpoints/paths out of a saved JS file

## Requirements

`subfinder`, `httpx`, `subzy`, and `gau` on `$PATH` (ProjectDiscovery tools
install to `~/go/bin`). Python 3 for the helper.

## Scope reminder

Only run these against assets you are explicitly authorized to test under a
program's scope. Recon tooling still generates traffic to the target  -  respect
rate limits and out-of-scope lists.

