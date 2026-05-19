# MrScraper (Cursor plugin)

This plugin registers the **MrScraper** Model Context Protocol server so Cursor can call scraping tools from chat.

## What you get

- **Hosted MCP**: connects to `https://mcp.mrscraper.com/mcp` (no local Python install required).
- **Tools**: fetch rendered HTML, Google SERP sync, create AI scrapers, rerun and bulk rerun, rerun manual scrapers, and read results (see MCP tool descriptions in Cursor).
- **Skills** (one workflow per folder):
  - **`ms-compliance`** — mandatory legal warning before login/cookie/credential scraping (Claude Code, Cursor, CLI, SDK)
  - `ms-serp`, `ms-fetch-html`, `ms-ai-scraper`, `ms-batch`, `ms-manual`, `ms-results`, `ms-code`

Agents must run **`ms-compliance`** when users supply username/password, cookies, session tokens, or want logged-in scraping. The user is warned they may be sued and bear all legal risk—not MrScraper.

## Setup

1. Install the plugin from this marketplace/repository in Cursor.
2. Obtain an API token from [app.mrscraper.com](https://app.mrscraper.com).
3. When the agent runs a tool, provide the token in the tool arguments (`token` for most tools; `access_token` for `serp`, which uses the sync API bearer token).

## Notes

- Large HTML responses can exceed context limits; prefer writing HTML to a file or extracting specific sections before analysis.
- Crawl depth and page limits materially affect cost and runtime; keep map crawls conservative unless you intend a broad crawl.

## License

MIT (see repository root if a root `LICENSE` is present).
