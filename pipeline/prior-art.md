# Prior art: pipelines other people use
Collected 2026-11-16 by agent. Pointers only. Nothing here is adopted until it's logged in [[studio]] or a game's decisions.md.
Our constraint still wins: no GitHub Actions / headless Claude (see [[README]]). Reuse their *scripts* and run them by hand from Bash in an interactive session.

## Code + tests (for [[agents/server-scripter/card]], harness in [[evals/README]])
- **Common toolchain:** Rojo (sync) + Wally (packages) + Selene (lint) + StyLua (format). Most Claude Code + Roblox guides assume this. Claude edits files and Rojo syncs them to Studio.
- **Roblox/place-ci-cd-demo** ([repo](https://github.com/Roblox/place-ci-cd-demo), archived Sep 2024 but still the official reference). Flow: `rojo build` → upload .rbxl to a **TEST place** → run Luau via Open Cloud Luau Execution → read results. Python wrappers in `/scripts`. Needs an API key with `universe.places:write` + `universe.place.luau-execution-session:write`. Closest match to our [[pipeline/loop]] step 3.
- **Jest-Lua** ([jsdotlua/jest-lua](https://github.com/jsdotlua/jest-lua)). Runs only inside Roblox. Wally dev-deps `Jest` + `JestGlobals`; v3 requires `jest.config.lua`; entry is `runCLI`. Older local runner: `run-in-roblox` (needs Studio). Don't confuse it with Roblox's internal "Jest Roblox", which has a similar API but is a different package.
- **Cloud Jest runners** (community): jestir, jest-rodeo. They wrap Jest-Lua + Luau Execution (universe/place/version/API key). TODO(verify) before use.
- **Known limits:** Luau Execution can reach real DataStores (we must inject mocks), has no physics, and caps tasks at 5 min. See [[roblox/gotchas]].

## Studio automation
- **Built-in Studio MCP** (`Roblox_Studio`, 30 tools: scripts, `execute_luau`, playtest, `screen_capture`, input simulation, generation). The official route now. Setup is in [[integration/claude-code/README]].
- Community MCPs: boshyxd/robloxstudio-mcp, hope1026/roblox-mcp. Unofficial; review the code before use.
- A common community loop: brief → plan → dry run → apply in Studio → validate → playtest. Similar to our loop, minus scoring.

## Assets (for [[agents/asset-builder/card]])
- Roblox docs' Blender flow: FBX Unit Scale, Z fwd / Y up, embed textures; the importer uses Front / Top / Stud. Calibrate with a round-tripped 1-stud cube. Values are in [[pipeline/assets]].
- Blender MCP (`ahujasid/blender-mcp`): the agent drives live Blender with `execute_blender_code`. Our check scripts still run separately (`blender -b -P`).

## Cutscenes (for [[agents/cutscene-integrator/card]])
- Moon2Cutscene (runtime player), Moon2Module (project → ModuleScript), or custom camera-CFrame playback. Details are in [[pipeline/cutscenes]].
- StreamingEnabled: PersistentPerPlayer set + `AddPersistentPlayer` is the community pattern.
