# JAMI for Claude Code

Design 3D scenes in JAMI from Claude Code: JAMI's MCP server, and skills that teach its way of working — measure, then render.

Generated from JAMI's guides and conventions for Design Interface 1.16.0. Do not edit
these files: they are built from JAMI's sources, and the next release builds them again.

## What it adds

- **The MCP server `jami`** (`.mcp.json`): JAMI's Design Interface over HTTP, at
  `https://jami.live/api/design/mcp`, or at the address `JAMI_MCP_URL` names when it is set. The plugin
  holds no token: the first time, Claude Code sends you to JAMI to sign in and consent (OAuth).
- **Skills** that teach JAMI's way of working, loaded when a request needs them:

  - `jami-3d-design`: measure, then render: the workflow, which op answers which question, the conventions
  - `jami-terrain-walk`: Walk a loop over real ground; A figure of props that walks
  - `jami-follow-camera`: Cameras that follow a walk
  - `jami-reference-match`: Match a model to its reference sheet
  - `jami-verify-report`: Verify, then report
  - `jami-model-from-reference`: Model from a reference, coarse to fine
  - `jami-animate-character`: Animate a character, pose by pose
  - `jami-export-animation`: Export an animation

## Using it

1. Add the marketplace that publishes it, then install it: `/plugin install jami3d@jami3d`.
2. For a JAMI other than the default, set `JAMI_MCP_URL` to its MCP address (the one that
   ends in `/api/design/mcp`) before you start Claude Code.
3. Type `/mcp`, choose `jami`, and sign in to JAMI in the browser.

You need a JAMI account with Design AI access. What the app may do is what you tick on JAMI's
consent page, and you can disconnect it in JAMI at any time.

## The skills are a summary

Each skill was written for one release. JAMI's guides hold the current text: the skills name the
guide to read (`read_guide`), and JAMI's own instructions come with the server.
