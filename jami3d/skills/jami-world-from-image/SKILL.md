---
name: jami-world-from-image
description: "In JAMI, through its MCP server: Lay out a world from one photo. Use when: A scene is laid out from one photo of a place: its ground, what stands where, the camera."
---

# JAMI: Lay out a world from one photo

Generated for DI 1.23 — read the guide for the current text: `read_guide "worlds"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Lay out a world from one photo

A scene is laid out from one photo of a place: its ground, what stands where, the camera.

Gather: the photo (an image asset) and its size in pixels; a height in it you know, or the camera's; a box round each thing in it, and how each is built.

1. Keep the photo as a board of one view, its crop the whole image.
   `edit {"calls":[{"op":"reference.board.set","input":{"sceneId":"scene-1000","assetId":"image-k7f3","name":"Street","views":[{"name":"custom","label":"photo","crop":[0,0,960,640]}]}}]}`
2. Solve its camera from its lines, scaled by an upright of known height or eyeHeightM: 10° up to 45° down. focalFrom and heightFrom say what is a prior.
   `read {"calls":[{"op":"reference.calibrate","input":{"boardId":"board-k7f3","mode":"scene","uprightPx":[[412,530],[409,262]],"heightM":1.8}}]}`
3. Mark each thing (a box, its footprint or foot, its route and tags) and areas to scatter: world.layout places each, with its spreadPct.
   `read {"calls":[{"op":"world.layout","input":{"boardId":"board-k7f3","calibrationId":"staged-0123456789abcdef","objects":[{"name":"Kiosk","route":"program","boxPx":[520,300,610,420],"footprintPx":[[522,418],[606,420],[600,404],[528,402]],"tags":["kiosk"]},{"name":"Tree","route":"nature","preset":"tree.broadleaf","boxPx":[300,160,420,470],"footPx":[360,468]}],"scatter":[{"polygonPx":[[0,560],[960,560],[960,640],[0,640]]}]}}]}`
4. Build the plan in one step: tagged placeholders, a board and a build each, a camera at the photo's pose.
   `edit {"calls":[{"op":"world.build","input":{"planId":"staged-0fedcba987654321"}}]}`
5. Send its next (terrain, scatter, presets), then heightfield.generate the terrain (read_guide "nature").
6. Build each by its route, keeping its ID: program.nodes.set, then program.bake; or model.place with replaceId (read_guide "generated-models").
   `edit {"calls":[{"op":"program.nodes.set","input":{"entityId":"prop-k7f3","set":[{"node":{"name":"Placeholder"},"sizeM":[2.4,2.6,1.8]}]}}]}`

Verify "The kiosk shows through the photo's camera" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The kiosk shows through the photo's camera","check":{"kind":"visibleInShot","subject":"prop-k7f3","cameraId":"cam-k7f3","atMs":0}}]}`

Look: look.view through the photo's camera, beside the photo.

Pitfalls:

- Mark where things meet the ground: a box alone guesses depth (footFromBox).
- A far object's spreadPct is wide.
- A generated object's crop leaves only once approved.

The current text: read_guide "worlds".
