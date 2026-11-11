---
name: jami-world-from-image
description: "In JAMI, through its MCP server: Lay out a world from one photo. Use when: From one photo: its ground, what stands where, its camera."
---

# JAMI: Lay out a world from one photo

Generated for DI 1.25 — read the guide for the current text: `read_guide "worlds"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Lay out a world from one photo

From one photo: its ground, what stands where, its camera.

Gather: the photo, its size in pixels; a height you know in it, or the camera's.

1. Keep the photo as a board: one view, cropped whole.
   `edit {"calls":[{"op":"reference.board.set","input":{"sceneId":"scene-1000","assetId":"image-k7f3","name":"Street","views":[{"name":"custom","label":"photo","crop":[0,0,960,640]}]}}]}`
2. Solve its camera from its lines, scaled by an upright of known height or eyeHeightM.
   `read {"calls":[{"op":"reference.calibrate","input":{"boardId":"board-k7f3","mode":"scene","uprightPx":[[412,530],[409,262]],"heightM":1.8}}]}`
3. After read_guide "world-finish" (once), mark each thing (box, footprint or foot, route, tags) and areas to scatter: world.layout places each.
   `read {"calls":[{"op":"world.layout","input":{"boardId":"board-k7f3","calibrationId":"staged-0123456789abcdef","objects":[{"name":"Kiosk","route":"program","boxPx":[520,300,610,420],"footprintPx":[[522,418],[606,420],[600,404],[528,402]],"tags":["kiosk"]},{"name":"Tree","route":"nature","preset":"tree.broadleaf","boxPx":[300,160,420,470],"footPx":[360,468]}],"scatter":[{"polygonPx":[[0,560],[960,560],[960,640],[0,640]]}]}}]}`
4. Build the plan in one step: placeholders, a board and build each, the photo's camera.
   `edit {"calls":[{"op":"world.build","input":{"planId":"staged-0fedcba987654321"}}]}`
5. Send next's terrain (heightfield.generate bakes it), scatter and presets in order, then world-finish's finish; LAST, each model.generate alone in its edit with confirm: true: STOP until approved.
6. Then world-finish's loop to its stop rule, using the calls you have: every side first (look.turntable round the ground), then each build in place, its ID kept (program.nodes.set; model.place replaceId), look.build, build.review.
   `edit {"calls":[{"op":"program.nodes.set","input":{"entityId":"prop-k7f3","set":[{"node":{"name":"Placeholder"},"sizeM":[2.4,2.6,1.8]}]}}]}`

Verify "The kiosk shows through the photo's camera" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The kiosk shows through the photo's camera","check":{"kind":"visibleInShot","subject":"prop-k7f3","cameraId":"cam-k7f3","atMs":0}}]}`

Look: look.turntable round the ground, then the photo's camera.

Pitfalls:

- Mark where each meets the ground: a box alone guesses depth.
- Done: world-finish's stop rule (say what misses it).
- A generated object's crop leaves only once approved.

The current text: read_guide "worlds".
