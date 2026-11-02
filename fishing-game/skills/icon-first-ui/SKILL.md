---
name: icon-first-ui
description: Icon-driven game interfaces with minimal text: symbol-based buttons, level pips, cost chips, locked and unlocked states, and collection grids using silhouettes. Use when designing or building game HUDs, menus, shop screens, or any UI that should read at a glance across languages.
---

# Icon-first UI

## Principles
- Each control is an icon with a number at most. Put the action in the icon, not a label.
- Level shows as pips (one small bar per level), max state shows a star.
- Cost is a coin icon plus a short number. Requirements use the icon of the requirement (rod icon with a level number).
- Locked content: show the silhouette or dimmed icon, not a padlock sentence.
- Undiscovered items: silhouette in a muted palette color. Discovered: full color with rarity stars.
- Use one icon family (same grid size, outline, palette) for the whole UI.

## Sizing and touch
- Minimum tap target 44 px on mobile; icons displayed at 28 px inside 44 px buttons.
- Disabled state: reduce opacity to about 0.4, keep the icon visible so the player learns the goal.
- Keep the HUD in corners; the play area stays uncluttered.

## Accessibility
- Pair color with shape: rarity uses stars count, not color alone.
- Give icons `alt=""` only when a nearby number explains them; otherwise add an `aria-label` to the control.
- Keep numbers large and high contrast on dark panels.

## Minimal text rule
- Text is allowed for numbers, one-word feedback when no icon fits, and the document title. Avoid tutorials; teach by feedback (pulsing ring when a tap is needed).
