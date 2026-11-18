---
name: jami-export-game-package
description: "In JAMI, through its MCP server: Export a game package. Use when: Scenes, entities or a kit must play in a Three.js game outside JAMI."
---

# JAMI: Export a game package

Generated for DI 1.32 — read the guide for the current text: `read_guide "export"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Export a game package

Scenes, entities or a kit must play in a Three.js game outside JAMI.

Gather: what goes in, by ID: a scene, entities, a kit instance or up to 16 scenes; its name and licence (SPDX terms, holder) from the person.

1. Preview it, writing nothing: size, version, losses, what refuses it (licences, stale forms).
   `read {"calls":[{"op":"export.preview","input":{"target":{"sceneId":"scene-1000"},"format":"jpkg","package":{"name":"Courtyard","licence":{"terms":"CC-BY-4.0","holder":"Example Games"}}}}]}`
2. Clear what refuses it: for a file not the person's own, propose leaving out or replacing what uses it; act on their word. Bake a stale form (form.bake).
3. Write it with the same target and package: a job alone in its edit.
   `edit {"calls":[{"op":"export.package","input":{"target":{"sceneId":"scene-1000"},"package":{"name":"Courtyard","licence":{"terms":"CC-BY-4.0","holder":"Example Games"}}}}]}`
4. Queued or running: read export.status after retryAfterMs until it is ready.
   `read {"calls":[{"op":"export.status","input":{"exportId":"0190f000-0000-7000-8000-0000000e0002"}}]}`
5. Check that very file by its exportId, alone in its edit too.
   `edit {"calls":[{"op":"export.validate","input":{"exportId":"0190f000-0000-7000-8000-0000000e0002"}}]}`
6. Once its verdict is ok, show the person its handoffUrl, version and what a major change removed.

Look: None: numbers say it.

Pitfalls:

- Own content and credited CC0/CC BY library files ship; JAMI-standard, template and platform files and their derivatives are refused.
- A member removed or changed is a major version: games using it break.
- One package at a time: busy? read export.status.
- Motion a game keeps: read_guide "game-packages"; its game side: read_guide "game-runtime".
- leaveOut {ids, tags} ADDS to what the package leaves out (remembered); putBack {ids, tags} takes out (what a tag it carries, or something above it, keeps out returns only with that); leaveOut {only: true, …} is exactly these ({only: true}: nothing). leftOut is the whole choice; sent either, none back: the server ignored it; say so, go no further.

The current text: read_guide "export".
