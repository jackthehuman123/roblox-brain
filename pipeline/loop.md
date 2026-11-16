# Training loop
Versions: Claude Code <VERSION> · Roblox Studio MCP <VERSION> · Blender <VERSION>
Last verified: <DATE>

Runs **only** inside an interactive Claude Code session that a human started (no SDK, no `claude -p`, no headless mode, no cron, no Actions). Started with `/train <agent> <n>`.

1. **Load** the agent's card.md + lessons.md (through its subagent).
2. **Pick** a task from `evals/tasks/train/` that has no run note yet. Do it in Studio through the Roblox Studio MCP (or in Blender for assets).
3. **Score** it by running the harness from Bash: headless tests through Open Cloud Luau Execution against a separate **TEST place** (never production), with DataStores mocked; Blender checks through `blender -b -P`. Paste the harness output verbatim into a run note ([[runs/_template]]). **Never self-grade.**
4. **After n tasks** (or earlier if the usage limit hits; stop cleanly and write `games/<GAME>/next.md`): read this batch's runs and write `agents/<agent>/candidate.md` (the proposed edit to card/lessons).
5. **Next session:** `/train <agent> holdout` runs the candidate on `evals/tasks/holdout/`. If it beats the current card with no regressions, mark it **PROMOTABLE** in candidate.md.
6. **A human** promotes candidate → card.md and bumps the card version. Stable cards are what get handed over to the software factory.
7. Default n = 5. Never loop unbounded. Stop after **K = <K>** batches with no improvement and tell the human. TODO: pick K.

## Notes
- Training works best on machine-scored work (tests, perf, lint, asset checks).
- Visual and cutscene quality stays human-judged.
- DataStore/purchase baselines are only as good as the tests a human wrote and understands.
- Check `/usage` before long batches.
