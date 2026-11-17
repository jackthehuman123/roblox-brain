# Candidate: asset-builder
Based on card: v1 · Batch: r001–r003 (asset-builder-001…003, train) · Status: DRAFT   <!-- DRAFT | HOLDOUT-TESTED | PROMOTABLE | REJECTED -->
Agents write this file. Only a human promotes it to [[agents/asset-builder/card|card]].

## Proposed change (as a diff against card.md / lessons.md)
Batch was 3/3 PASS on card v1, so nothing here fixes a scored failure. These are build-time habits that caught or avoided errors before scoring. Holdout can only show non-regression.

card.md → `## Does`, add:
+ - build.py prints triangle count and min/max bounds and asserts the tri budget before exporting; re-import the FBX in a fresh Blender to measure before handing off.

lessons.md, add (status: proposed):
+ - Recessed panels: bmesh `inset_individual(thickness=FRAME)` then `inset_individual(thickness=0, depth=-recess)`; `extrude_face_region` leaves the original faces and pushes outward (gave 4.24 studs / 120 tris) — from [[runs/2026-11/r001]] — status: proposed
+ - Round meshes: segment count divisible by 4 so verts land on ±X/±Y, else footprint is under the stated diameter — from [[runs/2026-11/r002]] — status: proposed
+ - Cylinder UVs: base U on segment index (i+1), not the wrapped neighbour, or the seam face stretches across the strip — from [[runs/2026-11/r002]] — status: proposed
+ - Multi-mesh assets: every part's origin at the shared asset pivot (world origin), transforms applied; measure the combined bbox on re-import — from [[runs/2026-11/r003]] — status: proposed
+ - Unwrap UVs after scaling (or use world-space box projection) to keep texel density uniform — from [[runs/2026-11/r003]] — status: proposed

Loads (pending, separate from the above so holdout can tell them apart):
+ @refs/asset-design/index.md (vN)   ← add once asset-researcher has written a version a human has skimmed; test it on holdout on its own

## Not for the card (human decisions)
- ~~The agent cannot self-run `harness/check_fbx.py`~~ Resolved 2026-11-16 (human decision): check_fbx.py takes the `check:` JSON inline, and /train passes it in the subagent prompt. See [[games/sandbox/decisions]].
- Harness gap: Studio checks total size only, not the Model pivot / bottom-center in Studio (r003).
- No task exercises embedded textures yet (all three "no textures").
- pipeline/assets.md still leaves triangulation undecided (r001).

## Evidence (links to run notes)
- [[runs/2026-11/r001]] — asset-builder-001 — RESULT overall PASS (blender 10/10, studio 3/3)
- [[runs/2026-11/r002]] — asset-builder-002 — RESULT overall PASS (blender 10/10, studio 3/3)
- [[runs/2026-11/r003]] — asset-builder-003 — RESULT overall PASS (blender 10/10, studio 3/3)

## Holdout result (pasted from harness, current card vs candidate)
- (not run yet — `/train asset-builder holdout`)
