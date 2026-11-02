---
name: game-design-doc
description: Writing a concise game design document for a small game: pillars, core loop, progression, content tables, feedback goals, and scope. Use when starting a new game, planning a feature, or aligning code and art work with the intended player experience.
---

# Game design doc

## Structure (keep to 1 to 3 pages)
1. Pitch: one sentence describing the player fantasy.
2. Pillars: 3 short rules every decision must satisfy (e.g. "always one more thing to unlock", "icons before words").
3. Core loop: the action the player repeats every 10 to 60 seconds, and what it rewards.
4. Progression: a table of unlocks in order with cost, requirement, and what changes for the player.
5. Content tables: items, enemies, or fish with value, rarity, and where they appear.
6. Feedback goals: what the player should feel on success, failure, and reward.
7. Art and audio direction: palette, grid size, animation list, sound moments.
8. Scope: in, out, and later.

## Writing rules
- Use tables for numbers, short bullets for rules, and avoid prose paragraphs.
- Every number must come from a config object in code. The doc links to the config, not copies of it.
- Mark assumptions explicitly and list open questions at the end.

## Review questions
- Can the player explain the goal after 2 minutes of play?
- Does every unlock change behavior, not only a multiplier?
- Is the core loop shorter than the time between sessions?
