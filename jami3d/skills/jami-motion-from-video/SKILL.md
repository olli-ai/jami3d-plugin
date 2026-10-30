---
name: jami-motion-from-video
description: "In JAMI, through its MCP server: Recreate a person's motion from a video. Use when: A humanoid character must move as a person in a video of the project moves."
---

# JAMI: Recreate a person's motion from a video

Generated for DI 1.19 — read the guide for the current text: `read_guide "video-motion"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Recreate a person's motion from a video

A humanoid character must move as a person in a video of the project moves.

Gather: the video, by its ID (the person uploads it in the Studio), and who in it moves; the character, by its ID.

1. Read what the project measured of the video. videoMotionOff: stop, the platform's owner has not turned video motion on for you.
   `read {"calls":[{"op":"video.analyses","input":{"video":"video-7c85"}}]}`
2. Find who is in it, boxes only: a job, alone in its edit.
   `edit {"calls":[{"op":"video.people","input":{"video":"video-7c85"}}]}`
3. Measure one person; running: the same call again. videoConsent: the person confirms it in the Studio.
   `edit {"calls":[{"op":"video.analyze","input":{"video":"video-7c85","person":0}}]}`
4. Read its angles and how sure, before you make anything.
   `read {"calls":[{"op":"video.inspect","input":{"analysis":"video-7c85/3fa2"}}]}`
5. Plan it on the character: its grade, root and keys.
   `edit {"calls":[{"op":"video.recreate.plan","input":{"analysis":"video-7c85/3fa2","subject":"char-6300"}}]}`
6. Store it as a library motion, the default, and send the next it answers: motionLib.add, perform.motion.add.
   `edit {"calls":[{"op":"video.recreate.toMotion","input":{"planId":"staged-4b1f9c2e7a0d5e38","name":"Walk from video"}}]}`
7. Compare the character with the analysis, at the height you planned at.
   `read {"calls":[{"op":"video.compare","input":{"analysis":"video-7c85/3fa2","subject":"char-6300"}}]}`

Verify "Moves as the video" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Moves as the video","check":{"kind":"matchesVideo","subject":"char-6300","analysis":"video-7c85/3fa2"}}]}`

Look: Once the numbers hold: look.videoCompare at the worst instants, four a call at most.

Pitfalls:

- An Action holds about 2 s with hands at medium keys: past that, actionTooLarge; keep the motion.
- A poor grade for a root reason keeps the root in place (rootDefault); asking root apply overrides it.
- Apps see skeletons on blank: frames: true is refused to them (personOnly).

The current text: read_guide "video-motion".
