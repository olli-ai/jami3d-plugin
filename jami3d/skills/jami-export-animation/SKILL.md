---
name: jami-export-animation
description: "In JAMI, through its MCP server: Export an animation. Use when: A character's motion must play in other software: Blender, a game engine, a VRM app."
---

# JAMI: Export an animation

Generated for DI 1.18 — read the guide for the current text: `read_guide "motion-export"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Export an animation

A character's motion must play in other software: Blender, a game engine, a VRM app.

Gather: the characters, by their IDs, and the span to bake; the format the person's software opens.

1. Preview, writing nothing, what the file would carry and lose with the options characters and performance: read what its report blocks, then its losses.
   `read {"calls":[{"op":"export.preview","input":{"target":{"sceneId":"scene-1000","entityIds":["char-6300"]},"format":"fbx","options":{"characters":"auto","performance":{"fromMs":0,"toMs":4000}}}}]}`
2. Check it as Blender plays it, in a file written only to be checked: a job, alone in its edit.
   `edit {"calls":[{"op":"export.validate","input":{"target":{"sceneId":"scene-1000","entityIds":["char-6300"]},"format":"fbx","options":{"characters":"auto","performance":{"fromMs":0,"toMs":4000}}}}]}`
3. Once its verdict is ok, write the file: alone in its edit too.
   `edit {"calls":[{"op":"export.model","input":{"target":{"sceneId":"scene-1000","entityIds":["char-6300"]},"format":"fbx","options":{"characters":"auto","performance":{"fromMs":0,"toMs":4000}}}}]}`
4. Still running: read export.status until it is ready, then show the person its handoffUrl.
   `read {"calls":[{"op":"export.status","input":{"exportId":"0190f000-0000-7000-8000-0000000e0001"}}]}`

Look: None: export.validate checks the file as Blender plays it, which no picture does.

Pitfalls:

- A model its licence keeps in JAMI refuses model and rig; neutral carries none of it, and auto picks it.
- A VRMA holds the neutral skeleton alone; a format a mode does not reach leaves the character out.
- rootMotion apply carries the travel in the hips; inPlace keeps the body on its mark.
- Never call export.model again to check: export.status reads it.

The current text: read_guide "motion-export".
