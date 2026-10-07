# Recon Commands Reference

The recon steps I run on an authorized target, in order, with the exact
commands. This is a reference I follow by hand - run only against assets you
are explicitly authorized to test, and respect the program's rate limits and
out-of-scope list.

## 1. Passive subdomain enumeration

Find subdomains from passive sources (quiet, no direct traffic to the target):

```
subfinder -d target.com -all -silent -o subs.txt
```

## 2. Probe for live hosts

Resolve the subdomains and see which are actually up, with title, status code,
and detected tech:

```
cat subs.txt | httpx -silent -title -status-code -tech-detect -o live.txt
```

What I look for in the results:

- Non-production hosts (`dev-`, `staging-`, `test-`, `uat-`)
- Odd ports and admin panels
- Hosts running a different tech stack than the rest of the estate

## 3. Check for subdomain takeover

Look for dangling DNS records pointing at unclaimed services:

```
cat subs.txt | subzy run --targets -
```

## 4. Collect historical URLs

Pull URLs that may no longer be linked anywhere but still resolve - old
endpoints are often less maintained:

```
gau target.com | sort -u > urls.txt
```

## Tools used

| Tool | Purpose |
|------|---------|
| [subfinder](https://github.com/projectdiscovery/subfinder) | Passive subdomain enumeration |
| [httpx](https://github.com/projectdiscovery/httpx) | Live-host probing and tech detection |
| [subzy](https://github.com/PentestPad/subzy) | Subdomain takeover detection |
| [gau](https://github.com/lc/gau) | Historical URL collection |

ProjectDiscovery tools install to `~/go/bin`. I run these from a Kali Linux VM.

## Prioritization

After mapping, I dig in roughly in this order:

1. Authenticated application functionality (richest authorization surface)
2. APIs backing the main app
3. Anything handling money, files, or other users' data
4. Non-prod environments (often weaker controls)

