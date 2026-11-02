---
name: game-core-loop
description: Architecture of a browser game's main loop: timestep clamping, update/draw separation, state machines for game phases, and deterministic-enough logic. Use when starting a game, adding a new game phase or mechanic, or debugging stutter, runaway timers, or tab-switch glitches.
---

# Game core loop

## Rules
- One `requestAnimationFrame` loop. Compute `dt` from timestamps and clamp it (e.g. max 0.05 s) so a backgrounded tab never teleports objects.
- Keep three steps separate and in order: `update(dt)` mutates state, `draw()` reads state only, `renderUI()` runs only when a dirty flag is set.
- Model phases as an explicit state machine (`idle -> wait -> bite -> idle`). Every transition lives in one function; no ad-hoc boolean flags.
- Put all randomness behind named functions (`rnd`, `pick`) so tests can stub them.
- Timers are countdowns in seconds that decrement in `update`, never `setTimeout` for gameplay.

## Checklist
- [ ] dt clamped
- [ ] draw has no side effects on game state
- [ ] each phase has one entry and one exit function
- [ ] UI rebuilt on change, not every frame
