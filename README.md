# bug-bounty-notes

My working notes, checklists, and sanitized writeups from bug bounty hunting.

I'm a bug bounty hunter (HackerOne: `ummtrey`, Intigriti: `trey708`) building
toward a penetration testing role. This repo is where I keep the methodology I
actually use, so it's a living document rather than a copy of a textbook.

## Contents

- **[`checklists/`](./checklists)** — the lists I run through on real targets
  - [`web-app-checklist.md`](./checklists/web-app-checklist.md)
  - [`api-checklist.md`](./checklists/api-checklist.md)
- **[`methodology/`](./methodology)** — how I approach recon and testing
  - [`recon-methodology.md`](./methodology/recon-methodology.md)
  - [`testing-workflow.md`](./methodology/testing-workflow.md)
- **[`writeups/`](./writeups)** — sanitized writeups of resolved findings

## Disclosure & ethics

Everything here is for authorized testing within bug bounty program scope only.
Writeups are published **only** when a finding is resolved and the program
permits disclosure, and all target names and identifiers are redacted. Nothing
in this repo targets any system I'm not authorized to test.

## Toolkit

Burp Suite, subfinder, httpx, nuclei, subzy, gau, interactsh — run from a Kali
VM. Learning stack: PortSwigger Web Security Academy, TCM Security, TryHackMe.

