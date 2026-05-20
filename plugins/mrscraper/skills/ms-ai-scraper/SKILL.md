---
name: ms-ai-scraper
description: "DEFAULT for structured extraction from natural language (general, listing, map agents). If scraping login-gated or account-only sites, run ms-compliance first. NOT for raw HTML (ms-fetch-html) or dashboard manual scrapers (ms-manual)."
compatibility: Requires MrScraper MCP with API token.
allowed-tools: mcp(mrscraper:create_ai_scraper), mcp(mrscraper:rerun_ai_scraper)
metadata:
  author: MrScraper
---

# AI Scraper

Extract structured data for: $ARGUMENTS

## Step 0: Login or account-only content?

If the target requires **being logged in**, or the user mentions credentials, cookies, or private/account data → follow **`ms-compliance`** first. Do not start `create_ai_scraper` until the user acknowledges **personal legal risk** (including possible **lawsuits**) and that **MrScraper is not liable**.

## Step 1: Create vs rerun

| Situation | Tool |
|-----------|------|
| New extraction spec | `create_ai_scraper` |
| Reuse `scraper_id` on new URL | `rerun_ai_scraper` |
| Many URLs | `ms-batch` → `bulk_rerun_ai_scraper` |

## Step 2: Agent choice

| Agent | Use when |
|-------|----------|
| `general` | Default — most single pages |
| `listing` | Product/job listing index pages |
| `map` | Site crawl from a root URL |

### Create (general / listing)

```
create_ai_scraper({
  token: "<MRSCRAPER_API_TOKEN>",
  url: "<target url>",
  message: "<plain-language fields to extract>",
  agent: "general"
})
```

### Create (map)

```
create_ai_scraper({
  token: "<MRSCRAPER_API_TOKEN>",
  url: "<site root>",
  message: "",
  agent: "map",
  max_depth: 2,
  max_pages: 50,
  limit: 1000
})
```

Keep `max_depth` ≤ 3. Use `include_patterns` / `exclude_patterns` with `||` between regexes.

### Rerun

```
rerun_ai_scraper({
  token: "<MRSCRAPER_API_TOKEN>",
  scraper_id: "<id from create>",
  url: "<new url>"
})
```

## Step 3: Results

Use `ms-results` if status is pending or you need history. Never echo API tokens.

## If MCP is unavailable

Stop. Enable the plugin and provide `token`.
