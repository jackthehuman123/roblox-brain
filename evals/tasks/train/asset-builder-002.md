id: asset-builder-002
agent: asset-builder
set: train
prompt: Build a stone pillar as one mesh named `SM_Pillar`: cylinder 2 studs in diameter and 10 studs tall (Y up), pivot at bottom-center, ≤ 400 triangles, with UVs. Export to `assets/asset-builder-002/SM_Pillar.fbx` per [[pipeline/assets]], with `build.py` beside it.
setup place or files: sandbox repo, empty `assets/asset-builder-002/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Pillar", "meshes": ["SM_Pillar"], "dims": [2, 10, 2], "tol": 0.03, "max_tris": 400, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-002 train` → `RESULT overall PASS`
notes: Tests the up axis (a lying-down pillar fails dims).
