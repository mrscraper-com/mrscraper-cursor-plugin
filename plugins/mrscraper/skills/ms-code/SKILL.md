---
name: ms-code
description: "Generate code integrating MrScraper REST API (Python, Node, curl). Include ms-compliance warning in generated apps when users pass credentials or cookies. NOT for live MCP calls in chat."
metadata:
  author: MrScraper
---

# MrScraper Code Generation

Generate integration code for: $ARGUMENTS

## Step 0: Authenticated scraping in generated code

If the user's app will send **username/password**, **cookies**, or **session tokens** to scrape login-gated sites, embed this warning in README/comments and runtime docs:

> Scraping while logged in may violate site terms and laws. Users may face lawsuits or other legal claims. MrScraper provides infrastructure only; **the developer and end user bear all legal risk, not MrScraper.**

In CLI/SDK samples that accept `--cookie` or auth flags, print the warning before the first authenticated request unless `--i-accept-risk` (or similar) is passed.

## When to use

- Building scripts, pipelines, or apps against MrScraper APIs
- Not for one-off live scrapes in chat → use MCP skills

## Auth

| API | Auth |
|-----|------|
| Unblocker `api.mrscraper.com` | Query `token=` |
| Platform `api.app.mrscraper.com` | Header `x-api-token` |

Store `MRSCRAPER_API_TOKEN` in environment variables only.

## MCP (Cursor / Claude Code)

```json
{
  "mcpServers": {
    "mrscraper": {
      "url": "https://mcp.mrscraper.com/mcp"
    }
  }
}
```

Agents using this connector must follow **`ms-compliance`** before login-related tool parameters.

## Quick API examples

**Unblocker:** `GET https://api.mrscraper.com?token=...&url=...`

**AI scraper:** `POST https://api.app.mrscraper.com/api/v1/scrapers-ai` with JSON body and `x-api-token`.

**Results:** `GET https://api.app.mrscraper.com/api/v1/results?...`

Emit complete runnable code, `.env.example`, and error handling for 401/429.

## Output rules

1. Match language to request (default Python)
2. Never hardcode real tokens
3. Document agent types: `general`, `listing`, `map`
4. Include compliance note whenever auth/cookies are in scope
