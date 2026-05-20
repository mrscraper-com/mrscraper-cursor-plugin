---
name: ms-fetch-html
description: "Fetch rendered HTML via MrScraper unblocker (stealth, geo, anti-bot). If the user needs login-gated HTML or will pass cookies/credentials, run ms-compliance first. NOT for SERP (ms-serp) or NL extraction (ms-ai-scraper)."
compatibility: Requires MrScraper MCP with API token.
allowed-tools: mcp(mrscraper:fetch_html)
metadata:
  author: MrScraper
---

# Fetch HTML (Unblocker)

Fetch HTML for: $ARGUMENTS

## Step 0: Login-gated pages?

If the user needs content **behind login**, or will supply cookies/credentials/session data (now or via API extensions) → follow **`ms-compliance`** first. Warn that logged-in scraping may lead to **lawsuits** and that **risk is the user's, not MrScraper's**; get acknowledgment before scraping.

## Step 1: Call the tool

```
fetch_html({
  token: "<MRSCRAPER_API_TOKEN>",
  url: "<target url>",
  timeout: 120,
  geo_code: "US",
  block_resources: false
})
```

Token: [app.mrscraper.com](https://app.mrscraper.com) → User Profile → API Tokens.

## Step 2: Handle large HTML

Do not paste full HTML into chat. Save to a file or extract only needed sections.

## Routing

| Need | Skill |
|------|--------|
| Google search | `ms-serp` |
| Structured fields | `ms-ai-scraper` |
| Dashboard manual workflow | `ms-manual` |

## If MCP is unavailable

Stop. Do not curl the URL directly—enable MrScraper MCP and retry.
