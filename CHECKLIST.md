# Checklists

## Scope

- [ ] Program page read in full, twice
- [ ] In-scope assets listed
- [ ] Out-of-scope items listed
- [ ] Program focus noted (API auth? checkout? contracts?)
- [ ] Testing rules noted (fork only? no scanners? rate limits?)
- [ ] Reward table noted

## Subdomain enumeration

- [ ] Certificate transparency checked
- [ ] DNS records listed (A, AAAA, CNAME, MX, TXT, NS)
- [ ] Search engine results collected
- [ ] sublist3r run, output saved
- [ ] Dangling CNAMEs checked (and verified, not assumed)
- [ ] Every subdomain has a recorded source

## Live-host probing

- [ ] httpx run, output saved
- [ ] Status codes recorded as observed (including flaky 200/403)
- [ ] Hosts classified (app / API / static / redirect / dead)
- [ ] Tech fingerprints noted (framework, CDN, WAF, auth)
- [ ] No host hammered; low concurrency used

## JavaScript bundle mining

- [ ] Bundles listed (katana / hakrawler / page source)
- [ ] Bundles fetched where possible; blocks recorded honestly
- [ ] `/api/` paths extracted
- [ ] GraphQL operations extracted (if any)
- [ ] Endpoint + parameter names collected
- [ ] Feature flags and internal hostnames noted

## API discovery

- [ ] Public API docs read (if any)
- [ ] Endpoints probed anonymously (200 / 401 / 403 recorded)
- [ ] Auth boundary mapped (anonymous vs authenticated)
- [ ] Same-origin vs separate API host noted
- [ ] Only my own IDs used in requests
- [ ] Response shapes noted per endpoint

## WAF behavior

- [ ] Flaky 200/403 pattern recorded (not reported as a single result)
- [ ] Blocked fetches recorded as blocked (not assumed empty)
- [ ] Geo-blocking noted (if observed)
- [ ] Rate limits respected; concurrency reduced after a limit
- [ ] Second-network verification done where results conflicted

## Recon log

- [ ] Log file written (date, scope, inventory, API map, bundles, WAF notes)
- [ ] Open questions listed
- [ ] Log saved with the engagement's other notes
