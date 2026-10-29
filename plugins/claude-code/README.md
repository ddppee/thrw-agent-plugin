# THRW for Claude Code

This package bundles the THRW remote MCP connection and one planning skill. It uses OAuth discovery and the recommended `openid email thrw:read thrw:write` scopes. No credentials, hooks, or local executables are bundled.

Install from the THRW Tools GitHub marketplace using the [Claude Code guide](https://github.com/ddppee/thrw-agent-plugin/blob/main/docs/claude-code.md). Complete authentication through `/mcp` if required. Preserve existing connections and avoid duplicate standalone skill/MCP installations.

The skill can be invoked as `/thrw:thrw-plan-and-organize`. It organizes confirmed work and tracks design, implementation, and verification using progress subtasks while preserving existing content. Automatic selection depends on the host. OAuth consent is distinct from per-call write approval; honor the client's execution policy and report failed or declined writes accurately.

These instructions target Claude Code, not a claim of Claude Desktop Chat or Cowork compatibility. Installation and package validation do not prove authentication or runtime success. This GitHub package is separate from official directory submission.

The [MIT license](LICENSE) covers this package, not the THRW server or service access. [Privacy](https://thrw.cc/privacy) · [Terms](https://thrw.cc/terms) · [Support](https://thrw.cc/support).
