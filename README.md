# MrScraper — Cursor plugin

Marketplace-ready Cursor plugin that registers the **hosted MrScraper MCP server** at `https://mcp.mscraper.com/mcp`.

## Contents

- `plugins/mrscraper/` — plugin manifest, `mcp.json`, logo, skill, and README
- `.cursor-plugin/marketplace.json` — marketplace metadata for submission

## Validate before submit

```bash
node scripts/validate-template.mjs
```

## Customize for submission

1. Update `.cursor-plugin/marketplace.json` → `owner` (name and email) to your legal publisher identity.
2. Update `plugins/mrscraper/.cursor-plugin/plugin.json` → `author` to match.
3. Confirm the MCP URL in `plugins/mrscraper/mcp.json` is correct for production.

## Submission

Follow Cursor’s current plugin submission process (see historical template guidance: valid manifests, logo path, validation passing, repository ready for Cursor team review).
