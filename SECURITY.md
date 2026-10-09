# Security Policy

Please report suspected vulnerabilities privately to
[support@mrscraper.com](mailto:support@mrscraper.com). Include the affected
component, reproduction steps, and potential impact. Do not open a public issue
for an unpatched vulnerability or include credentials, tokens, customer data,
or private target content in a report.

The plugin contains no MrScraper credentials, hooks, rules, commands, scripts,
or executables; `scripts/validate-template.mjs` is repository tooling and is not
part of the plugin. Authentication is handled by Cursor's OAuth 2.1 MCP
connection; in Grok Bot, OAuth tokens stay on Cursor's connector backend. If a
credential may have been exposed, revoke it through the relevant account or
client immediately and then contact support.
