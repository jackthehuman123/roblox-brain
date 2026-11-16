# Cutscene pipeline
Versions: Moon Animator 2 <VERSION> · playback module <VERSION>
Last verified: <DATE>

1. **Animate** in Moon Animator 2 (human).
2. **Export:** Export All → KeyframeSequences → ServerStorage. TODO(verify) exact steps
3. **Playback module:** decision TODO, not yet chosen. Record it in [[studio]] and the game's decisions.md once picked.
4. **Trigger:** <how cutscenes start: server event / zone / etc.>

Must always be true: player input is restored after end, skip, or error. Works with the game's StreamingEnabled setting (see [[roblox/gotchas]]).
Per-cutscene notes: `games/<GAME>/cutscenes/` from [[games/_template/cutscenes/_template]].
