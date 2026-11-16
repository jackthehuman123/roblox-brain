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
- Forward / Up axis: **Z Forward / Y Up** per Roblox's Blender page. TODO(verify)
  - Tested 2026-11-16 (Blender 5.3.0 → Open Cloud upload → Studio 0.747): Z and −Z forward gave the **same** result. Geometry on Blender **−Y** (the side the Front view looks at) ends up on Roblox **−Z** (front / LookVector). The importer honours the FBX axis metadata, so model the front toward Blender −Y.
  - Tested 2026-11-16: FBX Unit Scale + Unit System None → **1 Blender unit = 1 stud** in Studio (4×4×4 cube measured 4×4×4).
- Armature: **Add Leaf Bones off**
- Bake Animation: off unless exporting keyframed animation
- Selected objects only: <YES/NO>
- Other: <SETTINGS>

## Studio import
- Scripted route (training): Open Cloud Assets API upload (FBX → Model) → load by asset ID. See [[games/sandbox/decisions]].

### Manual route (3D Importer)
- File Transform: World Forward **Front**, World Up **Top** TODO(verify)
- File Geometry: Scale Unit **Stud** TODO(verify)
- After import: record the asset ID in `games/<GAME>/assets.md`
- Gate: must pass [[evals/assets/baselines]] first
