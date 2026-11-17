# Rules for agents working in this vault

## No API spend
Interactive Claude Code sessions only. Never suggest or use the Agent SDK, `claude -p`, headless mode, cron-driven Claude, or GitHub Actions. They bill a separate credit pool. Use subagents (`.claude/agents/`) and slash commands (`.claude/commands/`) only.

## Load only what your card lists
Read your `agents/<name>/card.md`, its `lessons.md`, and the files under **Loads**. Do not browse or search the rest of the vault.

## Ownership
- Humans only: `studio.md`, `games/*/spec.md`, `evals/**`, the **Never** section of every card, and promoting `candidate.md` → `card.md`.
- You may write: `runs/`, `agents/*/candidate.md`, `agents/*/lessons.md` (proposals), `games/*/next.md`, `games/*/decisions.md` (only after a human confirms), `handoffs/`, `inbox/`, and `refs/asset-design/` (asset-researcher only; asset-builder loads a pinned version via its card).
- **Never edit anything under `evals/`**, by any means (Edit, Write, Bash, or scripts). Changing a test or baseline to pass is the #1 failure mode. If a test looks wrong, write a note in `inbox/`.
- Agents propose, humans decide. Your writes are proposals until a human promotes them.

## Writing style
- Short. Templates, not essays. Store only what a model can't know or tends to get wrong.
- Never invent facts about our games, tools, or versions. Use `<PLACEHOLDER>` or `TODO(verify)`.
- Practices, gotchas, and baselines files start with `Versions:` and `Last verified:` lines.
- Use [[wikilinks]] between notes.
- Never self-grade. Scores are pasted verbatim from harness output.
- To hand work off, write a note in `handoffs/` from [[handoffs/_template]].

## Keep this file current (multi-machine)
This vault is used from more than one machine. Claude's memory is per-machine and does **not** travel. This file and git do.
- Before ending a session in which project state changed, update **Current state** below and commit. Do this with `/end-session` too.
- Put durable facts in the vault, not in Claude memory. Machine-specific facts go under **Machines**.
- On a new machine: `git pull`, read **Current state**, then check the Machines entry for this host (`hostname -s`) and add one if missing.

## Current state
Last updated: 2026-11-16
- Research drafts (all still `TODO(verify)`): [[roblox/gotchas]], [[pipeline/assets]], [[pipeline/cutscenes]], [[pipeline/prior-art]].
- **Training sandbox:** repo `~/Documents/roblox-sandbox` (local only, no remote yet), vault game `games/sandbox/`. Harness: `harness/score.sh <task> [train|holdout]` (Blender checks → Open Cloud upload → measure in Studio via MCP). Harness verified end to end 2026-11-16 with known-good fixtures: crate 4×4×4 → Studio 4×4×4 studs; signpost front → −Z. 3 test assets were uploaded and the place has a `HarnessImports` folder.
- **TEST place:** experience "Test place", universe `10777275246`, place `105044887830592` (user-owned, private). Also in the sandbox at `harness/test_place.json`. API key has luau-execution-sessions + universe-places write, scoped to it. Luau Execution verified 2026-11-16 (`harness/luau_exec.py`). The universe-places write (place upload) is not yet tested because it overwrites the published place.
- **Agent self-check:** asset-builder may run `harness/check_fbx.py` with inline `check:` JSON from /train (decision 2026-11-16). Scores still come only from `harness/score.sh`.
- **evals:** asset-builder task bank (train 001–005, holdout 101–102) + `evals/assets/baselines.md` were written by an agent under a one-time exception (see `games/sandbox/decisions.md`). Humans must review them. The rule is back in force.
- [[studio]] is still placeholders waiting on human answers. Server-scripter and cutscene-integrator have no tasks yet.
- Open for humans: `inbox/2026-11-16-research-for-humans.md`, `inbox/2026-11-16-install-smoke-test.md`.
- Next:
  1. Humans: review `evals/` (commit 6194512) and fill `games/sandbox/spec.md`.
  2. In the sandbox, run `claude --add-dir ~/Documents/vaults/roblox-brain`, then `/train asset-builder 5`. Needs Studio open with MCP enabled, plus `.env` (not in git; copy it by hand to other machines).
  3. Install Rojo/Wally/Selene/StyLua and uv.

## Machines
Paths in `integration/` assume the vault is at `~/Documents/vaults/roblox-brain`. Keep it there on every machine or update those files.

| Host | Blender | Roblox Studio | Claude Code | Studio MCP in Claude | Notes |
|---|---|---|---|---|---|
| Hungs-MacBook-Air (macOS) | 5.3.0 | 0.747.0 | 2.1.325 | via sandbox `.mcp.json`; `.env` set | harness passed 2026-11-16. No rojo/wally/selene/stylua/uv yet. Checked 2026-11-16 |
