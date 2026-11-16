# Inbox: research results that need a human
from: agent (interactive session) · 2026-11-16

Agents can't edit these, so they're here for you to decide:
- [[evals/assets/baselines]] `<CAP>`: current Roblox spec says **20,000 triangles per mesh**. Pin it once you've checked [[roblox/gotchas]].
- [[evals/assets/baselines]] "Export scale correct": the check script should test for **FBX Unit Scale** export (Roblox docs, 2026), not the old 0.01 scale. See [[pipeline/assets]].
- [[evals/README]] harness: Open Cloud Luau Execution can reach **real DataStores**. The harness must inject mocks, not just hope they're mocked. Starting point: Roblox/place-ci-cd-demo scripts (see [[pipeline/prior-art]]).
- [[studio]] toolchain row "Roblox Studio MCP": now built into Studio (server name `Roblox_Studio`). The old rust MCP repo was archived Apr 2026.
