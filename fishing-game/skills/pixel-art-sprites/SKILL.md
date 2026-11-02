---
name: pixel-art-sprites
description: Designing and generating pixel-art game sprites in code or ASCII grids: fixed palettes, grid sizes, outlines, shading bands, sprite sheet frame counts, pivots, and silhouette readability. Use when creating or revising any game art asset, icon, or character, or when a sprite looks muddy or inconsistent.
---

# Pixel art sprites

## Standards
- Fixed palette, 16 colors or fewer, referenced by name. Every sprite, icon and effect uses only these colors. Backgrounds may use palette gradients.
- Native grid sizes: 12x12 to 22x22 for icons and small objects, 16x16 to 32x32 for characters. Pick one size family per game.
- Outline every object with the darkest palette color (ink). Build the outline as a slightly larger shape behind the body fill.
- Shade in bands: top third light, middle base, bottom dark. Add one accent (pattern, highlight pixel) per object.
- Use the same light direction across all sprites.
- Pivot at bottom-center for anything standing on a surface, center for floating items.
- Pad sprites so no pixel touches the edge.

## Sprite sheet frame counts
- Idle loop: 2 to 4 frames (breathing, tail flick), loopable.
- Walk or swim: 4 to 6 frames.
- Action (cast, hit): 4 to 8 frames: anticipation, action, impact, recovery.
- Death or exit: 3 to 5 frames.

## Readability test
- Fill the sprite with solid black. The action or object must still read. If it does not, change the silhouette before adding detail.

## Procedural approach
- Describe shapes as ellipses, rectangles and ASCII rows, then render them. Keep a `P` palette object and a `pxl(g, x, y, key)` helper.
- Variations (species, tiers) come from parameters (colors, pattern type, crown flag), not from copy-pasted grids.
