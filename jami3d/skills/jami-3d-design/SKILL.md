---
name: jami-3d-design
description: "Designing 3D scenes in JAMI through its MCP server: measure, then render — orient, promise first, measure in numbers, act by intent, verify, look only where the verdict points, report each number with its source. Use when: any task on a JAMI project. At the start of a task, and after a reset or a compacted context. Before you place, move or judge anything: ask in numbers, never from a picture."
---

# Designing in JAMI: measure, then render

Generated for DI 1.13 — read the guide for the current text: `read_guide "measuring"`, `read_guide "conventions"`, `read_guide "connected-apps"`.

## Orient before you change anything

At the start of a task, and after a reset or a compacted context.

Gather: the project (list_projects, or the projectId you were given); the scene and the things the person names, by their IDs.

1. Read where you are: your note, your last changes, what you left open, the promises and their latest results.
   `get_project_overview {"recap":true}`
2. An ID from before a reset may name nothing now: ids.resolve says what it names, or what removed it.
   `read {"calls":[{"op":"ids.resolve","input":{"refs":["prop-5d7f"]}}]}`
3. What is in the scene at an instant, as one digest: the cameras and what they frame, what moves where.
   `read {"calls":[{"op":"scene.describe","input":{"sceneId":"scene-1000","atMs":0}}]}`
4. Then measure before you change anything: read_guide "measuring".

Look: None yet: a picture measures nothing.

Pitfalls:

- Never describe again the ops you learned before a reset: keep their cards.
- A name is not an ID: find gives the ID to send.

The current text: read_guide "connected-apps".

## Measure first

Before you place, move or judge anything: ask in numbers, never from a picture.

Gather: the question, in the person's words; the things it names, by ID; the instant (atMs) or span (during) it is about.

1. Send the op of the question's row (the measuring guide's table) with read; several go in one read.
   `read {"calls":[{"op":"space.heightAt","input":{"sceneId":"scene-1000","points":[[0,-3.75]]}},{"op":"entity.facts","input":{"ids":["group-6300"],"atMs":2000}}]}`
2. Over a span, read how it moves (entity.trajectory), or the check that judges it.
3. Use a number only with its source and accuracyM; unmeasured says what was not read.
4. Report what measured each number. Never report a number you did not measure.

Look: Once the numbers hold: look.view {quality: "final"} at the instants verify names.

Pitfalls:

- In a scan, y = 0 is not the ground: measure it.
- A canopy is not the ground: space.rays reads on through it.
- 8-bit depth is coarse: never read heights from it.

The current text: read_guide "measuring".

## Which op answers which question

One line a question, with the tool to send it with: [questions.md](questions.md). `read_guide "measuring"` holds the whole table, with what each answer gives.

## Conventions

- Lengths are metres, times integer milliseconds from the scene's start (`atMs`); a field ending `Deg` is degrees; rotation channels are radians in the `XYZ` order.
- Y is up. An entity faces its local +Z, a camera looks down its −Z; north (−Z) is the top of a plan. Heading 0° faces +Z, 90° faces +X; +X is the left of a subject facing +Z.
- A named view says where its camera stands: `front` +Z, `back` −Z, `right` +X, `left` −X.
- Rotations are unit quaternions `[x, y, z, w]`, stored within 1e-5 of unit length: send 6 decimals or more. Pictures echo a camera's rotation to 6 decimals with w ≥ 0; camera keys keep w ≥ 0.
- A camera without a lens set has a 36 × 24 mm sensor and a 35 mm lens: vertical FOV = 2·atan(12 / focalMm), 37.85°.
- `perceive.depth` is 8-bit grey (255 the nearest, 32 the farthest, 0 nothing drawn): never measure ground from it.
- One `edit` runs at most 50 calls; a script's batch, 200.
