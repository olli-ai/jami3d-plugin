---
name: jami-reference-match
description: "In JAMI, through its MCP server: Match a model to its reference sheet. Use when: A model must match a reference drawing, a turnaround or a character sheet, view by view."
---

# JAMI: Match a model to its reference sheet

Generated for DI 1.17 — read the guide for the current text: `read_guide "playbook-reference-match"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Match a model to its reference sheet

A model must match a reference drawing, a turnaround or a character sheet, view by view.

Gather: the reference image, an asset of the library; the model: one form; which sides the sheet draws, and the figure's height in metres.

1. Measure the sheet: its figures' boxes, where the outlines turn, the widths band by band.
   `look {"op":"look.reference","input":{"assetId":"image-k7f3"}}`
2. Keep it as a board: the image, the subject, its height and where each side is drawn — the views of look.reference's next, each renamed to the side it shows.
   `edit {"calls":[{"op":"reference.board.set","input":{"sceneId":"scene-1000","name":"Sheet","assetId":"image-k7f3","subject":"prop-k7f3","heightM":1.7,"views":[{"name":"front","crop":[56,86,311,694]},{"name":"left","crop":[668,86,832,694]}]}}]}`
3. Calibrate it; apply its next (reference.camera.set).
   `read {"calls":[{"op":"reference.calibrate","input":{"boardId":"board-k7f3"}}]}`
4. Build it as one form, then read it in numbers: model.sheet for its parts, mesh.section for its cross-sections.
5. Score it view by view: the overlap and the contour, the worst spots and the parts that own them, the calls that move them (next).
   `read {"calls":[{"op":"reference.compare","input":{"subject":"prop-k7f3","boardId":"board-k7f3"}}]}`
6. Apply its next and score again; keep it proved with a referenceFit check. Promotion and export: read_guide "characters".

Verify "The model matches its sheet" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The model matches its sheet","check":{"kind":"referenceFit","subject":"prop-k7f3","board":"board-k7f3","minIoU":0.85}}]}`

Look: look.turnaround: all its sides at one scale, beside the sheet.

Pitfalls:

- Never judge the likeness by eye: the comparison scores it.
- Sides are the subject's own: its left is +X when it faces +Z.
- A side drawn mirrored reads as a swapped view: the comparison names it (mirror).

The current text: read_guide "playbook-reference-match".
