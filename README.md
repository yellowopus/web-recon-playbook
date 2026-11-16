# Web Recon Playbook

A methodology for mapping a web target's attack surface — from public
data first, then careful live probing. Built from real recon work on
e-commerce, bounty-platform, and DeFi targets.

This is a **methodology** repo. It contains no target data: no domains,
no IP addresses, no credentials, no findings. Apply it to targets you
own or are authorized to test.

## The phases

1. **Scope** — read the program page twice before touching anything.
2. **Enumerate** — subdomains and hosts from public sources.
3. **Probe** — which hosts are actually live, and what they serve.
4. **Mine** — JavaScript bundles, API docs, and client-side routes.
5. **Map** — the API surface: endpoints, parameters, auth boundaries.
6. **Note** — everything goes in the recon log, with evidence.

## Contents

| File | What it is |
| --- | --- |
| [METHODOLOGY.md](METHODOLOGY.md) | Each phase in detail, including WAF behavior |
| [CHECKLIST.md](CHECKLIST.md) | Copy-paste checklists per phase |
| [TOOLS.md](TOOLS.md) | The verified tool inventory |

## Hard rules

- **Only authorized targets, in scope only.** If the program page says
  "web only", do not touch the API. If it says "API only", do not touch
  the marketing site.
- **Passive first.** Certificate transparency, DNS, archives, and search
  engines before any live request.
- **Read-only probing.** A probe asks "are you there and what do you
  serve?" — it does not change state.
- **Stop on a block.** A 403, a CAPTCHA, or a rate limit is the target
  telling you to stop. Do not route around it.
- **Log everything.** A recon note without a source and a timestamp is
  not evidence.

## License

MIT — see [LICENSE](LICENSE).
