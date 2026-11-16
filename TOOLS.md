# Tools

Only tools verified installed and used in this workflow. Each entry names
the tool, what it does, and where to get it.

## Enumeration

| Tool | What it does | Source |
| --- | --- | --- |
| sublist3r | Subdomain enumeration from public sources | https://github.com/aboul3la/Sublist3r |
| waybackurls | Historic URLs from the Wayback Machine | https://github.com/tomnomnom/waybackurls |
| gauplus | Historic URLs from multiple archives | https://github.com/bp0lr/gauplus |

## Crawling and probing

| Tool | What it does | Source |
| --- | --- | --- |
| katana | Web crawler: routes, parameters, JavaScript files | https://github.com/projectdiscovery/katana |
| hakrawler | Fast crawler for endpoints and JavaScript files | https://github.com/hakluke/hakrawler |
| httpx | Probe hosts: status, title, tech fingerprint | https://github.com/projectdiscovery/httpx |
| subpipe | Subdomain takeover checks and pipeline helpers | Installed locally — verify the upstream URL before linking it |

## Scanning (use gently, in scope only)

| Tool | What it does | Source |
| --- | --- | --- |
| nuclei | Template-based scanning (community templates) | https://github.com/projectdiscovery/nuclei |
| dalfox | Parameter analysis and XSS scanning | https://github.com/hahwul/dalfox |

## Notes

- **DNS can lie.** Local resolvers in sandboxed environments sometimes
  return synthetic answers. For DNS conclusions, use a trusted public
  resolver (for example, Cloudflare DNS over HTTPS) and say which one
  you used.
- **nuclei templates are powerful and destructive if misused.** Targeted
  templates, low concurrency, in scope only. Never a full template set
  at speed against production.
- **A 403 is data.** Behind a WAF, identical requests alternate between
  200 and 403. Record the pattern; do not report one side of it.
- **Keep a version note.** Record which tool version produced each
  output — a finding reproduced with "latest" is hard to re-check.
