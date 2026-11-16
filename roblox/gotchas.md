# Roblox gotchas
Versions: Roblox engine <VERSION> · Blender <VERSION> · Moon Animator 2 <VERSION>
Last verified: <DATE>

Each entry is `TODO(verify)` until a human confirms it against current docs or our own testing. Then replace it with `verified <DATE>`.

- Use `task.wait()`, `task.spawn()`, and `task.delay()`, not the legacy `wait()`, `spawn()`, and `delay()`. TODO(verify)
- Legacy BodyMovers (BodyVelocity, BodyGyro, BodyPosition, …) are deprecated. Use constraints (LinearVelocity, AlignOrientation, AlignPosition, …). TODO(verify)
- DataStore read-modify-write: use `UpdateAsync`, never `GetAsync` + `SetAsync`, because the latter loses writes when they race. TODO(verify)
- `MarketplaceService.ProcessReceipt` must be idempotent. Record the PurchaseId and only return `PurchaseGranted` after the grant is saved. TODO(verify)
- Mesh triangle cap: some sources say 20k, older posts say 10k. **Verify and pin one number here:** <CAP>. TODO(verify)
- Blender FBX export: scale 0.01 so that 1 m = 1 stud. TODO(verify) (see [[pipeline/assets]])
- StreamingEnabled reportedly breaks Moon Animator cutscene playback (rigs/parts not streamed in). TODO(verify) (see [[pipeline/cutscenes]])
