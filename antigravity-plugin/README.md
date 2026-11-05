# Faxbeep for Antigravity

Connect Antigravity to the hosted Faxbeep MCP server. No account, API key,
local server or build step is required.

## Install

Clone the public repository:

```sh
git clone https://github.com/faxbeep/faxbeep-mcp.git
```

In an Antigravity session, install the plugin from the local folder, using its
absolute path:

```text
/plugin install /absolute/path/to/faxbeep-mcp/antigravity-plugin
```

Use `/plugin list` to check the installation and `/mcp` to inspect the
Faxbeep connection. The server provides three read-only tools:
`get_test_numbers`, `list_test_faxes` and `get_test_fax`.

## Use

Ask your assistant for a test fax number, send a test fax or a scan-to-email
test, then ask whether it arrived. Every test that Faxbeep receives is public
on faxbeep.com for 30 days, so do not send a private document.

## Package details

- `plugin.json`: plugin name and description.
- `mcp_config.json`: the hosted endpoint, using Antigravity's `serverUrl` field.
- Endpoint: `https://faxbeep.com/mcp` (Streamable HTTP, no authentication).
- License: [MIT](../LICENSE), for the public repository contents.

These instructions install the package from a local folder. A marketplace
listing is not confirmed.

## Documentation

- [Faxbeep MCP server reference](https://faxbeep.mintlify.app/developers/mcp)
- [Overview](https://faxbeep.com/test-fax-mcp)
- [Google's plugin format and installation guide](https://antigravity.google/docs/plugins)
- [Google's MCP configuration reference](https://antigravity.google/docs/mcp)
