---
name: jami-build-from-image
description: "In JAMI, through its MCP server: Build a model from an image. Use when: One subject, from pictures or a reference sheet."
---

# JAMI: Build a model from an image

Generated for DI 1.23 — read the guide for the current text: `read_guide "generated-models"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Build a model from an image

One subject, from pictures or a reference sheet.

Gather: a calibrated board, or 1–4 views by asset ID; its height in metres (ask the person).

1. Route: organic (a body, a plush): generated; edges and panels, never generated: a program (read_guide "programs"); a drawing's blends: a form (read_guide "playbook-modelling"); both: generate, then step 6. Each, a staged build (read_guide "reconstruction"): once it stands, build.start (route generate, program, form, hybrid (both); boardId, or look.build and the interior gate cannot judge; contract, inventory); per pass build.next, work, build.gates, look.build (via look; orthographic only), build.review.
2. Generate with confirm: true, alone in its edit; approved by the person, resend it with its approvalId.
   `edit {"calls":[{"op":"model.generate","input":{"board":{"boardId":"board-k7f3"},"subject":"a felt owl","heightM":0.3}}]}`
3. Poll until done: it names the model file.
   `read {"calls":[{"op":"model.status","input":{"generationId":"018f0000-0000-7000-8000-000000000001"}}]}`
4. Prepare it (framed, cleaned, de-lit); queued: call it again.
   `edit {"calls":[{"op":"model.prepare","input":{"assetId":"model-k7f3","heightM":0.3}}]}`
5. Place it; a collider if things stand on it.
   `edit {"calls":[{"op":"model.place","input":{"preparedId":"mesh-k7f3","sceneId":"scene-1000","collider":"box"}}]}`
6. Hard parts: a program under it, in its frame.
   `edit {"calls":[{"op":"program.create","input":{"sceneId":"scene-1000","name":"Stand","parentId":"prop-k7f3","nodes":[{"kind":"box","name":"Base","sizeM":[0.24,0.02,0.24],"at":[0,-0.01,0],"bevelM":0.004}]}}]}`
7. Read it in numbers; baked-in light: texture.delight. Done: its build done, or ended improved (say so).
   `read {"calls":[{"op":"model.sheet","input":{"sceneId":"scene-1000","ids":["prop-k7f3"]}}]}`

Look: look.turnaround: an unseen side is the vendor's guess.

Pitfalls:

- Never skip build.review. Passes: as many as the person's budget allows (tight: one reviewed); end: true only once corrections or budget are spent: say which.
- Someone else's picture needs the person's word to send it.
- A kill switch: stop, tell the person.

The current text: read_guide "generated-models".
