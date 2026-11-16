id: asset-builder-102
agent: asset-builder
set: holdout
prompt: Build a barrel as one mesh named `SM_Barrel`: 2.5 studs in diameter, 3.5 studs tall (Y up), slightly bulged in the middle (max diameter 2.5), pivot at bottom-center, ≤ 600 triangles, with UVs. Export to `assets/asset-builder-102/SM_Barrel.fbx` per [[pipeline/assets]], with `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-102/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Barrel", "meshes": ["SM_Barrel"], "dims": [2.5, 3.5, 2.5], "tol": 0.04, "max_tris": 600, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-102 holdout` → `RESULT overall PASS`
notes: Holdout. Never quote in lessons.
