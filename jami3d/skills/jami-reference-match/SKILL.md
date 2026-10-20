---
name: jami-reference-match
description: "In JAMI, through its MCP server: Match a model to its reference sheet. Use when: A model must match a reference drawing, a turnaround or a character sheet, view by view."
---

# JAMI: Match a model to its reference sheet

Generated for DI 1.12 — read the guide for the current text: `read_guide "playbook-reference-match"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Match a model to its reference sheet

A model must match a reference drawing, a turnaround or a character sheet, view by view.

Gather: the reference image, an asset of the library; the model: the group of its parts; which sides the sheet draws, and the figure's height in metres.

1. Measure the sheet: its figures' boxes, where the outlines turn, the widths band by band.
   `look {"op":"look.reference","input":{"assetId":"image-k7f3"}}`
2. Keep it as a board: the image, the subject, its height and where each side is drawn — the views of look.reference's next, each renamed to the side it shows.
   `edit {"calls":[{"op":"reference.board.set","input":{"sceneId":"scene-1000","name":"Sheet","assetId":"image-k7f3","subject":"group-6300","heightM":1.7,"views":[{"name":"front","crop":[56,86,311,694]},{"name":"left","crop":[668,86,832,694]}]}}]}`
3. Build, then read the model in numbers: model.sheet for its parts, mesh.section for its cross-sections.
4. Score it view by view: the overlap, the width bands off, swapped views, the parts to change.
   `look {"op":"look.matchReference","input":{"subject":"group-6300","boardId":"board-k7f3"}}`
5. Fix the parts it names and score again; keep it proved with a referenceMatch check. Promotion and export: read_guide "characters".

Verify "The model matches its sheet" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The model matches its sheet","check":{"kind":"referenceMatch","subject":"group-6300","board":"board-k7f3","minIoU":0.85}}]}`

Look: look.turnaround: all its sides at one scale, beside the sheet.

Pitfalls:

- Never judge the likeness by eye: the match scores it.
- Sides are the subject's own: its left is +X when it faces +Z.
- A side drawn mirrored reads as a swapped view: the match names it.

The current text: read_guide "playbook-reference-match".
