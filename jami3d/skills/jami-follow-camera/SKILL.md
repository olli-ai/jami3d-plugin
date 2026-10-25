---
name: jami-follow-camera
description: "In JAMI, through its MCP server: Cameras that follow a walk. Use when: A subject walks a route and the cameras must keep it framed, cutting where it turns back."
---

# JAMI: Cameras that follow a walk

Generated for DI 1.16 — read the guide for the current text: `read_guide "playbook-follow-camera"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Cameras that follow a walk

A subject walks a route and the cameras must keep it framed, cutting where it turns back.

Gather: the subject (the group that moves); its span (fromMs, toMs), or the whole scene; how far behind and ahead the cameras ride.

1. Chase it: two trail cameras, behind and ahead, cut where it turns back; the answer lists the shots, cuts and any gap.
   `edit {"calls":[{"op":"camera.chase","input":{"subject":"group-6300","aheadM":4.5}}]}`
2. Where it lists a gap, find a fixed eye over that stretch.
   `read {"calls":[{"op":"camera.findViewpoint","input":{"sceneId":"scene-1000","subjectIds":["group-6300"],"during":{"fromMs":117000,"toMs":121000},"fixed":true}}]}`
3. Chase again with that eye as a static over the stretch.
   `edit {"calls":[{"op":"camera.chase","input":{"subject":"group-6300","aheadM":4.5,"statics":[{"fromMs":117000,"toMs":121000,"p":[2.4,1.8,-6.5]}]}}]}`
4. Verify the cameras; fix what fails and verify again.

Verify "The cameras keep it framed and clear" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"The cameras keep it framed and clear","check":{"kind":"cameraQuality","subject":"group-6300"}}]}`

Look: One final picture at each cut verify names, and one inside a gap's stretch.

Pitfalls:

- Never key a follow camera by hand: the chase solves its keys.
- An eye inside a canopy or below the ground fails as inside or belowGround: move it.
- On an open mesh an eye's inside cannot be told (unverified, openMesh): say so; skip: ["inside"] judges the rest.
- No shot under 1,500 ms (shotLength).

The current text: read_guide "playbook-follow-camera".
