id: asset-builder-004
agent: asset-builder
set: train
prompt: Build a low-poly boulder as one mesh named `SM_Rock`, irregular (not a plain primitive), bounding box about 3 × 2 × 3 studs (X × Y-up × Z), pivot at bottom-center, ≤ 800 triangles, with UVs. Export to `assets/asset-builder-004/SM_Rock.fbx` per [[pipeline/assets]], with `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-004/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Rock", "meshes": ["SM_Rock"], "dims": [3, 2, 3], "tol": 0.1, "max_tris": 800, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-004 train` → `RESULT overall PASS`
notes: Procedural displacement tends to blow the bbox or the tri budget. Shape quality is a human spot-check, not scored.
