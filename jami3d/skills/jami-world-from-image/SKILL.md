---
name: jami-world-from-image
description: "In JAMI, through its MCP server: Lay out a world from one photo. Use when: From one photo: its ground, what stands where, its camera."
---

# JAMI: Lay out a world from one photo

Generated for DI 1.24 — read the guide for the current text: `read_guide "worlds"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Lay out a world from one photo

From one photo: its ground, what stands where, its camera.

Gather: the photo, its size in pixels; a height you know in it, or the camera's.

1. Keep the photo as a board: one view, cropped whole.
   `edit {"calls":[{"op":"reference.board.set","input":{"sceneId":"scene-1000","assetId":"image-k7f3","name":"Street","views":[{"name":"custom","label":"photo","crop":[0,0,960,640]}]}}]}`
2. Solve its camera from its lines, scaled by an upright of known height or eyeHeightM.
   `read {"calls":[{"op":"reference.calibrate","input":{"boardId":"board-k7f3","mode":"scene","uprightPx":[[412,530],[409,262]],"heightM":1.8}}]}`
3. Mark each thing (box, footprint or foot, route, tags) and areas to scatter: world.layout places each.
   `read {"calls":[{"op":"world.layout","input":{"boardId":"board-k7f3","calibrationId":"staged-0123456789abcdef","objects":[{"name":"Kiosk","route":"program","boxPx":[520,300,610,420],"footprintPx":[[522,418],[606,420],[600,404],[528,402]],"tags":["kiosk"]},{"name":"Tree","route":"nature","preset":"tree.broadleaf","boxPx":[300,160,420,470],"footPx":[360,468]}],"scatter":[{"polygonPx":[[0,560],[960,560],[960,640],[0,640]]}]}}]}`
4. Build the plan in one step: placeholders, a board and a build each, the photo's camera.
   `edit {"calls":[{"op":"world.build","input":{"planId":"staged-0fedcba987654321"}}]}`
5. Send its next calls, then heightfield.generate the terrain (read_guide "nature").
6. Drive each build (read_guide "reconstruction"), as deep as the budget allows: per pass build.next, its route's work keeping its ID (program.nodes.set, program.bake; model.place replaceId: read_guide "generated-models"), build.gates, look.view through the photo's camera beside its crop (look.build: orthographic only), build.review.
   `edit {"calls":[{"op":"program.nodes.set","input":{"entityId":"prop-k7f3","set":[{"node":{"name":"Placeholder"},"sizeM":[2.4,2.6,1.8]}]}}]}`

Verify "The kiosk shows through the photo's camera" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The kiosk shows through the photo's camera","check":{"kind":"visibleInShot","subject":"prop-k7f3","cameraId":"cam-k7f3","atMs":0}}]}`

Look: look.view through the photo's camera, beside the photo.

Pitfalls:

- Mark where each meets the ground: a box alone guesses depth.
- Done: each build done, or ended improved (say so): end: true only once corrections or budget are spent, saying which.
- A generated object's crop leaves only once approved.

The current text: read_guide "worlds".
