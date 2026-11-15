---
name: jami-build-from-image
description: "In JAMI, through its MCP server: Build a model from an image. Use when: One subject from pictures or a reference sheet."
---

# JAMI: Build a model from an image

Generated for DI 1.28 — read the guide for the current text: `read_guide "generated-models"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Build a model from an image

One subject from pictures or a reference sheet.

Gather: a calibrated board (or 1–4 views); its height in m (ask).

1. Route: organic or a scene's prop: generated (largest first: read_guide "world-props"); a drawing's blends: a form (read_guide "playbook-modelling"); both: generate, then step 6; a standalone hard-surface object: a program, never generated: read_guide "build-playbook" once, follow ITS loop, not this one. Else a staged build (read_guide "reconstruction"): once it stands, build.start (a world's object: build.next): route generate, form, hybrid (both); boardId (renderSane: IoU 0.85, height within 0.08; none: no fit check, look.build, interior gate); contract, inventory. Per pass build.next, work, build.gates, look.build (via look), build.review.
2. Generate with confirm: true, alone; approved, again with approvalId AND confirm: true.
   `edit {"calls":[{"op":"model.generate","input":{"board":{"boardId":"board-k7f3"},"subject":"a felt owl","heightM":0.3},"approvalId":"0190f000-0000-7000-8000-000000000a99","confirm":true}]}`
3. Wait: it names the file.
   `read {"calls":[{"op":"model.status","input":{"generationId":"018f0000-0000-7000-8000-000000000001","waitMs":20000}}]}`
4. Prepare it (queued: its next).
   `edit {"calls":[{"op":"model.prepare","input":{"assetId":"model-k7f3","heightM":0.3}}]}`
5. Place it; collider if stood on.
   `edit {"calls":[{"op":"model.place","input":{"preparedId":"mesh-k7f3","sceneId":"scene-1000","collider":"box"}}]}`
6. Hard parts: a program under it.
   `edit {"calls":[{"op":"program.create","input":{"sceneId":"scene-1000","name":"Stand","parentId":"prop-k7f3","nodes":[{"kind":"box","name":"Base","sizeM":[0.24,0.02,0.24],"at":[0,-0.01,0],"bevelM":0.004}]}}]}`
7. Read it in numbers; baked light: texture.delight. Done: build done, or ended improved (say so).
   `read {"calls":[{"op":"model.sheet","input":{"sceneId":"scene-1000","ids":["prop-k7f3"]}}]}`

Look: look.turnaround: unseen sides are guessed.

Pitfalls:

- Never skip build.review; as many passes as budget allows. Send end: true only once corrections or budget are spent (say which): it always ends the build.
- Others' pictures: the person's OK.
- Kill switch: stop, tell them.

The current text: read_guide "generated-models".
