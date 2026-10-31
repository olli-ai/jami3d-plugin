---
name: jami-animate-character
description: "In JAMI, through its MCP server: Animate a character, pose by pose. Use when: A humanoid character must act — a gesture, a reaction, a beat of a dance — keyed in joint degrees."
---

# JAMI: Animate a character, pose by pose

Generated for DI 1.20 — read the guide for the current text: `read_guide "posing"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Animate a character, pose by pose

A humanoid character must act — a gesture, a reaction, a beat of a dance — keyed in joint degrees.

Gather: the character, by its ID; each pose in words and when: which joints, how far, at which ms.

1. Read its pose where the move starts, in the angles pose.set takes.
   `read {"calls":[{"op":"pose.get","input":{"ids":["char-6300"],"atMs":0}}]}`
2. Block the extremes in one call, stepped; a pose that holds says holdMs.
   `edit {"calls":[{"op":"pose.block","input":{"subject":"char-6300","poses":[{"atMs":400,"joints":{"torso":[10,0,0],"rightUpperArm":[90,60,-30]}},{"atMs":1000,"joints":{"rightUpperArm":[90,140,-60],"rightLowerArm":[30,0,0]},"holdMs":400}],"interpolation":"stepped"}}]}`
3. Read the extremes back; fix a joint with pose.set at its instant.
   `read {"calls":[{"op":"pose.get","input":{"ids":["char-6300"],"atMs":1000,"bones":["arms"]}}]}`
4. A breakdown where a move must arc; then spline every key.
   `edit {"calls":[{"op":"pose.tween","input":{"subject":"char-6300","atMs":700,"mode":"breakdown","factor":0.4}},{"op":"motion.interpolation","input":{"subject":"char-6300","mode":"spline"}}]}`
5. Anticipate the raise, overshoot and settle it; the forearm and hand trail.
   `edit {"calls":[{"op":"motion.anticipate","input":{"subject":"char-6300","atMs":1000}},{"op":"motion.settle","input":{"subject":"char-6300","atMs":1000}},{"op":"motion.overlap","input":{"subject":"char-6300","chains":[{"bones":["rightUpperArm","rightLowerArm","rightHand"],"delayMs":40}]}}]}`
6. Plant the feet where they touch, over the move.
   `edit {"calls":[{"op":"pose.plant","input":{"subject":"char-6300","detect":"auto","during":{"fromMs":0,"toMs":2000}}}]}`
7. The hand's world position at the instants that matter, in numbers.
   `read {"calls":[{"op":"pose.sample","input":{"ids":["char-6300"],"bones":["rightHand"],"times":[400,1000,1400]}}]}`

Verify "In its limits", "Feet planted", "Arm raised" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"In its limits","check":{"kind":"jointLimits","subject":"char-6300"}},{"name":"Feet planted","check":{"kind":"footSlide","character":"char-6300","maxCm":2,"during":{"fromMs":0,"toMs":2000}}},{"name":"Arm raised","check":{"kind":"poseReached","entityId":"char-6300","atMs":1000,"joints":{"rightUpperArm":[90,140,-60]},"toleranceM":0.01,"toleranceDeg":5}}]}`

Look: Once the numbers hold: look.motionSheet {keys: true, trails: ["rightHand"]}.

Pitfalls:

- All zeros is standing at attention, not the T-pose.
- A right joint takes its left twin's angles, mirrored.
- Outside its performance strip, its idles and walks show.
- Past a limit it keys and warns jointLimit; clamp: true holds it.

The current text: read_guide "posing".
