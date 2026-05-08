# MrScraper — Cursor marketplace bundle

This repository is a **Cursor Marketplace**–ready bundle that ships the **MrScraper** plugin. The plugin registers a **hosted Model Context Protocol (MCP)** server so agents in Cursor can use MrScraper’s scraping and extraction tools without running a local scraper stack.

**MCP endpoint:** `https://mcp.mrscraper.com/mcp` (defined in `plugins/mrscraper/mcp.json`).

## What the plugin does

MrScraper exposes tools for web scraping workflows in chat: rendered HTML, AI-driven scrapers, job reruns, and results APIs. For setup (API token, usage notes), see [`plugins/mrscraper/README.md`](plugins/mrscraper/README.md).

## Repository layout

| Path | Purpose |
|------|---------|
| [`plugins/mrscraper/`](plugins/mrscraper/) | Plugin: `mcp.json`, manifest, logo, bundled skill |
| [`plugins/mrscraper/.cursor-plugin/plugin.json`](plugins/mrscraper/.cursor-plugin/plugin.json) | Plugin manifest (`displayName`, `description`, `author`, `logo`, …) |
| [`.cursor-plugin/marketplace.json`](.cursor-plugin/marketplace.json) | Marketplace bundle metadata and plugin list |
| [`scripts/validate-template.mjs`](scripts/validate-template.mjs) | Validates manifests, paths, and component frontmatter |
| [`docs/add-a-plugin.md`](docs/add-a-plugin.md) | How to add another plugin to this bundle |

