---
name: jami-interactive-scene
description: "In JAMI, through its MCP server: Make motion a viewer changes. Use when: When a tap, a drag or a choice must change how things move as it plays: drift, bounce, push, spin, settle."
---

# JAMI: Make motion a viewer changes

Generated for DI 1.24 — read the guide for the current text: `read_guide "reactive-motion"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Make motion a viewer changes

When a tap, a drag or a choice must change how things move as it plays: drift, bounce, push, spin, settle.

Gather: what the viewer can do, and what each act changes (ask the person); its walls: camera.analyze's fovDeg and aspect at its depth.

1. Ask first; tell the person what cannot react: moving things never collide.
2. A speed param (ambient, the default) and a clock whose rate is that speed.
   `edit {"calls":[{"op":"igraph.create","input":{"entityId":"prop-5d7f"}},{"op":"igraph.param.add","input":{"entityId":"prop-5d7f","key":"vx","param":{"type":"number","label":"Speed","default":0.4}}},{"op":"igraph.param.add","input":{"entityId":"prop-5d7f","key":"u","param":{"type":"clock","label":"Travel","rate":"param.vx"}}}]}`
3. Drive the place from the clock, rest included: here it bounces between x = -2.4 and 2.4.
   `edit {"calls":[{"op":"rig.driver.add","input":{"entityId":"prop-5d7f","target":"self/translation[0]","expr":"2.4 - abs((u + 3.6) % 9.6 - 4.8)","variables":[{"name":"u","source":{"kind":"param","param":"u"}}]}}]}`
4. A tap sets the speed (set, never tween); a repeating timer settles it back.
   `edit {"calls":[{"op":"igraph.timer.add","input":{"entityId":"prop-5d7f","key":"settle","timer":{"durationMs":250,"repeat":true}}},{"op":"igraph.listener.add","input":{"entityId":"prop-5d7f","listener":{"input":{"kind":"click"},"actions":[{"kind":"set","param":"vx","value":"param.vx * 3"},{"kind":"timer","op":"start","timer":"settle"}],"a11y":{"label":"Push"}}}},{"op":"igraph.listener.add","input":{"entityId":"prop-5d7f","listener":{"input":{"kind":"timer","timer":"settle"},"when":"abs(param.vx) > 0.4","actions":[{"kind":"set","param":"vx","value":"param.vx * 0.9"}],"a11y":{"label":"Settle"}}}}]}`
5. Validate, then play it as a viewer: a look draws graphs at rest.
   `read {"calls":[{"op":"igraph.validate","input":{"entityId":"prop-5d7f"}}]}`
   `look {"op":"probe.open","input":{"sceneId":"scene-1000"}}`
   `look {"op":"probe.fire","input":{"probeId":"0199d000-0000-7000-8000-000000000001","input":{"kind":"click","entity":"prop-5d7f"}}}`
   `look {"op":"probe.step","input":{"probeId":"0199d000-0000-7000-8000-000000000001","ms":2000}}`
   `look {"op":"probe.capture","input":{"probeId":"0199d000-0000-7000-8000-000000000001"}}`

Verify "Pushed, it cuts into nothing" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Pushed, it cuts into nothing","check":{"kind":"interactionPath","inputs":[{"kind":"click","entity":"prop-5d7f"}],"untilMs":6000,"expect":{"noPenetration":{"ids":["prop-5d7f"]}}}}]}`

Look: probe.capture before and after a tap.

Pitfalls:

- Keys, strips and generators play fixed: never bake what the viewer changes.
- Speeds are ambient: judge the motion by where things are (probe.capture, an interactionPath check).
- A tweened speed reaches its clock only when it lands.

The current text: read_guide "reactive-motion".
