# Inbox: install smoke test
from: agent (interactive session) · 2026-11-16

## Detected versions (for [[studio]], humans fill)
- Blender 5.3.0 · Roblox Studio 0.747.0.7471481 · Roblox player 0.747.0.7471481 · Claude Code 2.1.325
- Not installed: rojo, wally, selene, stylua, aftman/rokit/foreman, uv/uvx (Blender MCP needs uvx)

## Blender FBX export (headless `blender -b`, 1×1×1 cube + markers on +Y and +Z)
Raw FBX header values, read straight from the file:
| Variant | UnitScaleFactor | Front axis (sign) | Mesh size |
|---|---|---|---|
| FBX Unit Scale, Z fwd, Y up (Roblox docs) | 100 | 2 (−1) | 1×1×1, scale 1 |
| FBX Unit Scale, −Z fwd, Y up | 100 | 2 (+1) | 1×1×1, scale 1 |
| Scale 0.01, −Z fwd (old advice) | 1 | 2 (+1) | object scale 0.01 |
- The two axis choices differ by 180° about Up. Only a Studio import can say which faces Roblox's Front.
- TODO(human): import `docs_fbxunit.fbx` and `docs_negz.fbx` into Studio (Front / Top / Stud). Check (a) the cube is 1 stud and (b) which one puts the +Y marker on the model's front. Then pin the axis in [[pipeline/assets]].

## Roblox Studio MCP
- `/Applications/RobloxStudio.app/Contents/MacOS/StudioMCP` exists and answers MCP `initialize` (serverInfo `RobloxStudio` 1.0.0, protocol 2025-06-18).
- `list_roblox_studios` → `{"studios":[]}`: Studio wasn't running, so `tools/list` had nothing to proxy.
- Not yet registered in Claude Code (`claude mcp list`).
- Note: the proxy logged "Allowed unauthenticated WebSocket request". Keep it local-only.
