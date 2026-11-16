# roblox-brain

Knowledge for the AI agents that build our Roblox games, and for us.
It holds only what models can't know or tend to get wrong: our conventions, pinned versions, decisions, and gotchas we've hit. No tutorials, no copied docs.

**Core principle:** an agent knows exactly what its card tells it to load, and nothing else. Agents never read the whole vault.

## Hard constraint: no API spend
We do **not** use the Claude Agent SDK, `claude -p`, headless mode, cron-driven Claude, or GitHub Actions. They bill a separate credit pool.
Everything runs inside **interactive** Claude Code sessions that a human starts, on Pro subscription limits.
- "Agent" = a Claude Code subagent (`.claude/agents/*.md`) used in an interactive session.
- "Workflow" = a slash command (`.claude/commands/*.md`) typed by a human.
- Check `/usage` before long batches. If you hit a limit, stop cleanly and write `next.md`.

## Ownership
**Humans only:** [[studio]], `games/*/spec.md`, `evals/**` (baselines + task bank), the **Never** section of every agent card, and promoting `candidate.md` → `card.md`.

**Agents may write:** `runs/`, `agents/*/candidate.md`, `agents/*/lessons.md` (proposals), `games/*/next.md`, `games/*/decisions.md` (only after a human confirms the decision), `handoffs/`, `inbox/`.

- Agents propose, humans decide. Nothing an agent writes becomes a rule until a human promotes it.
- Agents must **never** edit anything under `evals/`. Changing a test or baseline to pass is the #1 failure mode.

## How agents load notes
Each agent has a card: `agents/<name>/card.md`. Its **Loads** section is the full list of what it reads, plus its own `lessons.md`. Nothing else.
Template: [[agents/_template]]. Agents: [[agents/server-scripter/card]], [[agents/asset-builder/card]], [[agents/cutscene-integrator/card]].

## Wiring into a game repo
See [[integration/claude-code/README]]. In short: copy the subagents and commands into `<game-repo>/.claude/`, add the evals deny rule, then start Claude with
`claude --add-dir ~/Documents/vaults/roblox-brain`.

## Training
[[pipeline/loop]]. Scores come from the harness (in the game repo), never from an agent's self-report. See [[evals/README]].

## Review rhythm
- **End of every session:** `/end-session`, then commit both repos.
- **Weekly:** sort `inbox/`, read new `lessons.md` proposals and `handoffs/`, and promote or reject PROMOTABLE candidates.
- **Monthly:** roll `runs/YYYY-MM/` up into a summary. Re-verify any note whose `Last verified:` is more than about 3 months old. TODO(verify): agree on a cadence.
