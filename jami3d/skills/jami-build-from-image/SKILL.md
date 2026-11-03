---
name: jami-build-from-image
description: "In JAMI, through its MCP server: Build a model from an image. Use when: A model must be made from pictures or a reference sheet of one subject."
---

# JAMI: Build a model from an image

Generated for DI 1.23 — read the guide for the current text: `read_guide "generated-models"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Build a model from an image

A model must be made from pictures or a reference sheet of one subject.

Gather: 1–4 views by asset ID, or a calibrated board; its height in metres (ask the person); the scene.

1. Route: organic (a body, a plush, a soft shape) is generated; edges and panels are a program (read_guide "programs"); blends matched to a drawing, a form (read_guide "playbook-modelling"); both: generate, then step 6.
2. Generate with confirm: true, alone in its edit: it answers an approval; once the person approves it in JAMI, send it again with its approvalId.
   `edit {"calls":[{"op":"model.generate","input":{"board":{"boardId":"board-k7f3"},"subject":"a felt owl","heightM":0.3}}]}`
3. Poll until done: it names the model file.
   `read {"calls":[{"op":"model.status","input":{"generationId":"018f0000-0000-7000-8000-000000000001"}}]}`
4. Prepare it on the server (framed, cleaned, decimated, de-lit); queued: call it again.
   `edit {"calls":[{"op":"model.prepare","input":{"assetId":"model-k7f3","heightM":0.3}}]}`
5. Place it, with a collider if things stand on it.
   `edit {"calls":[{"op":"model.place","input":{"preparedId":"mesh-k7f3","sceneId":"scene-1000","collider":"box"}}]}`
6. Hard parts: a program under it, in its frame (feet at the origin, facing +Z).
   `edit {"calls":[{"op":"program.create","input":{"sceneId":"scene-1000","name":"Stand","parentId":"prop-k7f3","nodes":[{"kind":"box","name":"Base","sizeM":[0.24,0.02,0.24],"at":[0,-0.01,0],"bevelM":0.004}]}}]}`
7. Read it in numbers. Light baked in its colours: texture.delight.
   `read {"calls":[{"op":"model.sheet","input":{"sceneId":"scene-1000","ids":["prop-k7f3"]}}]}`

Verify "Fits its board" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Fits its board","check":{"kind":"referenceFit","subject":"prop-k7f3","board":"board-k7f3","minIoU":0.85}}]}`

Look: look.turnaround: every side; one no picture shows is the vendor's guess.

Pitfalls:

- Hard-surface subjects are never generated: build a program.
- Nothing is sent until the person approves.
- Someone else's picture needs the person's word that they may send it.
- Refused as switched off (a kill switch): stop, tell the person.

The current text: read_guide "generated-models".
