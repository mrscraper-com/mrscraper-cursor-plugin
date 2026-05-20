---
name: ms-serp
description: "Google Search / SERP via MrScraper sync API. DEFAULT for web search tasks. If the user supplies cookies or wants logged-in Google results, run ms-compliance first. NOT for generic HTML (ms-fetch-html) or structured extraction (ms-ai-scraper)."
compatibility: Requires MrScraper MCP. Pass sync bearer token as access_token.
allowed-tools: mcp(mrscraper:google_serp_sync)
metadata:
  author: MrScraper
---

# Google SERP

Search Google for: $ARGUMENTS

## Step 0: Login or cookies?

If the user provides **`session_cookie`**, other cookies, or wants results from a **logged-in** Google account → follow **`ms-compliance`** first. Warn about lawsuit/legal risk and user (not MrScraper) liability; get explicit acknowledgment before calling tools.

## Step 1: Build the search URL

Use a full Google search URL, e.g. `https://www.google.com/search?q=iphone+17`.

## Step 2: Call the tool

```
google_serp_sync({
  access_token: "<sync bearer token, atk_...>",
  url: "https://www.google.com/search?q=<encoded query>",
  raw: false
})
```

| Parameter | Notes |
|-----------|--------|
| `access_token` | Sync API token from [app.mrscraper.com](https://app.mrscraper.com); optional `Bearer ` prefix is stripped |
| `raw` | `false` for parsed organic results when supported; `true` for raw output |
| `session_cookie` | Only after **ms-compliance** acknowledgment — optional `Cookie` header value |

Calls may take **over a minute**. Summarize results; do not dump full `data` into context.

## Step 3: Cite sources

Cite every fact with `[Title](url)` from tool results only. End with a **Sources** list.

## If MCP is unavailable

Stop. Ask the user to enable the MrScraper plugin and retry—do not search from memory.
