# UX Design Note: On-Demand Desktop Open-Item Highlighter

## UX goal
Provide a fast, low-friction way to answer a single question: “Which desktop items are open right now?” The utility should not create a permanent visual state.

## Interaction model
The utility should support one or more of these activation paths:
- global hotkey,
- tray toggle,
- command palette action,
- optional quick action in PowerToys settings.

The best default experience is:
- activate,
- inspect,
- dismiss.

## Visual behavior
The desktop should look unchanged when the utility is inactive. When active, open desktop items should be marked clearly but lightly enough that the desktop does not feel boxed in or noisy.

## Recommended visual treatment
Use a partial corner frame or similar directional marker instead of a full thick outline. The marker should be visible at small icon sizes and on both simple and busy wallpapers.

## UX constraints
- The utility should not break drag/drop or icon selection.
- The mode should be easy to dismiss.
- The marker should not obscure icon labels.
- It should remain understandable even if many icons are highlighted at once.

## Accessibility considerations
- Keyboard invocation should be supported.
- High-contrast visibility matters.
- Animation, if any, should be subtle and optional.
- The visual language should remain legible across scaling levels.
