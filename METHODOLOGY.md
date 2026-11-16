# Methodology

## Phase 0 — Scope

Read the program page in full, twice. Note:

- In-scope assets (domains, apps, APIs, mobile apps).
- Out-of-scope items (usually: third-party services, other users' data,
  social engineering, DDoS, physical).
- The program's focus (for example: API authorization, checkout/payment
  flows, or smart contracts).
- Testing rules (local fork only? no automated scanners? rate limits?).
- Reward table and what the program actually pays for.

If scope is ambiguous, ask the program. Never probe first and ask later.

## Phase 1 — Subdomain enumeration

Goal: the fullest possible list of hosts, from public sources only.

- **Certificate transparency logs** — certificates issued for the
  domain and its subdomains.
- **DNS records** — A, AAAA, CNAME, MX, TXT, NS. A CNAME pointing at a
  dead service is worth noting (dangling CNAME), but verify it is
  actually dangling before claiming anything.
- **Search engines and archives** — indexed subdomains and historic
  URLs.
- **Tools:** sublist3r for enumeration; waybackurls and gauplus for
  historic URLs.

Record the source of every subdomain. A subdomain from one source is a
lead; the same subdomain from three sources is a fact.

## Phase 2 — Live-host probing

Goal: which hosts answer, and what they serve.

- Probe with httpx: status code, title, content length, tech fingerprint.
- Record status codes as observed. The same host can answer 200 and 403
  on alternating requests behind a WAF — that flakiness is itself a
  finding about the environment, not a bug.
- Classify hosts: live app, API, static asset host, redirect, dead.
- Do not hammer. Low concurrency, one pass, then analyze before a
  second pass.

## Phase 3 — JavaScript bundle mining

Goal: endpoints and logic the UI does not show.

- List every JavaScript bundle the app loads (crawl with katana or
  hakrawler, or read the page source).
- Fetch the bundles and search for: `/api/` paths, GraphQL operations,
  endpoint names, parameter names, feature flags, and internal hostnames.
- Reconstruct the API's route table from the bundle: which endpoints
  exist, which need auth, which take an ID in the path.
- Note what you **cannot** fetch: some bundles are blocked from some
  networks (WAF rules, geo-blocking). Record the block honestly instead
  of assuming the content.

## Phase 4 — API discovery

Goal: the API surface, mapped.

- Read the public API documentation first, if any exists.
- Probe documented endpoints anonymously: which are 200, which are 401,
  which are 403? The anonymous/authorized boundary is the map.
- For each endpoint, note: method, path, parameters, auth requirement,
  and what it returns for your own account.
- Same-origin vs cross-origin matters: an app that only calls
  same-origin `/api/*` paths behaves differently from one that calls a
  separate API host. Note which one you observe.
- Never call an endpoint with another user's identifier. Test with your
  own IDs only.

## Phase 5 — WAF and bot-management behavior

Some targets sit behind a WAF or bot manager (for example, Akamai Bot
Manager). Expect:

- **Flaky results.** Identical requests alternating between 200 and 403.
  Record both. Do not report the 200 as "the site is open" or the 403
  as "the site is down" — report the pattern.
- **Blocked tooling.** A bundle or page that loads in a browser may
  refuse a scripted fetch. That is a property of the environment, not a
  vulnerability.
- **Geo-blocking.** Some apps refuse whole regions (for example, an app
  that redirects to a "restricted" page from certain networks). Note it
  and move on — do not route around it.
- **Rate limits.** If you hit one, stop, wait, and reduce concurrency.
  Never parallelize your way around a limit.

When in doubt, verify from a second network or a real browser session —
and record which network produced which result.

## Phase 6 — Recon log

Every recon run produces a log file with:

- Date, target (as named by the program), and scope version.
- Subdomain inventory with sources.
- Live-host table (host, status, title, tech).
- API map (endpoint, method, auth, observed response).
- JS bundle inventory (URL, fetchable or blocked, notable strings).
- WAF behavior observed.
- Open questions (what is still unknown).

The log is the deliverable of recon. A recon phase without a log did not
happen.
