---
name: idle-game-economy
description: Designing and balancing idle and incremental game economies: exponential upgrade costs, income rates, reward tables with weights, rarity curves, storage caps, and offline progress. Use when tuning costs, drop rates, unlock gates, or passive income, or when progression feels too slow or too fast.
---

# Idle game economy

## Cost curves
- Upgrade cost: `floor(base * growth^level)`. Growth 1.6 to 2.2 for most upgrades.
- Gate new areas with both currency cost and a capability requirement (e.g. rod level), so spending alone does not skip content.
- Cap levels (max 10 to 15) and show a max state.

## Reward tables
- Weight by rarity: `weight = base / (1 + rarity * k)`. Rare entries get a bonus multiplier from a luck upgrade, e.g. `1 + 0.25 * bait`.
- Expected value: `sum(weight * value) / sum(weight)`. Use it for income estimates and offline math, so the numbers agree with live play.
- Keep rare items rare: the top tier should appear about once per several hundred actions at the mid-game rate.

## Rates and pacing
- Automation rate = `1 / cycleTime`. Include the random wait average in cycleTime.
- Target pacing: first upgrade within about 1 minute, first new area within about 15 minutes, late-game area within a few hours.
- Each upgrade should change the experience, not just a number: faster bite, new zone, auto-sell.

## Offline progress
- Store a timestamp on save. On load compute `elapsed` capped (e.g. 2 hours).
- Multiply by 0.5 to 0.6 to reward returning without replacing active play.
- Only grant offline income for mechanics that cannot overflow storage, or cap it.

## Tuning checklist
- [ ] cost curve values written down in one config object
- [ ] expected income matches observed income within 20 percent in a simulation
- [ ] no upgrade is strictly dominated
