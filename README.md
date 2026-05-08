# Cursor plugin template

Build and publish Cursor Marketplace plugins from a single repository.

This bundle ships one plugin:

- **mrscraper**: hosted MrScraper MCP for rendered HTML, AI scrapers, job reruns, and results APIs

## MrScraper plugin

The `plugins/mrscraper/` plugin registers the **hosted MrScraper MCP server** so Cursor agents can call scraping tools from chat. The default connection uses the remote endpoint (no local scraper runtime required).

| Area | What you get |
|------|----------------|
| Raw page HTML | `fetch_html` — stealth, rendering, geo |
| Structured extraction | `create_scraper` — natural-language instructions; listing vs map-style crawls |
| Re-run jobs | `rerun_scraper`, `bulk_rerun_scraper`, `rerun_manual_scraper` |
| Results | `get_all_results`, `get_result_by_id` |

**Skill** — guidance the model uses to pick tools, handle tokens, and avoid unsafe or wasteful scraping:

- `mrscraper` — authentication, tool selection, keeping HTML out of huge context payloads, crawl limits, and respectful use of targets

### Quick setup

1. Create an API token in the [MrScraper app](https://app.mrscraper.com).
2. Install the plugin from the Marketplace (the bundle includes `plugins/mrscraper/mcp.json` with the hosted URL). To configure the server manually in Cursor, add:

```json
{
  "mcpServers": {
    "mrscraper": {
      "url": "https://mcp.mrscraper.com/mcp"
    }
  }
}
```

3. When tools run, pass your **token** in the tool arguments unless your environment injects auth another way.

More detail: [`plugins/mrscraper/README.md`](plugins/mrscraper/README.md) and [`plugins/mrscraper/skills/mrscraper/SKILL.md`](plugins/mrscraper/skills/mrscraper/SKILL.md).
