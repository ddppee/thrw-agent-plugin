# Codex

## Chat-assisted installation

Use the prompt in [README.md](../README.md) and follow [INSTALL.md](../INSTALL.md). The direct path installs two separate components: a user-scoped MCP connection and the standalone skill from `skills/thrw-plan-and-organize/`. Registering the URL alone does not install the skill.

After checking for existing equivalent connections, a client with the corresponding CLI commands can register and authenticate:

```sh
codex mcp add thrw --url https://api.thrw.cc/mcp
codex mcp login thrw --scopes openid,email,thrw:read,thrw:write
```

Run the add command only if the connection is absent. Registration may itself start authentication; run login only if authentication is still needed. Reuse the actual existing server name if it differs. Check the installed CLI's help before using options; older clients may expose another supported configuration flow.

For skills, use the built-in `$skill-installer` if available, pointing it at this repository and `skills/thrw-plan-and-organize`. Install into a recognized **user** skill root: current documentation uses `~/.agents/skills`, while the bundled installer can default to `$CODEX_HOME/skills` or `~/.codex/skills`. Inspect existing roots first and choose only one. Do not install into a project's skill directory for a user-scope request, or create duplicate copies across roots. Copy the entire skill folder, including `agents/openai.yaml`. Never overwrite a locally modified existing skill without resolving the conflict.

## Native plugin alternative

If no direct installation is active and the installed client supports Git-backed marketplaces:

```sh
codex plugin marketplace add ddppee/thrw-agent-plugin
```

Select **THRW Tools → THRW** in the supported desktop plugin UI and install. CLI versions whose `codex plugin --help` lists `add` also support:

```sh
codex plugin add thrw@thrw-tools
```

The Codex catalog at `.agents/plugins/marketplace.json` selects `plugins/codex`. Complete OAuth for the server identifier exposed by that installed plugin. Do not add a second direct MCP connection or standalone skill when the plugin already provides them.

These CLI forms were checked against local help in Codex CLI 0.163.0. This is syntax evidence, not an end-to-end installation or OAuth result. Check your version's help; the desktop UI is the fallback when CLI installation is unavailable.

The package retains OpenAI's documented per-server `extensions.com.openai` OAuth settings. The generic Agent Plugins 1.0 MCP JSON Schema currently rejects that extension, although the portable MCP core validates. Full generic-schema conformance and actual Codex interpretation of this configuration are not established; the direct MCP/standalone-skill path is separate from this package-format boundary. See the official packaging reference below rather than deleting authentication settings to silence a validator.

## Verify and use

After installation or an update, save your work and start a fresh Codex session; in the desktop app, fully quit and reopen the app. This is recommended to load updated MCP settings and skills; use a supported reload instead if it refreshes both. Do not close an active session automatically, and keep any discovery checks pending until they can be performed.

Check connection authentication, tool discovery, and skill discovery separately in the fresh session. Invoke the skill through the client's skill picker or `$thrw-plan-and-organize` where supported. Skill selection without an explicit mention depends on the host.

The recommended complete scope set is `openid email thrw:read thrw:write`. These are not all mandatory: supported subsets limit capabilities; `email` requires `openid`. A denied write needs the permission named in its error, not weaker execution approval settings. OAuth access and approval of individual writes are independent.

## Updates and removal

For a direct installation, update only the installed THRW skill folder from the chosen ref, preserving local edits unless the user chooses replacement. A server update does not update that folder. Keep the existing MCP registration when its endpoint and authentication are still valid.

For marketplace installs, refresh the configured source:

```sh
codex plugin marketplace upgrade thrw-tools
```

Then use the client's plugin update/reinstall flow and verify the installed version. Refreshing a marketplace alone does not prove the installed skill was replaced.

On a supported CLI, remove the plugin with `codex plugin remove thrw@thrw-tools`. For direct installations, remove only the identified THRW connection and skill when the user requests removal. Keep other MCP connections, skills, and credentials intact. Do not remove a shared marketplace if the user relies on other entries from it.

Official references: [plugin packaging and marketplaces](https://developers.openai.com/plugins/build/plugins), [skills](https://developers.openai.com/codex/skills).
