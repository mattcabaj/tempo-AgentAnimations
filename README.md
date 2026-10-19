# Skedulo Tempo: Agent Animations

**Version v1.0** · see `CHANGELOG.md` for what changed and integration notes.

For the Skedulo dev team to confirm the Tempo agent-state animations
render and loop correctly in-platform.

## What's inside
- `CHANGELOG.md`: what changed in each version, with integration notes.
- `index.html`: the Tempo Motion System page. Open it in any browser to play the
  exact SVG files in `svg-exports/`, chained into one run. It has a Guides toggle
  (with legend) that shows the frame edge, resting logo and center, plus
  a table mapping each function to its files.
- `svg-exports/`: the 9 production SVG files to drop into the platform (two-tone).
- `svg-exports-mono/`: the same 9 files as a one-colour mark. See Monochrome below.

## The five functions
A **function** is what the agent is doing. Its **states** are the animation
phases: intro, loop, outro.

| Function | Files | How to play |
|---|---|---|
| Reveal | `reveal.svg` | One-shot on first paint, forms from the center, freezes on the logo |
| Thinking | `thinking-intro.svg`, `thinking-loop.svg`, `thinking-outro.svg` | intro on enter, loop while thinking, outro on exit |
| Tool use | `tooluse-intro.svg`, `tooluse-loop.svg`, `tooluse-outro.svg` | intro on enter, loop while running, outro on exit |
| Waiting | `waiting-loop.svg` | Self-looping; starts and ends on the logo |
| Complete | `complete.svg` | One-shot on completion, freezes on the logo |

## One frame for every file
- All 9 files share the same square frame: `viewBox="0 0 880 880"`.
- The resting logo is centered at `440, 440`, and each animation is balanced
  around that point, so files can be swapped in the same container with no jump.
- Nothing is clipped: every file stays inside the frame, and `thinking-loop`
  runs edge to edge. The frame has no built-in margin, so add padding in your layout.
- Open `index.html` and turn on Guides to see all of this per file.

## Integration notes
- Continuous functions (Thinking, Tool use) ship as 3 files: play `intro` once,
  repeat `loop` for the duration, then play `outro` once. Each `intro`'s last
  frame equals its `loop`'s first frame, and each `outro` starts on that same
  frame and ends on the logo, so swapping at any boundary is seamless.
- One-shots (Reveal, Complete) play once and hold on the logo.
- Files are animated SVG (SMIL). They play in browsers; for contexts that don't
  run SMIL, request GIF or MP4.
- Sizing: set the width and height of the whole 880 frame. The resting logo
  fills about 42% of it, so a 48px frame shows a logo about 20px wide.
  Recommended minimum frame: **48px**. Below ~24px use a goo-off variant with
  clean circles.

## Monochrome
- Colour is baked into the two-tone files' animation, so page CSS cannot recolor
  them. For a one-colour mark, use the files in `svg-exports-mono/`: same names,
  same motion, same frame.
- Default colour is navy `#002755`. When the SVG is inlined, set the CSS variable
  `--tempo-color` on the SVG or any parent (for example `--tempo-color: #fff` on
  dark). Used as an `<img>`, the file stays navy.
- The green hand-offs in Thinking and Tool use are invisible in mono, so those
  functions read as motion only.

## Viewing
Open `index.html` in Chrome, Safari, or Firefox. No build step. Everything is
self-contained.

---
Tempo Motion System v0.2.0 · agent-function animation for the Tempo sub-brand.
