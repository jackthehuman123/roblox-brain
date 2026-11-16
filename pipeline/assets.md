# Asset pipeline: Blender → FBX → Studio
Single source of truth for export settings. Change only by human decision.
Versions: Blender <VERSION> · Roblox engine <VERSION>
Last verified: <DATE>

## Blender
- Units: <UNITS> TODO(verify)
- Before export: apply transforms, check UVs, triangulate? <YES/NO> TODO(verify)
- Triangle cap: see [[roblox/gotchas]] (<CAP>)
- Naming: see [[studio]]

## FBX export settings
- Scale: 0.01 (1 m = 1 stud) TODO(verify)
- Forward / Up axis: <AXIS> TODO(verify)
- Apply scalings: <SETTING> TODO(verify)
- Selected objects only: <YES/NO>
- Other: <SETTINGS>

## Studio import
- Importer: <3D Importer settings> TODO(verify)
- After import: record the asset ID in `games/<GAME>/assets.md`
- Gate: must pass [[evals/assets/baselines]] first
