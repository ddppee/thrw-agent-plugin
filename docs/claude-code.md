# Claude Code

## Install

Follow [INSTALL.md](../INSTALL.md) to check for existing THRW connections and skills first. Use your own THRW account and preserve other installations.

From a shell with Claude Code installed:

```sh
claude plugin marketplace add ddppee/thrw-agent-plugin
claude plugin install thrw@thrw-tools --scope user
```

The Claude catalog at `.claude-plugin/marketplace.json` selects `plugins/claude-code`. Within a Claude Code session, `/plugin marketplace add ddppee/thrw-agent-plugin` and `/plugin` provide the interactive path. Choose user scope when prompted. Installation from this GitHub marketplace does not require an official directory listing.

Open `/mcp`, select the installed THRW connection, and complete OAuth if needed. Use the server name actually shown by the host; plugin namespaces may be added. Avoid creating a second direct connection to the same endpoint. Do not remove a pre-existing direct installation until its replacement works and the user has chosen the migration.

The package pins `openid email thrw:read thrw:write` using Claude Code's `oauth.scopes`. This is the recommended complete grant, not four mandatory scopes. Supported subsets follow the service's permission rules; `email` requires `openid`. Browser consent is not approval of every later write.

## Verify and use

After installation or an update, save your work and start a fresh Claude Code session; if using the desktop app, fully quit and reopen it. This is recommended to load the new setup, although a supported reload may be sufficient. Do not end the user's session automatically. Confirm the plugin, MCP connection, and skill in the fresh session; keep checks pending when they cannot yet be performed.

```sh
claude plugin list
claude plugin details thrw
```

Verify the enabled plugin's component inventory includes its MCP connection and `thrw-plan-and-organize` skill. Confirm authentication and a read-only tool separately. Invoke the skill explicitly as `/thrw:thrw-plan-and-organize`; implicit selection depends on the host and request.

Command syntax was checked against local help in Claude Code 2.1.208. Package validation and CLI help do not establish successful OAuth, runtime loading, or automatic skill selection. Claude Desktop Chat, Cowork, and other hosted surfaces need their own supported installation path; these Code commands do not claim compatibility with them.

## Update or remove

```sh
claude plugin marketplace update thrw-tools
claude plugin update thrw@thrw-tools --scope user
```

Restart or reload as directed by your client, then verify the installed version. MCP reconnection alone does not update bundled skills.

To uninstall this plugin when requested:

```sh
claude plugin uninstall thrw@thrw-tools --scope user
```

Keep other plugins, connections, and standalone skills intact. Authentication failures are not a reason to reset all credentials or weaken execution approvals. Report declined or failed writes without claiming that data was saved.

Official references: [marketplaces](https://code.claude.com/docs/en/plugin-marketplaces), [plugin manifest](https://code.claude.com/docs/en/plugins-reference), [OAuth scopes](https://code.claude.com/docs/en/mcp#restrict-oauth-scopes).
