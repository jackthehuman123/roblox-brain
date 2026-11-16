# Baselines: asset-builder
Versions: Blender <VERSION> · Roblox engine <VERSION>
Last verified: <DATE>

| Check | Target | Scored by |
|---|---|---|
| Triangles under cap | ≤ <CAP> TODO(verify) | `blender -b -P` check script |
| Export scale correct | 1 m = 1 stud | `blender -b -P` check script |
| Transforms applied | loc/rot/scale applied | `blender -b -P` check script |
| UVs present | every mesh | `blender -b -P` check script |
| Naming convention | matches [[studio]] | check script |
| Texture size budget | ≤ <SIZE> px | check script |
| Visual | render + fixed rubric | render script + human spot-check |
