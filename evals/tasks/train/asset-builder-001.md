id: asset-builder-001
agent: asset-builder
set: train
prompt: Build a wooden crate as a single mesh named `SM_Crate`, exactly 4 × 4 × 4 studs (X × Y-up × Z), pivot at bottom-center, ≤ 200 triangles, with UVs. Export to `assets/asset-builder-001/SM_Crate.fbx` using [[pipeline/assets]]. Keep the bpy build script next to it as `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-001/`. Studio open on the TEST place with MCP enabled.
check: {"name": "SM_Crate", "meshes": ["SM_Crate"], "dims": [4, 4, 4], "tol": 0.02, "max_tris": 200, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-001 train` → `RESULT overall PASS`
notes: Calibration task. If Blender passes but Studio size is off by a constant factor, the export or importer scale is wrong.
