# Rules for agents working in this vault

## No API spend
Interactive Claude Code sessions only. Never suggest or use the Agent SDK, `claude -p`, headless mode, cron-driven Claude, or GitHub Actions. They bill a separate credit pool. Use subagents (`.claude/agents/`) and slash commands (`.claude/commands/`) only.

## Load only what your card lists
Read your `agents/<name>/card.md`, its `lessons.md`, and the files under **Loads**. Do not browse or search the rest of the vault.

## Ownership
- Humans only: `studio.md`, `games/*/spec.md`, `evals/**`, the **Never** section of every card, and promoting `candidate.md` → `card.md`.
- You may write: `runs/`, `agents/*/candidate.md`, `agents/*/lessons.md` (proposals), `games/*/next.md`, `games/*/decisions.md` (only after a human confirms), `handoffs/`, `inbox/`.
- **Never edit anything under `evals/`**, by any means (Edit, Write, Bash, or scripts). Changing a test or baseline to pass is the #1 failure mode. If a test looks wrong, write a note in `inbox/`.
- Agents propose, humans decide. Your writes are proposals until a human promotes them.

## Writing style
- Short. Templates, not essays. Store only what a model can't know or tends to get wrong.
- Never invent facts about our games, tools, or versions. Use `<PLACEHOLDER>` or `TODO(verify)`.
- Practices, gotchas, and baselines files start with `Versions:` and `Last verified:` lines.
- Use [[wikilinks]] between notes.
- Never self-grade. Scores are pasted verbatim from harness output.
- To hand work off, write a note in `handoffs/` from [[handoffs/_template]].
