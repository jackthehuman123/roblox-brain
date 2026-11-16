# Cutscene pipeline
Versions: Moon Animator 2 <VERSION> · playback module <VERSION>
Last verified: <DATE>
Docs checked: 2026-11-16 by agent. Community sources only (Moon Animator has no official docs here).

1. **Animate** in Moon Animator 2 (human).
2. **Export:** Export All writes rig tracks as KeyframeSequences into the place. The camera is **not** a normal KeyframeSequence: it comes out as a folder of CFrame values (plus FOV). Property tracks (e.g. Transparency) are **not** exported by Export All. TODO(verify) exact menu steps on our version.
3. **Playback module:** decision TODO, not yet chosen. Record it in [[studio]] and the game's decisions.md once picked. Candidates:
   - **Moon2Cutscene** (open source, community): plays Moon 2 save files at runtime from `ServerStorage.MoonAnimator2Saves`. API shape `Moon2Cutscene.new(file, map?)` → `:play()` / `:stop()` / `setFrame`. Handles camera + rigs ([thread](https://devforum.roblox.com/t/v2-moon2cutscene-play-moon-animator-2-files/3001411)). TODO(verify) license + current version.
   - **Moon2Module** (plugin): converts a Moon project to a ModuleScript, including property tracks ([thread](https://devforum.roblox.com/t/moon2module-plugin-that-converts-your-moon-animator-projects-into-modulescripts/2975574)).
   - **Custom:** play exported KeyframeSequences via uploaded Animations + tween the camera from the CFrame folder. The most control and the most code.
4. **Trigger:** <how cutscenes start: server event / zone / etc.>

**StreamingEnabled:** put the set (rigs + props) in a Model with `ModelStreamingMode = PersistentPerPlayer`. The server calls `AddPersistentPlayer(player)` before starting and removes the player after end/skip/error. The client waits for the parts before playing. Don't rely on `RequestStreamAroundAsync` alone. See [[roblox/gotchas]]. TODO(verify) in our game.

Must always be true: player input is restored after end, skip, or error. Works with the game's StreamingEnabled setting.
Per-cutscene notes: `games/<GAME>/cutscenes/` from [[games/_template/cutscenes/_template]].
