---
name: ms-compliance
description: "MANDATORY before any login-gated scrape. When the user provides username/password, cookies, session tokens, or asks to scrape while logged in, warn them about legal risk and get acknowledgment before calling MrScraper MCP tools. Applies to Cursor, Claude Code, CLI, and SDK clients."
compatibility: Requires MrScraper MCP or API access.
metadata:
  author: MrScraper
---

# Authenticated scraping — legal warning (mandatory)

Use this skill **before** any MrScraper MCP, CLI, or SDK call when the user intends to scrape **while logged in** or supplies **their own** credentials, including:

- Username and password
- Cookies or `Cookie` headers (e.g. `session_cookie` on SERP tools)
- Session tokens, auth headers, or exported browser sessions
- Manual scrapers/workflows built for login-gated pages in the dashboard

## Step 1: Stop and warn the user

Do **not** call MrScraper tools yet. Show the user this warning (you may rephrase slightly, but keep every point):

---

**Warning — scraping with login or your own session**

If you scrape while logged in (for example using your username and password, or cookies and session tokens you provide), you may be violating the target site's terms of service and applicable law. **You could be sued** or face other legal claims from the site operator or other parties.

MrScraper provides scraping infrastructure only. **You are solely responsible** for your scraping activity, for obtaining any required permissions, and for compliance with laws and site policies.

**This legal and compliance risk is yours, not MrScraper's.** MrScraper does not assume liability for how you choose to scrape authenticated or login-gated content.

Only proceed if you understand and accept that risk.

---

## Step 2: Require explicit acknowledgment

Ask the user to confirm in clear terms, for example:

> I understand the risks and accept that I am solely responsible; MrScraper is not liable.

If they decline, refuse, or do not answer: **do not** pass credentials, cookies, or login-related parameters to any tool. Do not suggest workarounds to bypass this step.

## Step 3: After acknowledgment only

You may proceed with the appropriate skill (`ms-fetch-html`, `ms-serp`, `ms-ai-scraper`, `ms-manual`, etc.).

- Never log or repeat credentials in chat after the scrape.
- Prefer the minimum session data needed.
- Remind the user that terms of service and robots rules still apply.

## When this skill does NOT apply

Public pages with **no** user-supplied login or session data, and **no** intent to access account-only content, do not require this warning—though general scraping compliance (rate limits, site terms) still applies.

## Connected clients

This applies to any agent using MrScraper through:

- **Cursor** (this plugin + hosted MCP)
- **Claude Code / Claude Desktop** (MCP connector)
- **CLI or scripts** that wrap the MrScraper API
- **SDK** integrations you generate (`ms-code`)

The agent must deliver the warning; MrScraper tools will not block the call—the user and agent are responsible for informed consent.
