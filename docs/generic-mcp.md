# Other MCP clients

Use the client's own MCP registration UI or configuration format:

- Name: `thrw`
- URL: `https://api.thrw.cc/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth discovery and Dynamic Client Registration
- Recommended complete scopes: `openid email thrw:read thrw:write`

The client must support this transport and authentication flow. No API key, client secret, or access token is supplied in this repository. Let the client store credentials through its supported secure mechanism, not in public configuration or chat.

`thrw:read` enables reads. `thrw:write` enables reads and writes under the service's scope policy. `openid` and `email` are identity permissions; `email` requires `openid`. Configure the grant supported by the client and chosen by the user. Do not claim a client supports scope selection unless verified in that client.

The JSON formats in `plugins/codex/mcp.json` and `plugins/claude-code/.mcp.json` are client-specific examples. Do not paste one into an unrelated client's configuration without adapting it to that client's documented format.

## Skills are separate

An MCP connection exposes tools and context. It does not automatically install the planning skill. If the client supports Agent Skills, install the complete folder at `skills/thrw-plan-and-organize` according to that client's instructions. If it does not, report that only MCP was connected; do not label a tool description or pasted prompt as a persistent installed skill.

Use [INSTALL.md](../INSTALL.md) for duplicate prevention and separate MCP/skill verification. Each client controls its tool approvals and credential storage. This distribution does not guarantee per-call approval UI, implicit skill selection, or support for all clients.
