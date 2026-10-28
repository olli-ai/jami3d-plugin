---
name: jami-creature-walk-talk
description: "In JAMI, through its MCP server: Walk a creature to a mark, and give it a voice. Use when: A creature (a rigged model that is no humanoid) must walk to a mark, make a sound, move by role."
---

# JAMI: Walk a creature to a mark, and give it a voice

Generated for DI 1.18 — read the guide for the current text: `read_guide "creatures"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Walk a creature to a mark, and give it a voice

A creature (a rigged model that is no humanoid) must walk to a mark, make a sound, move by role.

Gather: its model, by its ID; its mark and when it arrives; its sound: an audio file.

1. Read what ingest made of its model: body plan, roles, legs, gaits.
   `read {"calls":[{"op":"cast.rig.suggest","input":{"assetId":"avatar-6a00"}}]}`
2. Cast it as a creature; placing its model then plays that member.
   `edit {"calls":[{"op":"cast.add","input":{"asset":"avatar-6a00","body":"creature"}},{"op":"entity.placeAsset","input":{"sceneId":"scene-1000","asset":"avatar-6a00","at":{"position":[0,0,0]}}}]}`
3. Gaits of procedural samples, at the speeds it suggests.
   `edit {"calls":[{"op":"blendSpace.create","input":{"name":"Gaits","samples":[{"gait":{"pattern":"walk"},"speed":1.1},{"gait":{"pattern":"trot"},"speed":2}]}}]}`
4. Walk it to its mark: footfalls planned, legs planted.
   `edit {"calls":[{"op":"perform.walkTo","input":{"character":"char-6300","to":[0,0,3],"arriveAtMs":4000,"gait":"blend-6d00"}}]}`
5. Its sound, by speaker: its jaw opens with the loudness.
   `edit {"calls":[{"op":"clip.add","input":{"sceneId":"scene-1000","kind":"audio","clip":{"startMs":4500,"endMs":5000,"assetId":"audio-6b00","speaker":{"kind":"cast","castId":"cast-6c00"}}}}]}`
6. Wag its tail by role, on top.
   `edit {"calls":[{"op":"motion.oscillate","input":{"subject":"char-6300","bones":["role:tail"],"axis":[0,1,0],"amplitudeDeg":20,"periodMs":500}}]}`
7. Its feet over the walk, in numbers.
   `read {"calls":[{"op":"pose.contacts","input":{"ids":["char-6300"],"during":{"fromMs":0,"toMs":4000}}}]}`

Verify "Feet planted" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Feet planted","check":{"kind":"footSlide","character":"char-6300","maxCm":3}}]}`

Look: Once the numbers hold: look.contactSheet at a step and at the sound.

Pitfalls:

- A joint turns from its rest, in its own axes: {eulerDeg} or {q}.
- A humanoid bone is refused on a creature: role:<key> or bone:<name>.
- The speaker must stand in the scene, or no jaw opens.

The current text: read_guide "creatures".
