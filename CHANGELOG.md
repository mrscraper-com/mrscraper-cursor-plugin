# Changelog

All notable changes to the MrScraper Cursor plugin are documented here. The
project follows [Semantic Versioning](https://semver.org/).

## 0.3.2 - 2026-10-29

- Reworded search as web search in the plugin and
  marketplace descriptions, keywords, READMEs, and skills.
  The `webSearch` tool is unchanged. The skills now differ from the MrScraper
  Claude plugin 0.2.2 only in this wording.

## 0.3.1 - 2026-10-22

- Updated the `mrscraper` skill and the README for the hosted server's three
  scopes: `scraperAPI` needs `scrape:write`, `webSearch` needs `scrape:read`,
  and `status` needs `account:read`. If `scraperAPI` returns 403
  `insufficient_scope`, sign in again so Cursor requests `scrape:write`.
  Skills are identical to the MrScraper Claude plugin 0.2.2.

## 0.3.0 - 2026-10-14

- Updated the skills for the hosted MCP server's new tools: `scraperAPI`
  (pages as HTML, Markdown, or screenshots), `webSearch` (Google), and `status`
  (account usage). The `fetch`, `scrape`, `serp`, `rerun`, `results`, and
  `result` tools no longer exist.
- Removed the `mrscraper-scrape` skill. Skills are identical to the MrScraper
  Claude plugin 0.2.0.
- Updated the manifests, keywords, and READMEs.

## 0.2.0 - 2026-10-09

- Updated for the current hosted MrScraper MCP server (0.1.3), whose tools are
  `fetch`, `scrape`, `serp`, `rerun`, `results`, `result`, and `status`.
  Authentication now uses OAuth 2.1 browser sign-in instead of API tokens in
  tool arguments.
- Replaced the eight `ms-*` skills, which called tools the server no longer
  provides and asked for API tokens in tool arguments, with the `mrscraper`,
  `mrscraper-fetch`, `mrscraper-scrape`, and `mrscraper-serp` skills, unchanged
  from the MrScraper Claude plugin 0.1.4. The legal warning before
  login-protected scraping is now part of the `mrscraper` skill's manual-rerun
  flow.
- Updated both manifests (description, homepage, repository, keywords, and
  support contact).
- Added the MIT `LICENSE`, `SECURITY.md`, and this changelog; rewrote both
  READMEs; removed the template guide `docs/add-a-plugin.md`.

## 0.1.0 - 2026-05-08

- Initial plugin: hosted MCP URL and the `ms-*` skills.
