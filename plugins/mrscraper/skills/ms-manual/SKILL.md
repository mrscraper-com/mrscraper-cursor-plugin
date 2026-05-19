---
name: ms-manual
description: "Rerun dashboard manual scrapers (selectors/workflows). Often used for login flows—run ms-compliance first when workflows use user login or session. NOT for AI scrapers (ms-ai-scraper)."
compatibility: Requires MrScraper MCP, API token, and an existing manual scraper in the dashboard.
allowed-tools: mcp(mrscraper:rerun_manual_scraper)
metadata:
  author: MrScraper
---

# Manual Scraper Rerun

Rerun manual scraper for: $ARGUMENTS

## Step 0: Login workflows (common)

Manual scrapers often include **Input**, **Click**, or steps that assume a **logged-in** session. If the user built or runs a login workflow, or supplies session/credentials → follow **`ms-compliance`** first. Warn about **legal action including lawsuits**; confirm **user bears all risk, not MrScraper**.

## Prerequisites

1. [app.mrscraper.com](https://app.mrscraper.com) → **Scraper** → **New Manual Scraper +**
2. Save workflow; copy **`scraperId`**

Do not use for AI scrapers (`ms-ai-scraper`).

## Step 1: Single URL

```
rerun_manual_scraper({
  token: "<MRSCRAPER_API_TOKEN>",
  scraper_id: "<dashboard id>",
  url: "<target url>"
})
```

## Step 2: Many URLs

`ms-batch` → `bulk_rerun_manual_scraper`.

## Step 3: Results

`ms-results` for full rows when needed.

## If MCP is unavailable

Stop. Enable plugin and provide `token` and `scraper_id`.
