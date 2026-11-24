# MrScraper for Cursor

MrScraper connects [Cursor](https://cursor.com) to a hosted MCP server for
retrieving public web pages as HTML, Markdown, or screenshots, web
search, and account usage. The plugin also includes three focused skills
that help the agent choose the right workflow and preserve raw page content.

[Grok Bot](https://docs.x.ai/grok-bot/overview) installs plugins from the
Cursor Marketplace, so the same plugin works there too.

## What this plugin adds

- The hosted Streamable HTTP endpoint at `https://mcp.mrscraper.com/mcp`.
- OAuth 2.1 browser sign-in through Cursor's MCP client; no API key to paste
  and no credential stored in this repository.
- A retrieve-first workflow that keeps raw page responses available for
  analysis, verification, and follow-up transformations.

## Requirements

- A current version of Cursor, or Grok Bot.
- A [MrScraper](https://app.mrscraper.com) account.
- Permission to access and process the target content.

## Install

### Cursor

Open **Customize** in the sidebar, search for **MrScraper**, select
**Install**, and choose a project or user scope. You can also browse the
[Cursor Marketplace](https://cursor.com/marketplace).

To install from this repository instead, for example before a release reaches
the Marketplace, copy the plugin folder into Cursor's local plugin directory:

```bash
git clone https://github.com/mrscraper-com/mrscraper-cursor-plugin.git
mkdir -p ~/.cursor/plugins/local
cp -R mrscraper-cursor-plugin/plugins/mrscraper ~/.cursor/plugins/local/mrscraper
```

Restart Cursor or run **Developer: Reload Window**. Cursor skips symlinks that
point outside `~/.cursor/plugins/local`, so copy the folder rather than linking
it. On Teams and Enterprise plans, local plugins load only if an admin allows
local plugin imports.

### Grok Bot

Select **Plugins** (or **Marketplace**) in the Grok Bot sidebar, search for
**MrScraper**, and choose **Add**.

## Sign in

After installation, open **Customize** and find the `mrscraper` MCP server.
When Cursor shows that it needs authentication, start the sign-in there;
Cursor opens MrScraper's consent page in your browser. Sign in, approve access,
and return to Cursor. In Grok Bot, choose **Authorize** when asked and finish
the same sign-in in your browser.

Cursor registers its own OAuth client with MrScraper, so there is no API key to
copy. MrScraper grants `scrape:read` (the six scraping and search tools) and
`account:read` (`status`). Never paste OAuth tokens or API keys into chat.

## Try it

```text
Fetch https://www.scrapethissite.com and summarize the page.
```

The connection exposes these MCP tools:

| Tool | Description |
| --- | --- |
| `status` | Return the raw account status API response without summarizing, redacting body fields, or adding calculated fields. |
| `scrapeHtml` | Retrieve the raw HTML of a page. Browser rendering and a screenshot are optional. |
| `scrapeMarkdown` | Retrieve a page as Markdown. Browser rendering is optional. |
| `getScreenshot` | Capture a base64 PNG screenshot of the full page, the top viewport, or a custom viewport size. Browser rendering is always enabled. |
| `scrapeBrand` | Extract a website's colors, typography, logos, and social links as JSON. |
| `scrapeJson` | Extract structured JSON from a page using a natural-language prompt. Append Json Schema: and a JSON schema to shape the output. |
| `webSearch` | Search the web and return ranked results with titles, URLs, descriptions, and sources. |

The skills appear in Cursor's **Agent Decides** list, and you can invoke one
directly in chat:

| Skill | Use it for |
| --- | --- |
| `/mrscraper` | Connection, authentication, routing, and account usage. |
| `/mrscraper-fetch` | Page content from a known public URL; the default first step. |
| `/mrscraper-serp` | Web search when no target URL is known. |

## Retrieve-first routing

When a public URL is already known, the skills direct the agent to retrieve it
with `scrapeMarkdown` or `scrapeHtml` first and treat the raw response as the
source of truth. The agent can read, summarize, compare, or derive structured
output locally without losing details.

For roughly 100 known pages that share a layout, the agent can retrieve pages
concurrently, retain every raw response, and apply one reusable local
extractor.

## Data and permissions

The plugin sends MCP tool inputs, including target URLs and search queries, to
MrScraper's hosted service. Page responses and tool results are then available
to the agent for the requested task. Use it only with public or otherwise
authorized content, and follow the target site's requirements.

Network endpoints and credentials:

- `https://mcp.mrscraper.com/mcp`: the hosted MCP server, reached over HTTPS.
  Tool inputs are sent here.
- `https://api.app.mrscraper.com`: the OAuth 2.1 authorization server
  (authorization, token, and dynamic client registration endpoints),
  advertised in the server's protected resource metadata at
  `https://mcp.mrscraper.com/.well-known/oauth-protected-resource/mcp`.
- `https://app.mrscraper.com`: the MrScraper sign-in and consent pages opened
  in your browser.
- Credentials: a MrScraper account and the OAuth grant that Cursor stores for
  the connection. In Grok Bot, OAuth tokens stay on Cursor's connector backend
  and Bots invoke tools without receiving them. The plugin reads no
  environment variables or files and ships no hooks, rules, commands, scripts,
  or executables.

Review MrScraper's [MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server),
[Privacy Policy](https://mrscraper.com/privacy-policy),
[Terms of Use](https://mrscraper.com/terms-of-use), and
[Acceptable Use Policy](https://mrscraper.com/acceptable-use-policy) before use.

## Update or remove

Manage the plugin from **Customize**: Marketplace updates appear there after
Cursor reviews each new version, and the same page uninstalls the plugin. For
a local copy, replace or delete `~/.cursor/plugins/local/mrscraper` and reload
the window.

If you installed the CLI-oriented MrScraper skills with
`npx -y @mrscraper/cli@latest init --agent cursor`, both skill sets use the
same names. Keep only the set that matches how you connect: this plugin for
MCP, or the CLI skills for the `mrscraper` command.

## Support and security

- Product help: [MrScraper MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server)
- Bugs and feature requests: [GitHub Issues](https://github.com/mrscraper-com/mrscraper-cursor-plugin/issues)
- Account help: [support@mrscraper.com](mailto:support@mrscraper.com)
- Security reports: see [SECURITY.md](SECURITY.md)

## Development

The repository is a Cursor multi-plugin repository with one plugin:

```text
.cursor-plugin/marketplace.json
plugins/mrscraper/
├── .cursor-plugin/plugin.json
├── assets/logo.svg
├── mcp.json
└── skills/
```

Validate the manifests, paths, and skill frontmatter before a release:

```bash
node scripts/validate-template.mjs
```

Then test the plugin from `~/.cursor/plugins/local` as described in
[Install](#install). Bump `version` in both manifests for every release and
record user-visible changes in [CHANGELOG.md](CHANGELOG.md). Cursor reviews
every Marketplace update before it ships.

## License

[MIT](LICENSE)
