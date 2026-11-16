# Roblox gotchas
Versions: Roblox engine <VERSION> · Blender <VERSION> · Moon Animator 2 <VERSION>
Last verified: <DATE>
Docs checked: 2026-11-16 by agent (not a human verification; sources inline)

Each entry is `TODO(verify)` until a human confirms it against current docs or our own testing. Then replace it with `verified <DATE>`.

## Scripting
- Use `task.wait()`, `task.spawn()`, and `task.delay()`, not the legacy `wait()`, `spawn()`, and `delay()`. Docs mark the legacy ones "superseded… should not be used for future work" ([globals](https://create.roblox.com/docs/reference/engine/globals/RobloxGlobals)). TODO(verify)
- Legacy BodyMovers (BodyVelocity, BodyGyro, BodyPosition, …) are deprecated. Use constraints (LinearVelocity, AlignOrientation, AlignPosition, …). Docs tag `BodyVelocity` Deprecated ([ref](https://create.roblox.com/docs/reference/engine/classes/BodyVelocity)). TODO(verify)
- `RemoteFunction:InvokeClient`: if the client never returns, the server "yields forever"; client errors and disconnects throw on the server. Use `RemoteEvent:FireClient` ([ref](https://create.roblox.com/docs/reference/engine/classes/RemoteFunction)). TODO(verify)

## Data and purchases
- DataStore read-modify-write: use `UpdateAsync`, never `GetAsync` + `SetAsync`. Docs: UpdateAsync "reads the current key value" and re-runs the callback if another server changed it. The callback may run **more than once**, so keep it side-effect free. Return `nil` to cancel ([ref](https://create.roblox.com/docs/reference/engine/classes/GlobalDataStore)). TODO(verify)
- Dev product receipts must be idempotent. Key the grant on `PurchaseId` with `UpdateAsync`. Report success only after the grant is saved. Otherwise return not-processed, and the receipt is redelivered (next opportunity or next join). TODO(verify)
- `MarketplaceService:BindReceiptHandler` is a newer alternative to `ProcessReceipt`. Bound handlers take precedence, and unmatched receipts fall through to `ProcessReceipt` ([ref](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService)). Pick one per game and log it in decisions.md. TODO(verify)

## Meshes / Blender
- Mesh triangle cap: **20,000 triangles per mesh** per the current spec page ([specs](https://create.roblox.com/docs/art/modeling/specifications)). The 10k figure is from older posts. Rigid/layered accessories are stricter (about 4k, check the avatar spec). TODO(verify) then pin.
- Blender FBX export: the old "scale 0.01" advice is **outdated**. Current docs say Apply Scalings = **FBX Unit Scale** with all other scales at 1.0. 0.01 is listed only as a fallback ([blender](https://create.roblox.com/docs/art/blender)). Settings live in [[pipeline/assets]]. TODO(verify)
- FBX textures import grey unless Path Mode = Copy + Embed Textures ([export reqs](https://create.roblox.com/docs/art/modeling/export-requirements)). TODO(verify)

## Streaming / cutscenes
- StreamingEnabled can leave cutscene rigs/parts not streamed in on the client. This is community-reported, including with Persistent ([devforum](https://devforum.roblox.com/t/module-script-moon-animator-2-cutscene-support-module/3178584)). Options: group the set as a Model with `ModelStreamingMode = PersistentPerPlayer` and call `AddPersistentPlayer` just before, remove after; or `Atomic`. `RequestStreamAroundAsync` is reported unreliable, so don't rely on it alone ([streaming techniques](https://create.roblox.com/docs/workspace/streaming/techniques)). See [[pipeline/cutscenes]]. TODO(verify)

## Testing (Open Cloud Luau Execution)
- Tasks have full engine API access, **including real DataStores**. Mocking is our job, so the harness must inject mocks. Physics doesn't run. Server/LocalScripts don't auto-run; tests must `require` modules ([ref](https://create.roblox.com/docs/cloud/reference/features/luau-execution)). TODO(verify)
- Limits: 5 min per task, 4 MB script, 450 KB logs kept, max 10 incomplete tasks per place, create-task rate 5/min per key owner. TODO(verify)
