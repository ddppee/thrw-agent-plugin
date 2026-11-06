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

## Complete list inventories

MCP implementation 1.2.0 adds a page mode to `list_tasks`. Once that server release is deployed and the client has refreshed its tool definitions:

1. Use `list_task_group_hierarchy` to obtain the desired `taskGroupId`.
2. Call `list_tasks({ taskGroupId: "<returned-list-id>", page: 0 })` without `preset`.
3. Read `tasks` and call the same list with the returned `nextPage` until it is null. For all lists, repeat for each list ID.

Each page returns `taskGroupId`, `page`, `pageSize: 50`, `totalCount`, `nextPage`, and up to 50 non-deleted root todos, including completed ones, in list order. `totalCount` counts roots only; empty and out-of-range pages return an empty array and `nextPage: null`. Unavailable lists return errors rather than masquerading as empty lists. Concurrent changes are not frozen across calls.

Each item includes `id`, `title`, `kind`, `parentTaskId: null`, `isStarred`, and `subTaskCount`; only `todo_item` includes `isDone`. Documents omit inactive completion fields. Optional `scheduledStartLocal`, `scheduledEndLocal`, and `dueLocal` retain the user's time zone. `completedSubTaskCount` is omitted when zero. `subTaskCount` covers all visible active direct children, including documents; `completedSubTaskCount` counts completed `todo_item` children only. These are not an all-todo completion ratio; children do not occupy page slots. Titles over 128 Unicode codepoints become the first 127 plus `…`. Use `read_content` with `entity: "task"` and the returned `id` for the full title, description, and children.

Existing `list_tasks({ preset: "open" })` and `list_tasks({ preset: "recents" })` calls retain their existing bounds. Open selects todo roots; recents includes both kinds. Do not combine `preset` with page arguments. A client holding older schemas may keep using presets but reject or fail to understand page calls. Refresh `tools/list` through the host's supported refresh/reconnect flow; a new conversation or restart may be needed. A version bump alone does not invalidate every cache. Do not delete credentials or repeat OAuth by default. Updating a plugin package or standalone skill is a separate client action; refreshing MCP metadata does not replace installed skills. This source does not assert deployment, publication, or runtime verification in every host.

## Skills are separate

An MCP connection exposes tools and context. It does not automatically install the planning skill. If the client supports Agent Skills, install the complete folder at `skills/thrw-plan-and-organize` according to that client's instructions. If it does not, report that only MCP was connected; do not label a tool description or pasted prompt as a persistent installed skill.

Use [INSTALL.md](../INSTALL.md) for duplicate prevention and separate MCP/skill verification. Each client controls its tool approvals and credential storage. This distribution does not guarantee per-call approval UI, implicit skill selection, or support for all clients.

## Task kinds

Tasks and subtasks use independent `kind: "todo_item" | "document"`. Creation defaults to `todo_item`; omit kind for ordinary work or explicitly select either kind. Use `document` for reference content without progress tracking. Use existing `create_tasks` and `update_tasks`; tool names, entity names and IDs remain unchanged. Titles-only child creation still defaults to todo; read the parent for child IDs before updating a child's kind.

Kind and stored status are independent. A kind-only update preserves the previous completion state, and switching back to todo exposes that state again. All AI/MCP task reads include kind; documents omit `isDone`/`status` instead of returning null or false. Parent and child kinds do not propagate. General pages, recents and search include both kinds; open work selects todos. This read projection is not a full sync row and must not be converted into a patch that clears or defaults missing status. Description content supports Markdown for either kind.

These server changes are included in server-v1.4.0; this contract guidance is included in package 1.2.0. Refresh MCP tool metadata through the host's supported flow. Updating an installed plugin or standalone skill is a separate action; neither update implies the other or requires resetting OAuth credentials.
