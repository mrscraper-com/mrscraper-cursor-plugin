# MrScraper

This Cursor plugin connects to the hosted MrScraper MCP server and adds focused
skills for page retrieval as HTML, Markdown, or screenshots, web search,
and account usage. Grok Bot can install it from the Cursor Marketplace as well.

When a public URL is known, scraperAPI is the normal first content-acquisition
step. It preserves the page response so the agent can inspect every available
detail, answer follow-up questions, and apply reusable local extraction logic,
including one local batch extractor for many same-layout pages.

The plugin connects to `https://mcp.mrscraper.com/mcp` and authenticates
through OAuth 2.1 browser sign-in. A MrScraper account is required. Do not
paste OAuth tokens or API keys into chat.

See the repository [README](../../README.md) for installation, usage, data
handling, update, and support instructions.
