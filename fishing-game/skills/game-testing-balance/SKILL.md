---
name: game-testing-balance
description: Testing game logic and balance without a browser: pure-function unit tests, seeded simulations of drop rates and income, property checks on save validation, and manual play checklists. Use when verifying economy or probability code, before shipping a balance change, or when a bug only shows after long play.
---

# Game testing and balance

## Structure logic so it is testable
- Keep economy, probability and save code in pure functions that take inputs and return outputs.
- Pass randomness in as a function (`rand: () => number`) so tests can seed it.

## Tests to write
- Cost function: monotonic in level; equals expected values at levels 0, 1, 5, max.
- Weighted pick: over 100000 draws, frequencies match weights within 1 percent.
- Expected value: matches the simulated average within 2 percent.
- Save validation: each malformed case from game-save-state is rejected or repaired.
- Clamping: no level exceeds its max after load.

## Simulation
- Simulate N hours of play with a simple bot (always buy the cheapest affordable upgrade). Record time to each unlock.
- Compare against the pacing targets in idle-game-economy; adjust the config, not the code.

## Manual checklist before release
- [ ] fresh game, first 5 minutes, no dead time
- [ ] reload mid-catch: state recovers, no stuck phase
- [ ] hide tab for 10 minutes: offline gain is capped and shown
- [ ] corrupt the save in devtools: game loads with defaults
- [ ] resize window: canvas and HUD stay usable
- [ ] long play at max level: no slowdown from arrays growing
