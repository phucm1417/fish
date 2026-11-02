---
name: canvas-2d-rendering
description: Practical Canvas 2D rendering for games: pixel-crisp sprite blitting, sprite caches built from offscreen canvases, bottom-center pivots, layered draw order, and responsive scaling. Use when drawing sprites, scenes, or effects on a canvas, or when images look blurry or jitter.
---

# Canvas 2D rendering

## Rules
- Set `ctx.imageSmoothingEnabled = false` and CSS `image-rendering: pixelated` on the canvas.
- Build each sprite once into an offscreen canvas and cache it by key. Never redraw a sprite procedurally per frame.
- Blit with a helper that: saves state, rounds x/y to whole pixels, applies rotate and scale, draws with a bottom-center pivot, restores state.
- Draw in a fixed layer order: sky, far background, water, submerged objects, surface effects, world objects, rod and line, UI-like overlays (rings, pulses), particles, floating text.
- Fixed logical resolution (e.g. 800x450) scaled by CSS width. Do not resize the backing store on every frame.
- Use `globalAlpha` for fades and reset it to 1 after each block.
- Use `destination-out` to cut shapes (crescents, notches) on offscreen sprites, then restore `source-over`.

## Pitfalls
- Forgetting `save()/restore()` leaks transforms into later draws.
- Mixing `fillRect(x,y,1,1)` pixel-building with scaled drawing produces seams; build sprites at native size and scale once at blit time.
