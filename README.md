# Faxbeep MCP server

[![Faxbeep MCP connector - tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.faxbeep/faxbeep/badges/score.svg)](https://glama.ai/mcp/connectors/com.faxbeep/faxbeep)

Test a fax machine, a fax service or a scan-to-email setup from your AI agent. Faxbeep gives free public test fax numbers and test email addresses. Send a test to one, then ask your agent whether it arrived.

```
https://faxbeep.com/mcp
```

Remote server, Streamable HTTP, no authentication. Read-only.

> Every test that Faxbeep receives is public on faxbeep.com for 30 days. Do not send a private document.

## Add it to your chat app

- **Claude:** Customize > Connectors > Add custom connector. Name `Faxbeep`, URL `https://faxbeep.com/mcp`, no sign in.
- **ChatGPT:** turn on developer mode in the Apps settings, then create an app with the URL `https://faxbeep.com/mcp` and no authentication.

Menus change often. The [docs](https://faxbeep.mintlify.app/developers/mcp) have the current steps.

## Add it to a coding agent

```sh
# Claude Code
claude mcp add --transport http faxbeep https://faxbeep.com/mcp

# Codex
codex mcp add faxbeep --url https://faxbeep.com/mcp
```

Cursor: put this in `~/.cursor/mcp.json`, or in `.cursor/mcp.json` in a project:

```json
{
  "mcpServers": {
    "faxbeep": {
      "url": "https://faxbeep.com/mcp"
    }
  }
}
```

## Add it to Gemini CLI

Install the extension from this repository:

```sh
gemini extensions install https://github.com/faxbeep/faxbeep-mcp --ref main
```

Use `/mcp` to check the connection and see the three tools. The `--ref main` is needed: without it, the installer takes a release, and a release holds only the ChatGPT package.

## Add it to Antigravity

The [Antigravity plugin package](antigravity-plugin/) connects to the hosted server. See its [installation instructions](antigravity-plugin/README.md).

## Tools

| Tool               | What it does                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `get_test_numbers` | The test fax numbers (US, UK, Australia), the test email addresses, the limits, and `now`, the server time   |
| `list_test_faxes`  | The test faxes received since a time, newest first. Filters: sender, page count, limit                       |
| `get_test_fax`     | One test fax, by its slug (`fax_1a2b3c4d`) or by the URL of its page on faxbeep.com                           |

Each result gives the sender (masked as on faxbeep.com), the time received, the page count, and links to the PDF, the thumbnail and the page of the fax.

A match by time, sender or page count narrows the candidates. It does not prove that a fax is yours, because other people send tests at the same time. Check the page.

## Example

> I want to test the fax machine at the office. Give me a number, and tell me when my fax arrives.

The agent calls `get_test_numbers`, gives you a number, and notes the server time. You send the fax. The agent calls `list_test_faxes` with that time and shows you the page of each new fax, so you can find yours.

To try the connection without sending anything, ask for the fax `fax_example`. It is a fixed sample, not a real fax.

## Faxbeep does not send faxes

Faxbeep only receives. To send a test without a fax machine, use a fax sending service, for example [PayPerFax](https://payperfax.com/fax-mcp/), which has its own MCP server.

## Documentation

- [Faxbeep MCP](https://faxbeep.com/test-fax-mcp): overview and example prompts
- [MCP server reference](https://faxbeep.mintlify.app/developers/mcp): tools, fields, errors, polling rules, limits
- [Faxbeep API](https://faxbeep.mintlify.app/developers/overview): the same data over plain HTTP
- [Privacy](https://faxbeep.com/privacy)

## About this repository

This repository documents the hosted server. The server code is not open source. [`server.json`](server.json) is the entry in the [official MCP registry](https://registry.modelcontextprotocol.io/) as `com.faxbeep/faxbeep`. Its `version` counts the versions of that registry entry. It is not the version that the server reports.

The files in this public repository are available under the [MIT License](LICENSE). That license does not cover the hosted server, which is not included here.
