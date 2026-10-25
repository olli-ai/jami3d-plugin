---
name: jami-model-from-reference
description: "In JAMI, through its MCP server: Model from a reference, coarse to fine. Use when: A model must match a reference picture."
---

# JAMI: Model from a reference, coarse to fine

Generated for DI 1.16 — read the guide for the current text: `read_guide "playbook-modelling"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Model from a reference, coarse to fine

A model must match a reference picture.

Gather: the board, views named, height in metres (ask the person); the scene.

1. Calibrate; apply its next.
   `read {"calls":[{"op":"reference.calibrate","input":{"boardId":"board-k7f3"}}]}`
2. Level 0: suggested blocks, one form; rename parts.
   `read {"calls":[{"op":"form.suggest","input":{"boardId":"board-k7f3"}}]}`
   `edit {"calls":[{"op":"form.create","input":{"sceneId":"scene-1000","name":"Figure","planId":"staged-4f1c0a9e2b7d3c58"}}]}`
3. Per level: compare; fit the parts it ranks (in a region, the region's own); apply the fit's plan — compare's only if the fit makes none and one call compared every view.
   `read {"calls":[{"op":"reference.compare","input":{"subject":"prop-k7f3","boardId":"board-k7f3","level":0}}]}`
   `read {"calls":[{"op":"form.fit","input":{"entityId":"prop-k7f3","boardId":"board-k7f3","partIds":["part-k7f3"],"level":0}}]}`
   `edit {"calls":[{"op":"form.parts.set","input":{"entityId":"prop-k7f3","planId":"staged-4f1c0a9e2b7d3c58"}}]}`
4. Level 1: shapes from silhouettes; to replace a block, move its children to the new part (keep: "world"), remove it.
   `read {"calls":[{"op":"form.fromSilhouette","input":{"boardId":"board-k7f3","entityId":"prop-k7f3","name":"Body","kind":"loft","region":{"part":"part-k7f3","children":false,"marginFraction":0}}}]}`
   `edit {"calls":[{"op":"form.parts.set","input":{"entityId":"prop-k7f3","move":[{"part":"part-m2q8","parentId":"part-r5t1","keep":"world"}],"remove":[{"part":"part-k7f3"}]}}]}`
5. Level 2: a part's details, placed by reference.locate {onto: {part}}.
   `read {"calls":[{"op":"form.suggest","input":{"boardId":"board-k7f3","entityId":"prop-k7f3","level":1,"region":{"part":"part-m2q8"}}}]}`
6. Level 3: server bake; project, apply, read the picture; nothing floats.
   `edit {"calls":[{"op":"form.bake.prepare","input":{"entityId":"prop-k7f3","resolution":"medium"}}]}`
   `edit {"calls":[{"op":"form.bake","input":{"entityId":"prop-k7f3","bakeId":"fbake-4f1c0a9e2b7d3c58"}}]}`
   `edit {"calls":[{"op":"texture.project","input":{"entityId":"prop-k7f3","boardId":"board-k7f3"}}]}`
   `edit {"calls":[{"op":"texture.apply","input":{"entityId":"prop-k7f3","textureId":"image-k7f3"}}]}`
   `read {"calls":[{"op":"texture.inspect","input":{"entityId":"prop-k7f3","include":["reference"],"boardId":"board-k7f3","views":["front","left"]}}]}`
   `read {"calls":[{"op":"model.sheet","input":{"sceneId":"scene-1000","ids":["prop-k7f3"]}}]}`

Verify "Fits", "Colours", "Closed" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Fits","check":{"kind":"referenceFit","subject":"prop-k7f3","board":"board-k7f3","minIoU":0.9}},{"name":"Colours","check":{"kind":"textureMatch","subject":"prop-k7f3","board":"board-k7f3"}},{"name":"Closed","check":{"kind":"meshSound","entityId":"prop-k7f3"}}]}`

Look: look.region where compare points; albedo after texture.apply.

Pitfalls:

- A part buried in its parent is refused (noSurface): move it out first.
- After the overall bounds move, project again.
- partRelations fails sunk separate parts.
- Over a call's room (overBudget), split views.

The current text: read_guide "playbook-modelling".
