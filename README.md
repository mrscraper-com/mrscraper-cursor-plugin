# MrScraper for Cursor

MrScraper connects [Cursor](https://cursor.com) to a hosted MCP server for
fetching public web pages, managed structured extraction, Google discovery,
saved scraper reruns, stored results, and account usage. The plugin also
includes four focused skills that help the agent choose the right workflow and
preserve raw page content.

[Grok Bot](https://docs.x.ai/grok-bot/overview) installs plugins from the
Cursor Marketplace, so the same plugin works there too.

## What this plugin adds

- The hosted Streamable HTTP endpoint at `https://mcp.mrscraper.com/mcp`.
- OAuth 2.1 browser sign-in through Cursor's MCP client; no API key to paste
  and no credential stored in this repository.
- A fetch-first workflow that keeps raw page responses available for analysis,
  verification, and follow-up transformations.
- Managed extraction, site mapping, Google SERP discovery, saved reruns, and
  stored-result tools when those capabilities are useful.

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
copy. MrScraper grants `scrape:read` (`fetch`, `serp`, `results`, `result`),
`scrape:write` (`scrape`, `rerun`), and `account:read` (`status`). Never paste
OAuth tokens or API keys into chat.

## Try it

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

The connection exposes these MCP tools:

| Tool | Purpose |
| --- | --- |
| `fetch` | Retrieve and preserve a known page's raw response. |
| `scrape` | Run managed structured extraction or bounded site mapping. |
| `serp` | Discover public pages through Google. |
| `rerun` | Reuse a saved AI or manual scraper configuration. |
| `results` | Browse and filter stored result records. |
| `result` | Retrieve one stored result or poll an asynchronous run. |
| `status` | Inspect subscription usage and request outcomes. |

The skills appear in Cursor's **Agent Decides** list, and you can invoke one
directly in chat:

| Skill | Use it for |
| --- | --- |
| `/mrscraper` | Connection, authentication, routing, saved scrapers, stored results, and account usage. |
| `/mrscraper-fetch` | Raw content from a known public URL; the default first step. |
| `/mrscraper-scrape` | Managed structured extraction or bounded URL discovery within a site. |
| `/mrscraper-serp` | Google discovery when no target URL is known. |

## Fetch-first routing

When a public URL is already known, the skills direct the agent to fetch it
first and treat the raw response as the source of truth. The agent can read,
summarize, compare, or derive structured output locally without losing details
to an early extraction prompt.

This preference can still be faster for large same-layout sets. For roughly
100 known pages, the agent can safely fetch pages concurrently, retain every
raw response, and apply one reusable local extractor instead of requesting 100
separate backend-LLM extractions. Use `scrape` when managed extraction is
explicitly requested or has a clear benefit after the page structure and
desired schema are understood.

## Data and permissions

The plugin sends MCP tool inputs, including target URLs and extraction
instructions, to MrScraper's hosted service. Page responses and tool results
are then available to the agent for the requested task. Managed general and
listing extraction sends page content and the extraction prompt to a backend
language model and saves a reusable scraper configuration; reruns create new
stored results. Use it only with public or otherwise authorized content, and
follow the target site's requirements.

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
