# Installing into a game repo

Interactive Claude Code only. No SDK, no `claude -p`, no headless mode, no cron, no GitHub Actions (see [[README]]).

1. Copy `agents/*.md` → `<game-repo>/.claude/agents/`
2. Copy `commands/*.md` → `<game-repo>/.claude/commands/`
3. Merge the `deny` rules from `settings.json` into `<game-repo>/.claude/settings.json`.
4. In the cards and commands, replace `<GAME>` with the game's folder name under `games/`.
5. Start Claude from the game repo:
   `claude --add-dir ~/Documents/vaults/roblox-brain`

Then use `/train <agent> <n>`, `/train <agent> holdout`, and `/end-session`.

Notes:
- The subagent files are thin wrappers. The rules live in the vault cards, so don't copy rules into them.
- Deny rules block Claude's Edit/Write tools. They do **not** stop a Bash command from writing files. CLAUDE.md forbids that, and humans should review `git diff evals/` in the vault before committing. TODO(verify): consider also denying Bash patterns that touch `evals/`.
- Subagent `tools:` lists now name MCP tools, assuming the servers are registered as `Roblox_Studio` and `blender`. Check the real names with `/mcp`. TODO(verify)

## MCP setup (docs checked 2026-11-16, unconfirmed)
- **Roblox Studio MCP (built into Studio).** The old `Roblox/studio-rust-mcp-server` was archived Apr 2026. In Studio: Assistant → ⋯ → Manage MCP Servers → *Enable Studio as MCP server* → Quick connect → Claude Code. Manual (macOS): `claude mcp add --transport stdio Roblox_Studio -- /Applications/RobloxStudio.app/Contents/MacOS/StudioMCP`. Every tool takes a `studio_id`; call `list_roblox_studios` first. `execute_luau` also needs `datamodel_type` (Edit/Client/Server) and returns the script's **return value**; `print` goes only to `get_console_output`. Right after start the proxy lists no studios for a few seconds, so retry. Studio 0.747 exposes 36 tools, not the 30 in the docs (extra: `open_cloud_invoke`, `generate_scene`, `generate_texture`, `segment_mesh`, `auto_setup_avatar`, skill tools) ([docs](https://create.roblox.com/docs/studio/mcp)). TODO(verify)
- **Blender MCP (community, `ahujasid/blender-mcp`).** Install the addon in Blender, open Blender first, then `claude mcp add blender uvx blender-mcp`. The package name has varied across releases, so check the README ([repo](https://github.com/ahujasid/blender-mcp)). Main tool: `execute_blender_code` (arbitrary Python in Blender). TODO(verify)
- Studio MCP has `multi_edit`, which edits scripts inside Studio and so bypasses Rojo. Keep it off script-writing agents so files on disk stay the source of truth.
