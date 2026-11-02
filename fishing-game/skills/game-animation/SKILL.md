---
name: game-animation
description: Animation principles and code patterns for 2D game objects: anticipation, squash and stretch, follow-through with springs, eased arcs, and looping idle motion. Use when animating a throw, cast, catch, bounce, flight path, or any moving object that should feel physical.
---

# Game animation

## Principles in code
- Anticipation: before a big move, play a short reverse pose (e.g. rod pulled back 0.16 s before the cast).
- Squash and stretch: scale x and y in opposite directions by a small factor (about 15 to 25 percent), keeping area roughly constant. Use it on impacts (landing, bobber splash) and fast motion.
- Follow-through: drive secondary parts (rod tip, hair, tails) with a damped spring toward a target: `v += (target - x) * k * dt - v * damping * dt`. Tune k around 100 to 200 and damping so there is one small overshoot.
- Ease in and out: flight paths use `e = p*p*(3-2p)` (smoothstep), not linear interpolation.
- Arcs: move on parabolic or sine-lifted paths, e.g. `y = lerp(y0, y1, e) - sin(pi*p) * height`.
- Secondary rotation: tie a small angle to the arc (e.g. `-sin(pi*p) * 0.4`) so the object tilts while flying.

## Loops
- Idle: derive a frame index from time: `Math.floor(t * fps) % frames`. Use slow rates for breathing (about 1 to 2 fps) and faster for tails (about 6 fps).
- Bob: `Math.sin(t * speed) * amplitude`, amplitude 1 to 3 px for water and boats.

## Timing guide (seconds)
- Anticipation 0.12 to 0.2
- Action 0.2 to 0.4
- Flight of a caught object 0.7 to 1.0
- Impact squash decay 0.12 to 0.2
