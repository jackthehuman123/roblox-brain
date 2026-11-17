---
description: Run the training loop for one agent. Usage /train <agent> <n|holdout>
argument-hint: <agent> <n|holdout>
---
Agent: $0 · Count or set: $1 (default 5 train tasks if empty)

Read ~/Documents/vaults/roblox-brain/pipeline/loop.md and follow it exactly. It is the single source of truth. Key rules:
- Do at most the requested number of tasks, then stop. Never loop unbounded.
- Each task: read the task file's `check:` line yourself and give the subagent the prompt **plus** that JSON, so it can self-check with `/Applications/Blender.app/Contents/MacOS/Blender -b --factory-startup -P harness/check_fbx.py -- <fbx> '<check JSON>'`. Never give it the task file path or any other evals/ content. Then delegate the work to the `$0` subagent, then **you** run the harness from Bash and paste its output verbatim into a run note at ~/Documents/vaults/roblox-brain/runs/YYYY-MM/. Never self-grade.
- TEST place only. Never production. DataStores mocked.
- Never edit ~/Documents/vaults/roblox-brain/evals/**.
- If the usage limit gets close: stop cleanly, write games/<GAME>/next.md, and tell me.
- At the end, write agents/$0/candidate.md (for train) or the holdout comparison (for holdout), then summarise the scores for me.
