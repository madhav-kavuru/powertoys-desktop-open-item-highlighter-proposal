# UX Design Note: On-Demand Desktop Open-Item Highlighter

## UX goal
The goal of the experience is to give users a fast, low-friction way to answer a simple question: which desktop items are open right now? The utility should support quick inspection on crowded desktops without creating a permanent visual state or adding ongoing clutter.

## Interaction model
The utility should support one or more lightweight activation paths, such as a global hotkey, a tray command, a command palette action, or an optional quick action in the PowerToys interface.

The intended default interaction is simple:
- Activate the mode.
- Inspect the desktop.
- Dismiss the mode.

This interaction should feel immediate and easy to repeat whenever the user wants a temporary visual audit of the desktop.

## Visual behavior
When the utility is inactive, the desktop should appear completely unchanged. When the mode is active, open desktop items should be marked clearly enough to stand out, but lightly enough that the desktop does not feel crowded, noisy, or visually overdrawn.

The visual behavior should help the user identify active items quickly without competing with icon labels, wallpapers, or existing desktop elements.

## Recommended visual treatment
A partial corner frame or similar directional marker is a stronger fit than a full heavy outline. It provides a distinct visual cue while avoiding the boxed-in feeling that full rectangular borders can create when many items are highlighted at once.

The marker should remain legible at small icon sizes, across common scaling levels, and on both simple and visually busy wallpapers.

## UX constraints
- The utility should not interfere with normal desktop interaction, including icon selection, drag-and-drop, or right-click actions.
- The mode should be easy to dismiss at any time.
- Visual markers should avoid obscuring icon labels or making text harder to read.
- The interface should remain understandable even when many desktop items are highlighted at once.
- The experience should feel lightweight and temporary rather than persistent or stateful.

## Accessibility considerations
- Keyboard invocation should be supported as a first-class interaction path.
- The visual treatment should remain visible in high-contrast and low-clarity desktop conditions.
- Any animation should be subtle, optional, and nonessential to understanding the highlighted state.
- The visual language should remain legible across common DPI and scaling settings.
- The feature should reduce cognitive effort rather than introduce a new source of visual complexity.
