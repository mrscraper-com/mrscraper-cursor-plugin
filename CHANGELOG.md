# Changelog

All notable changes to the MrScraper Cursor plugin are documented here. The
project follows [Semantic Versioning](https://semver.org/).

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
