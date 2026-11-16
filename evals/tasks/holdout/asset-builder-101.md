id: asset-builder-101
agent: asset-builder
set: holdout
prompt: Build a park bench as meshes `SM_Bench_Seat`, `SM_Bench_Back`, `SM_Bench_LegL`, `SM_Bench_LegR`. Whole bench 5 wide (X) × 2.5 tall (Y) × 1.5 deep (Z) studs, with the backrest at the back (+Z; the seat faces −Z). Pivot at bottom-center, ≤ 1500 triangles total, all with UVs. Export to `assets/asset-builder-101/SM_Bench.fbx` per [[pipeline/assets]], with `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-101/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Bench", "meshes": ["SM_Bench_Seat", "SM_Bench_Back", "SM_Bench_LegL", "SM_Bench_LegR"], "dims": [5, 2.5, 1.5], "tol": 0.05, "max_tris": 1500, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-101 holdout` → `RESULT overall PASS`
notes: Holdout. Never quote in lessons.
