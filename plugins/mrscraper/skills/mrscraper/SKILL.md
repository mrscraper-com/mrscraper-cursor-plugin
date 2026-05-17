---
name: mrscraper
description: Use MrScraper MCP tools for rendered HTML, Google SERP sync, AI scrapers, reruns, bulk jobs, manual scrapers, and paginated results.
---

# MrScraper MCP

This plugin connects Cursor to the hosted **MrScraper** MCP server.

## Authentication

Most tools require a MrScraper API **token** (from [MrScraper app](https://app.mrscraper.com)). Pass `token` on each tool call unless your deployment injects auth another way.

**`serp`** uses the sync API bearer token: pass `access_token` (same `atk_...` token; a leading `Bearer ` prefix is stripped if present).

## Tool selection

- **`serp`**: Google Search results for a full search URL (e.g. `https://www.google.com/search?q=iphone+17`). Set `raw: true` for raw API output; `false` for parsed organic results when supported. Optional `session_cookie` if your deployment requires a `Cookie` header. Calls can take a minute or more—avoid dumping full `data` into context; summarize or save externally.
- **`fetch_html`**: Raw HTML for a single URL (stealth/render/geo). Avoid pulling huge HTML into the model; save to disk or extract slices first.
- **`create_scraper`**: Default for structured extraction from natural-language instructions. Use `agent: "listing"` when the URL is clearly a listing page; use `agent: "map"` when crawling a site (respect depth/page limits).
- **`rerun_scraper`**: Reuse an AI scraper configuration on a new URL (or crawl params for map agents).
- **`bulk_rerun_scraper`**: Same scraper, many URLs in one batch.
- **`rerun_manual_scraper`**: Only for scrapers built in the dashboard with manual selectors, not AI scrapers.
- **`get_all_results` / `get_result_by_id`**: List or fetch completed results (pagination and filters as supported by the API).

## Safety

Scraping may be rate-limited or disallowed by target sites and laws. Prefer robots/terms compliance and reasonable concurrency.
