---
name: jami-verify-report
description: "In JAMI, through its MCP server: Verify, then report. Use when: Before you say the work is done."
---

# JAMI: Verify, then report

Generated for DI 1.20 — read the guide for the current text: `read_guide "measuring"`. The workflow, the questions and the conventions are in the `jami-3d-design` skill.

## Verify, then report

Before you say the work is done.

Gather: the person's criteria, and the scene's stored checks.

1. Promise first: each criterion as a check; check.kinds gives its fields and limits.
   `read {"calls":[{"op":"check.kinds","input":{"kinds":["motionQuality"]}}]}`
2. Verify: one call judges them all; a row is a worst value, when, its limit.
3. Fix the cause of each failing number; verify again.
4. Look where the verdict points: two or three final pictures, for appearance only.
5. Report each number with its source and accuracyM; unverified is no pass.

Verify "Feet on the ground", "Framed" in one call:
`verify {"sceneId":"scene-1000","inline":[{"name":"Feet on the ground","check":{"kind":"motionQuality","subject":"group-6300"}},{"name":"Framed","check":{"kind":"cameraQuality","subject":"group-6300"}}]}`

Look: The instants the verdict's next names.

Pitfalls:

- A key-fitting error is not a ground contact: say what each number measured.
- problems.list {since: {mine: true}} lists what your own saves touched.

The current text: read_guide "measuring".
