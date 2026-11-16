id: asset-builder-003
agent: asset-builder
set: train
prompt: Build a table as five meshes: `SM_Table_Top` (6 × 0.5 × 4 studs) and legs `SM_Table_Leg1`…`SM_Table_Leg4` (0.5 × 3 × 0.5 each, under the corners). Whole table: 6 wide (X) × 3.5 tall (Y) × 4 deep (Z), pivot at bottom-center, ≤ 1000 triangles total, all with UVs. Export all to `assets/asset-builder-003/SM_Table.fbx` per [[pipeline/assets]], with `build.py`.
setup place or files: sandbox repo, empty `assets/asset-builder-003/`. Studio TEST place with MCP enabled.
check: {"name": "SM_Table", "meshes": ["SM_Table_Top", "SM_Table_Leg1", "SM_Table_Leg2", "SM_Table_Leg3", "SM_Table_Leg4"], "dims": [6, 3.5, 4], "tol": 0.02, "max_tris": 1000, "origin": "bottom_center"}
pass criteria (machine-checkable):
- `harness/score.sh asset-builder-003 train` → `RESULT overall PASS`
notes: Multi-mesh. Tests naming and transforms applied on every object.
