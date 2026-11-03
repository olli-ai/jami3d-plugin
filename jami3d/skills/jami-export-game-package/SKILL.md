---
name: jami-export-game-package
description: "In JAMI, through its MCP server: Export a game package. Use when: A scene, some of its entities, a kit or several scenes must play in a Three.js game outside JAMI."
---

# JAMI: Export a game package

Generated for DI 1.23 — read the guide for the current text: `read_guide "export"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Export a game package

A scene, some of its entities, a kit or several scenes must play in a Three.js game outside JAMI.

Gather: what goes in: a scene, entities or a kit instance by ID, or up to 16 scenes; its name, and its licence from the person: the terms (an SPDX id) and who holds them.

1. Preview it, writing nothing: its size, tiers and files, the version it would take, its losses, and what refuses it (licences, stale forms).
   `read {"calls":[{"op":"export.preview","input":{"target":{"sceneId":"scene-1000"},"format":"jpkg","package":{"name":"Courtyard","licence":{"terms":"CC-BY-4.0","holder":"Example Games"}}}}]}`
2. Clear what refuses it: a file that is not the person's own is left out or replaced by their own; a stale form is baked (form.bake).
3. Write it with the same target and package: a job, alone in its edit.
   `edit {"calls":[{"op":"export.package","input":{"target":{"sceneId":"scene-1000"},"package":{"name":"Courtyard","licence":{"terms":"CC-BY-4.0","holder":"Example Games"}}}}]}`
4. Still queued or running: read export.status after retryAfterMs, until it is ready.
   `read {"calls":[{"op":"export.status","input":{"exportId":"0190f000-0000-7000-8000-0000000e0002"}}]}`
5. Check that very file as a game reads it, by its exportId: alone in its edit too.
   `edit {"calls":[{"op":"export.validate","input":{"exportId":"0190f000-0000-7000-8000-0000000e0002"}}]}`
6. Once its verdict is ok, show the person its handoffUrl, its version and what a major change removed.

Look: None: the preview's numbers and the check's verdict say what no picture does.

Pitfalls:

- Own content only: library, template and platform files are refused, and anything made of one.
- A member removed or changed makes a major version: games that used it break.
- One package is written at a time: refused as busy, read export.status first.

The current text: read_guide "export".
