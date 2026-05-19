---
name: ms-batch
description: "Bulk rerun one scraper over many URLs. If URLs are login-gated or the scraper uses user session/login, run ms-compliance first. Use bulk_rerun_ai_scraper or bulk_rerun_manual_scraper."
compatibility: Requires MrScraper MCP with API token.
allowed-tools: mcp(mrscraper:bulk_rerun_ai_scraper), mcp(mrscraper:bulk_rerun_manual_scraper)
metadata:
  author: MrScraper
---

# Batch Rerun

Process multiple URLs for: $ARGUMENTS

## Step 0: Authenticated scraping?

If any URL or the scraper config involves **login**, **user cookies**, or **account-only** pages → follow **`ms-compliance`** before batch tools. One acknowledgment covers the batch only if the user clearly understands scope; otherwise warn again.

## Step 1: Pick tool

| Scraper | Tool |
|---------|------|
| AI (`create_ai_scraper`) | `bulk_rerun_ai_scraper` |
| Manual (dashboard) | `bulk_rerun_manual_scraper` |

## Step 2: Call

```
bulk_rerun_ai_scraper({
  token: "<MRSCRAPER_API_TOKEN>",
  scraper_id: "<id>",
  urls: ["<url1>", "<url2>"]
})
```

## Step 3: Collect results

Use `ms-results` when runs complete. Label per-URL outcomes for the user.

## If MCP is unavailable

Stop. Enable MrScraper MCP and retry.
