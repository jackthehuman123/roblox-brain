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
- TODO(verify): add the Roblox Studio MCP / Blender MCP tool names to each subagent's `tools:` list once the MCP servers are set up.
