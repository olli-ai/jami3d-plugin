---
name: jami-terrain-walk
description: "In JAMI, through its MCP server: Walk a loop over real ground. A figure of props that walks. Use when: A figure walks a route over measured ground, often a loop. A figure built from props on pivots (no skinned bones) must walk with its feet planted."
---

# JAMI: Walk a loop over real ground; A figure of props that walks

Generated for DI 1.13 — read the guide for the current text: `read_guide "playbook-terrain-walk"`, `read_guide "playbook-prop-rig-walk"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Walk a loop over real ground

A figure walks a route over measured ground, often a loop.

Gather: the figure (the group that travels) and its feet; the waypoints in order: anchors, landmarks or points; the pace (paceMps) and the step cycle (cycleMs).

1. Measure the ground: what measures it and how well, its named places, where the figure fits.
   `read {"calls":[{"op":"space.terrain","input":{"sceneId":"scene-1000"}},{"op":"space.landmarks","input":{"sceneId":"scene-1000"}},{"op":"space.regions","input":{"sceneId":"scene-1000","agentFrom":"group-6300"}}]}`
2. Plan the route through the waypoints over the real ground, closed for a loop: its length, worst step and a planId.
   `read {"calls":[{"op":"route.plan","input":{"sceneId":"scene-1000","waypoints":[{"entity":"group-6300"},{"entity":"anchor-7a00"},{"entity":"anchor-7a01"}],"closed":true,"lanes":{"side":"right","offsetM":0.3},"uTurnRadiusM":3,"offsetM":0.02,"agentFrom":"group-6300"}}]}`
3. Make it and walk it in one edit: the route from its planId, the figure bound to it in whole laps, a gait timed from the follow.
   `edit {"calls":[{"op":"route.create","input":{"planId":"staged-4f1c0a9e2b7d3c58","name":"Walking loop"}},{"op":"motion.followPath","input":{"ids":["group-6300"],"curveId":{"$result":"0/output/curveId"},"paceMps":0.84,"cycleMs":600,"until":"sceneEnd","sceneLength":"extend","carrier":"newParent"}},{"op":"motion.walkCycle","input":{"subject":"group-6300","timing":{"speedFromId":"group-6300"}}}]}`
4. Verify the walk, its feet as contacts; fix what fails (a step, a gap, the seam).

Verify "The walk keeps to the ground and loops" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The walk keeps to the ground and loops","check":{"kind":"motionQuality","subject":"group-6300","contactIds":["prop-6310","prop-6311"],"cyclic":true,"limits":{"slide":0.05}}}]}`

Look: Two or three look.view {quality: "final"} at the instants verify names.

Pitfalls:

- A canopy is not the ground; in a scan, neither is y = 0.
- cyclic judges the whole scene as one lap: bind until "sceneEnd" with sceneLength "extend".
- Never type a walk's keys: the follow and the walk cycle write them.
- Without foot IK a foot slides at turns, dips on slopes: widen turns, lift the route 2 cm, judge slide at 0.05 m.

The current text: read_guide "playbook-terrain-walk".

## A figure of props that walks

A figure built from props on pivots (no skinned bones) must walk with its feet planted.

Gather: the figure's group; under it a body group that dips, holding the torso and the legs; the legs: groups that swing at their pivots, a foot under each; the path it follows: a planned route or a curve.

1. Read the figure in numbers: its parts with sizes and sides, which touch, cross or float.
   `read {"calls":[{"op":"model.sheet","input":{"sceneId":"scene-1000","ids":["group-6300"]}}]}`
2. Bind it to its path first, then give it a gait: legs on pivots and a body that dips, timed from the follow.
   `edit {"calls":[{"op":"motion.walkCycle","input":{"subject":"group-6300","rig":{"kind":"pivots","limbs":[{"entityId":"group-6320","role":"leg","side":"left"},{"entityId":"group-6321","role":"leg","side":"right"}],"bodyId":"group-6330"},"timing":{"speedFromId":"group-6300","cycleMs":600}}}]}`
3. Verify the feet: no slide while planted, no gap to the ground.

Verify "The feet stay planted" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The feet stay planted","check":{"kind":"motionQuality","subject":"group-6300","contactIds":["prop-6310","prop-6311"]}}]}`

Look: A side picture at a planted step verify names.

Pitfalls:

- A knee-less leg's swing glides over the ground: slide is judged only while a foot is planted.
- The walk cycle takes its pace from the follow: bind the path before the gait.
- A stride (pace × cycle) longer than the legs reach slides the feet: shorten the cycle.
- An open path eases in and out (rampMs 400) under a gait of one pace: bind it with rampMs 0.
- A leg beside the body, not under it, is refused: the body dips and carries the legs.
- Sides are the figure's own: its left is +X when it faces +Z.

The current text: read_guide "playbook-prop-rig-walk".
