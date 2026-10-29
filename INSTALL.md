# Install THRW MCP and its planning skill

This is the installation procedure for an agent acting on a user's installation request. Install for the current client in **user scope**, preserving existing MCP settings, skills, connections, and execution permissions. Read the relevant client guide before making changes.

## 1. Identify the client and existing installation

Determine whether the user is running Codex, Claude Code, or another MCP client. Ask only when the available environment cannot establish the client or a material configuration conflict.

Inspect only the relevant THRW installation state. Do not display full configuration files, environment variables, tokens, cookies, OAuth callback URLs, or credential stores. Any necessary backup stays local and private, outside this repository.

Check for:

- A THRW plugin already providing the MCP connection and skill.
- A direct connection to `https://api.thrw.cc/mcp`, including under another name.
- A standalone `thrw-plan-and-organize` skill in any active user skill root.
- An existing `thrw` name that points at a different service.

Reuse an equivalent installation. Do not combine plugin and standalone installations of the same connection/skill. Do not overwrite conflicting connections or locally modified skills, delete credentials, unlink accounts, or change permissions to force installation. Explain conflicts and ask which installation to retain when needed.

## 2. Select one installation path

- **Codex:** follow [docs/codex.md](docs/codex.md). Use direct MCP plus the standalone skill for the chat-assisted path. If a suitable THRW plugin is already installed, use it instead. Native marketplace installation is an alternative when supported by the installed client.
- **Claude Code:** follow [docs/claude-code.md](docs/claude-code.md). Prefer the marketplace plugin, which includes both components.
- **Other clients:** follow [docs/generic-mcp.md](docs/generic-mcp.md). Report unsupported skill installation rather than claiming MCP registration also installed the skill.

Use this repository's selected Git ref consistently for the instructions and skill/package files. A user-selected release tag takes precedence over the default branch. For a fresh installation from an existing checkout, use that checkout's files. Keep support files inside the skill folder together. Do not execute unreviewed remote shell scripts.

## 3. Authenticate

The endpoint is `https://api.thrw.cc/mcp`; the intended name is `thrw`. Let the client discover the OAuth endpoints and register the client. No bundled or invented client ID/secret is needed. Request the permissions described in the relevant guide and honor the user's grant choices. Open the client's normal authentication flow and let the user sign in and consent.

Do not ask the user to paste tokens or secrets into chat or this repository. If browser interaction is needed, explain that step and report authentication as pending until the client confirms it.

## 4. Verify the two components separately

1. Confirm the effective connection resolves to the intended endpoint and that authentication succeeded.
2. Confirm THRW tools are available. Use a minimal read-only THRW request when authorized by the installation request; report availability without echoing personal planning records.
3. Confirm the skill is discovered and its installed content matches the selected source. If refresh, a new turn, or restart is required, say exactly what remains to be checked.
4. Confirm no duplicate active THRW connection or duplicate skill was introduced.

Do not create, change, or complete actual todos just to verify installation. Behavioral checks involving writes need a separate test request and disposable data.

## 5. Report the actual result

Report the client, user scope, installation path, source/ref or package version, and separate MCP/authentication/skill results. Distinguish complete, failed, and pending steps. Never infer automatic skill selection from file installation, or completion of authentication from an opened browser page.

After installing or updating MCP settings, a plugin, or the standalone skill, explicitly recommend saving current work and starting a fresh session so the client can load the new setup. For a desktop app, recommend fully quitting and reopening it; for a CLI, recommend exiting the current session and starting a new one. A supported reload may be sufficient, and a restart is a recommendation rather than a universal requirement. Do not close the app or end the user's session automatically. Ask the user to confirm THRW tools and the skill are available in the new session, and keep any checks that could not yet be performed marked as pending.

If an operation fails or is declined, preserve the existing setup, explain the incomplete step, and stop that operation. Do not blindly retry or bypass an approval. Follow the client's normal refresh and update procedures; never disable security settings as a troubleshooting shortcut.
