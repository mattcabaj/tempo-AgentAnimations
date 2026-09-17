# Skedulo Tempo — Agent Animations (Test Batch)

Test batch for the Skedulo dev team to confirm the Tempo agent-state animations
render and loop correctly in-platform.

## What's inside
- `index.html` — the animation gallery. Open it in any browser to see every
  animation running. This is the live reference for how each SVG should look and move.
- `svg-exports/` — the 9 production SVG files to drop into the platform.

## The five functions
A **function** is what the agent is doing. Its **states** are the animation
phases: intro, loop, outro.

| Function | Files | How to play |
|---|---|---|
| Reveal | `reveal.svg` | One-shot on first paint, freezes on the logo |
| Thinking | `thinking-intro.svg`, `thinking-loop.svg`, `thinking-outro.svg` | intro on enter → loop while thinking → outro on exit |
| Tool use | `tooluse-intro.svg`, `tooluse-loop.svg`, `tooluse-outro.svg` | intro on enter → loop while running → outro on exit |
| Waiting | `waiting-loop.svg` | Self-looping; starts and ends on the logo |
| Complete | `complete.svg` | One-shot on completion, freezes on the logo |

## Integration notes
- Continuous functions (Thinking, Tool use) ship as 3 files: play `intro` once,
  repeat `loop` for the duration, then play `outro` once. Each `intro`'s last
  frame equals its `loop`'s first frame, so swapping at the boundary is seamless.
- One-shots (Reveal, Complete) play once and hold on the logo.
- Files are animated SVG (SMIL). They play in browsers; for contexts that don't
  run SMIL, request GIF or MP4.
- Recommended minimum size: **48px**. The metaball blend needs room to read;
  below ~24px use a goo-off variant with clean circles.

## Viewing
Open `index.html` in Chrome, Safari, or Firefox. No build step — everything is
self-contained.

---
Tempo Motion System · procedural agent-function animation for the Tempo sub-brand.
