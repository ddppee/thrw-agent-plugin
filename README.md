# THRW Agent Plugin

THRW MCP integration and one planning skill for Codex and Claude Code. Find relevant planning context, organize confirmed todos and schedules, and track work on matching todos.

- **Codex:** [installation and updates](docs/codex.md).
- **Claude Code:** [marketplace installation and updates](docs/claude-code.md).
- **Other MCP clients:** [connection settings](docs/generic-mcp.md). Skill support depends on the client.

## Install with your agent

Send this prompt to Codex or Claude Code:

```text
Read https://github.com/ddppee/thrw-agent-plugin/blob/main/INSTALL.md.
Install THRW MCP and its official planning skill for the current client,
in user scope, and help me authenticate. Preserve existing MCP settings
and other skills. Reuse an existing matching THRW connection instead
of registering another one. Verify the connection and skill separately.
```

The agent follows the [installation procedure](INSTALL.md). Authentication can require browser interaction. Installation, OAuth access, and approval of individual writes are separate steps. This GitHub distribution is not an official directory listing.

After setup or an update, save your work and start a fresh session. For a desktop app, fully quit and reopen it; for a CLI, exit and start a new session. This is recommended to load the new setup, although a supported reload may be enough. Then check that THRW tools and the planning skill are available.

## What the skill does

- Treat THRW/throw commands and contextual localized pronunciation variants as requests to organize supplied context and apply supported planning changes, not only create new todos. English command forms are case-insensitive.
- Search existing work and reuse matching todos, groups, and lists.
- Structure rough input without forcing every hierarchy level; preserve relevant context in descriptions and children. Audit each affected todo's saved fields, including schedule, deadline, and importance.
- Save confirmed actions and explicitly requested changes. Do not save tentative ideas or unaccepted suggestions.
- Recognize existing todos that clearly match the work, even without a THRW mention.
- For substantive work, append missing progress stages and check them when finished:
  - `■□□ Design·Planning`
  - `□■□ Execution·Implementation`
  - `□□■ Verification·Testing`
- Preserve existing descriptions and unrelated subtasks. Reuse saved stages on resumption; pending design approval or failed required verification is not completion.
- Report actual saved outcomes, including failures or declined writes.

The filled square identifies a stage; its checkbox indicates completion. After verification, the skill reviews the parent's full requirements and current children. When all work is verified complete and no child remains open, it completes the parent without an extra status request, subject to user instructions and host approval. Checked stages alone are not sufficient. The [skill source](skills/thrw-plan-and-organize/SKILL.md) describes the full behavior. Implicit skill selection varies by host; explicit invocation is available in supported clients.

## Connection and data

- Endpoint: `https://api.thrw.cc/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth with discovery and Dynamic Client Registration
- MCP name: `thrw`

Use your own THRW account. No service credentials, access tokens, client secrets, hooks, local executables, or background processes are bundled. Tool calls send the selected arguments to THRW; the plugin does not require uploading your repository. Keep account data and authentication artifacts out of support reports.

The package version is in [VERSION](VERSION). MCP server releases and installed skill updates are separate. See [CHANGELOG.md](CHANGELOG.md).

## Support and license

[THRW](https://thrw.cc) · [Support](https://thrw.cc/support) · [Privacy](https://thrw.cc/privacy) · [Terms](https://thrw.cc/terms)

Publisher: DDPPEE. Public support contact: ddppee@ddppee.com.

This distribution is [MIT licensed](LICENSE). The license covers the distributed package, not the THRW server or entitlement to the hosted service.
