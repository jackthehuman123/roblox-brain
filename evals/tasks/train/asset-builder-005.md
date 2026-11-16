id: asset-builder-005
agent: asset-builder
set: train
prompt: Build a signpost as two meshes: `SM_Signpost_Post` (0.4 × 5 × 0.4 studs) and `SM_Signpost_Tip` (an arrow head 1 × 1 × 1) attached at the top and pointing toward the model's **front** (Roblox front = −Z, i.e. the direction a Model's LookVector points). Whole model about 1 × 5.5 × 1.5 studs, pivot at bottom-center of the post, ≤ 300 triangles, with UVs. Export to `assets/asset-builder-005/SM_Signpost.fbx` per [[pipeline/assets]], with `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-005/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Signpost", "meshes": ["SM_Signpost_Post", "SM_Signpost_Tip"], "dims": [1, 5.5, 1.5], "tol": 0.1, "max_tris": 300, "front_part": "SM_Signpost_Tip"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-005 train` → `RESULT overall PASS`
notes: Settles the Z vs −Z forward-axis question in [[pipeline/assets]]: studio_front_is_minus_z must pass.
