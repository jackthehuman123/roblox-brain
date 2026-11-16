# Baselines: asset-builder
Versions: Blender 5.3.0 · Roblox Studio 0.747.0
Last verified: <DATE>
First version written by an agent 2026-11-16 under a one-time human exception. A human must review it.

Harness: `harness/score.sh <task-id> [train|holdout]` in the sandbox repo (`~/Documents/roblox-sandbox`). Task-specific numbers live in each task's `check:` line.

| Check | Target | Scored by |
|---|---|---|
| Triangles under cap | ≤ 20000 per mesh (Roblox spec) TODO(verify) | `check_fbx.py` (blender -b) |
| Triangle budget | ≤ task `max_tris` total | `check_fbx.py` |
| Export scale correct | FBX UnitScaleFactor = 100 (Apply Scalings = FBX Unit Scale), Y up | `check_fbx.py` (raw header) |
| Transforms applied | every mesh scale 1, rotation 0 after import | `check_fbx.py` |
| UVs present | every mesh | `check_fbx.py` |
| Naming | mesh names = task `meshes` | `check_fbx.py` + `studio_check.py` |
| Size | bbox = task `dims` ± `tol`, in Blender **and** in Studio (studs) | `check_fbx.py` + `studio_check.py` |
| Pivot | bottom-center when task says so | `check_fbx.py` |
| Orientation | `front_part` sits toward −Z in Studio | `studio_check.py` |
| Texture size budget | ≤ 1024 px TODO(verify) | `check_fbx.py` |
| Imports into Studio | Open Cloud upload OK + loads in TEST place | `upload_fbx.py` + `studio_check.py` |
| Visual | render + fixed rubric | human spot-check (not scored) |
