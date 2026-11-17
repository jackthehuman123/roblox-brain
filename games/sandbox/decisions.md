# Decisions: sandbox
One line per decision, with the why. Agents append only after a human confirms.
Format: `- <DATE> · <decision> — why: <reason> · confirmed by: <human>`

- 2026-11-16 · Training uses a separate sandbox repo `~/Documents/roblox-sandbox`, not a real game — why: keep harness experiments away from game code · confirmed by: repo owner (chat)
- 2026-11-16 · Assets reach Studio via Open Cloud Assets API upload (FBX → Model) + Studio MCP insert — why: scriptable and scoreable, unlike the manual 3D Importer · confirmed by: repo owner (chat)
- 2026-11-16 · One-time exception: an agent wrote the first asset-builder task bank + baselines in `evals/`. Humans review the diff; the rule is back in force after this — why: bootstrap · confirmed by: repo owner (chat)
- 2026-11-16 · Agents may self-run the Blender check (`check_fbx.py` with the task's `check:` JSON passed inline by /train). They never get the task file path. A self-check is never a score — why: the agent fixes faults before handoff; criteria are already in the prompt · confirmed by: repo owner (chat)
