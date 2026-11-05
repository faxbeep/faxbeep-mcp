# ChatGPT directory package

The package for the ChatGPT plugin directory. It connects the full Faxbeep server, `https://faxbeep.com/mcp`, with its three read-only tools. Faxbeep sells nothing, so the ChatGPT commerce rules do not apply.

## Files

- `plugin.json`: package identity, listing text, review test cases, publication notes.
- `mcp.json`: the one MCP server.
- `assets/logo.png`: 512 x 512, the Faxbeep logo.

## Review fixtures

The test cases use fixed answers that the server keeps for reviewers. A real fax is public for 30 days and then removed, so a test case built on it would fail when a reviewer returns. A real fax is also a real person's document.

| Input                                          | Answer                                                        |
| ---------------------------------------------- | ------------------------------------------------------------- |
| `get_test_fax` with `fax_example`              | A fixed sample fax: 1 page, sender `FAXBEEP-EXAMPLE`          |
| `get_test_fax` with its `view_url`             | The same sample fax                                           |
| `get_test_fax` with `fax_example_removed`      | The answer for a removed fax                                  |
| `list_test_faxes` with `from` `FAXBEEP-EXAMPLE` | A list with only `fax_example`, whatever `since` says         |

The server instructions and the `list_test_faxes` description name these samples, so they are not hidden behaviour.

## Before you submit

- [ ] Record the video walkthrough and add `demo_recording_url` to `review` in `plugin.json`.
- [ ] Check each test case against `https://faxbeep.com/mcp`.

## Build the ZIP

```sh
cd openai-plugin && zip -r ../faxbeep-openai-plugin.zip plugin.json mcp.json assets
```

Do not commit the ZIP. Attach it to a release. The Gemini CLI installer picks a release when one exists, which is why the Gemini install line in the main README uses `--ref main`.

## Submit

1. Platform > Plugins > "Upload new or existing plugin". Choose the verified Faxbeep identity.
2. Fix the metadata findings and upload again.
3. MCPs > Connect. Serve the challenge token as plain text at `https://faxbeep.com/.well-known/openai-apps-challenge` (a file in `public/.well-known/` of the core app, and a deploy). Wait for the tool scan.
4. Submit for review. In the reviewer notes:
   > Faxbeep gives free public test fax numbers and test email addresses. This app lets a user check, from ChatGPT, whether their test fax or scan-to-email test arrived. All three tools are read-only.
   >
   > Fixed sample answers for testing (they never expire): `get_test_fax` with `fax_example` (a 1-page sample fax), `get_test_fax` with `fax_example_removed` (the removed-fax answer), and `list_test_faxes` with `from` set to `FAXBEEP-EXAMPLE` (a list with only the sample). Real faxes are public for 30 days and then removed, so the test cases use these samples.
5. After approval, publish.

To update: upload a new ZIP to the same plugin; do not delete it. To change the MCP URL after you submit, you must contact OpenAI support. OpenAI scans the server daily, and a new tool waits for approval.
