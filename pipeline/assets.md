# Asset pipeline: Blender → FBX → Studio
Single source of truth for export settings. Change only by human decision.
Versions: Blender <VERSION> · Roblox engine <VERSION>
Last verified: <DATE>
Docs checked: 2026-11-16 by agent. Values below are from Roblox docs ([blender](https://create.roblox.com/docs/art/blender), [export reqs](https://create.roblox.com/docs/art/modeling/export-requirements)) and await a human test export.

## Blender
- Units: Scene → Units → Unit System **None**, Rotation **Degrees** TODO(verify)
- Before export: apply all transforms (Ctrl+A → All Transforms), check UVs. Triangulate? <YES/NO> TODO(verify): docs give no rule, so decide after a test import
- Triangle cap: 20,000 per mesh, see [[roblox/gotchas]] TODO(verify)
- Calibrate once: export a Studio 1×1×1 part, round-trip it, and confirm size and orientation.
- Naming: see [[studio]]

## FBX export settings
- Path Mode: **Copy** + **Embed Textures** on (otherwise grey mesh) TODO(verify)
- Apply Scalings: **FBX Unit Scale**. All other scales 1.0. Not 0.01, which is the old advice and now a fallback only. TODO(verify)
- Forward / Up axis: **Z Forward / Y Up** per Roblox's Blender page. Community guides say −Z Forward; settle it with the calibration export. TODO(verify)
- Armature: **Add Leaf Bones off**
- Bake Animation: off unless exporting keyframed animation
- Selected objects only: <YES/NO>
- Other: <SETTINGS>

## Studio import (3D Importer)
- File Transform: World Forward **Front**, World Up **Top** TODO(verify)
- File Geometry: Scale Unit **Stud** TODO(verify)
- After import: record the asset ID in `games/<GAME>/assets.md`
- Gate: must pass [[evals/assets/baselines]] first
