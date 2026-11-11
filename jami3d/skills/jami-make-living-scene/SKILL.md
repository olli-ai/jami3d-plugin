---
name: jami-make-living-scene
description: "In JAMI, through its MCP server: Make a living scene. Use when: Ground and plants that move in the wind — a field, a wood — must be built in numbers, each plant addressable."
---

# JAMI: Make a living scene

Generated for DI 1.25 — read the guide for the current text: `read_guide "playbook-living-scene"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Make a living scene

Ground and plants that move in the wind — a field, a wood — must be built in numbers, each plant addressable.

Gather: the scene, and the square the place covers in metres; what grows there: the plant presets (read_guide "nature").

1. Lay the ground: a heightfield of seeded relief, its layers, its tags. heightfield.generate bakes it on the server (queued or running: again), its walkable ground too.
   `edit {"calls":[{"op":"heightfield.create","input":{"sceneId":"scene-1000","sizeM":128,"cells":256,"generator":{"kind":"fractal","seed":7,"heightM":6,"featureM":48},"layers":[{"name":"Grass","color":"#4a7a35"},{"name":"Earth","color":"#6b5a43"}],"tags":["meadow"]}}]}`
   `edit {"calls":[{"op":"heightfield.generate","input":{"entityId":"env-k7f3"}}]}`
2. Measure the ground where plants of their own will stand.
   `read {"calls":[{"op":"space.heightAt","input":{"sceneId":"scene-1000","points":[[12,-8],[4,6]]}}]}`
3. Make them from presets at those heights. Trees, shrubs, ferns and stones answer stale: program.bake.prepare, then program.bake its bakeId.
   `edit {"calls":[{"op":"program.create","input":{"sceneId":"scene-1000","name":"Oak","preset":"tree.broadleaf","transform":{"position":[12,1.7,-8]}}},{"op":"program.create","input":{"sceneId":"scene-1000","name":"Grass","preset":"grass.clump","transform":{"position":[4,1.2,6]}}}]}`
   `edit {"calls":[{"op":"program.bake.prepare","input":{"entityId":"prop-m2q8"}}]}`
4. Scatter more, sampled on the server in 32 m chunks (64 a call), one weight a prop, off steep slopes and water. Send its next to array.scatter with prototypeIds in weight order: grass, then oak.
   `edit {"calls":[{"op":"array.scatter.prepare","input":{"sceneId":"scene-1000","area":{"min":[-64,-64],"max":[64,64]},"spacingM":2,"groundId":"env-k7f3","weights":[8,1],"slopeDeg":[0,30],"avoidWater":true}}]}`
5. Give the scene a wind: plants sway by the wind fields their bakes carry.
   `edit {"calls":[{"op":"wind.set","input":{"sceneId":"scene-1000","fromDeg":250,"speedMs":5,"gust":0.3}}]}`
6. By tag: a scattered plant is prop-k7f3#<id>; entity.fromInstance makes it an entity.
   `read {"calls":[{"op":"entity.select","input":{"sceneId":"scene-1000","select":{"tags":{"all":["tree"]}},"instances":true}}]}`
7. Creatures that live on its ground: read_guide "life"; a game package of it: read_guide "export".

Look: look.view from above and at eye height; look.contactSheet for the wind.

Pitfalls:

- Measure the ground first: never y = 0.
- A prototype is baked before array.scatter.
- A preset beside materials is refused: program.set after.
- Species are presets and tags, never kinds.

The current text: read_guide "playbook-living-scene".
