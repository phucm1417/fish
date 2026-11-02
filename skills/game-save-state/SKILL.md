---
name: game-save-state
description: Saving and restoring browser game state safely: versioned keys, schema validation, clamping values to legal ranges, error-tolerant storage access, periodic and on-exit saves, and migrations. Use when adding persistence, changing saved fields, or handling corrupted or old save data.
---

# Game save state

## Rules
- Use a versioned key (e.g. `game_v2`). Bump the version when the shape changes incompatibly, and write a migration instead of silently dropping data.
- Wrap `localStorage` access in try/catch. Storage may be disabled or full; the game keeps running.
- Validate before trusting: check types of every field the game reads; reject the whole save if the core fields are wrong.
- Clamp numbers to legal ranges (levels between min and max, coins non-negative), and filter arrays of items to well-formed entries.
- Build the in-memory state from defaults, then overlay the validated save, so new fields get defaults automatically.
- Save every few seconds and on `pagehide` and `visibilitychange` (hidden).
- Store a timestamp `t` for offline calculations.

## Do not
- Do not store derived values (income rates, totals) that can be recomputed.
- Do not store transient animation state.
- Do not use `eval` or trust a save as code.

## Test cases
- Empty storage
- Invalid JSON
- Wrong types in one field
- Levels above max
- Items with missing fields
- Timestamp in the future
