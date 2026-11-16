# Baselines: server-scripter
Versions: Jest-Lua <VERSION> · Rojo <VERSION> · Roblox engine <VERSION>
Last verified: <DATE>

| Metric | Target | Scored by |
|---|---|---|
| Unit tests pass (Jest-Lua) | 100% | harness script (Open Cloud Luau Execution on TEST place) |
| Remote handlers validate args | 100% | static check script |
| Server frame time in stress place | < <X> ms | Open Cloud Luau Execution task (stress place) |
| Holdout tasks solved | ≥ <N>/10 | harness script over `tasks/holdout/` |
| Diff size per task | < <N> lines | git (`git diff --stat`) |
