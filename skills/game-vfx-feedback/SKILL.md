---
name: game-vfx-feedback
description: Visual feedback for game actions ("juice"): particle bursts, ripples, floating icons and numbers, sparkles for rare results, and screen-level cues, all kept cheap. Use when adding feedback to a reward, hit, purchase, or state change, or when a game feels flat.
---

# Game VFX and feedback

## Pattern
- Every player action gets at least two feedback channels: motion (squash, flight), and color or icon (particles, floater).
- Rarity scales the effect: common = small burst; rare = more particles, a gold star burst, and a larger ripple.
- Floating feedback shows an icon first, then a short number. No sentences.
- Pool or cap arrays: remove dead items each frame, cap particle count (e.g. 200) to avoid slowdowns.

## Implementation
- Particles: `{x, y, vx, vy, life, color, star}` with gravity `vy += g * dt`, life decreasing by `dt / lifetime`.
- Ripples: ellipses with `ry = rx * 0.3`, radius growing, alpha fading.
- Floaters: rise about 30 px per second, fade over about 1.2 s.
- Use palette colors only, and 2x2 pixel squares for particles to match pixel art.

## Feedback table
- Success: burst in the object's rarity color
- Failure: small red cross icon
- Full storage: bag icon
- Purchase: gold burst at the upgraded object
- Unlock: green-and-gold burst at the new area
