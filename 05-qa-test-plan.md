# QA Test Plan: On-Demand Desktop Open-Item Highlighter

## Objective
This test plan validates that the utility correctly highlights open desktop items on demand, remains visually useful on crowded desktops, and does not interfere with normal desktop interaction or other desktop overlay use cases.

The QA goal is not only to confirm correctness, but also to verify that the feature remains practical, lightweight, and safe across realistic desktop conditions.

## Test environments
Testing should cover a representative range of Windows desktop configurations, including:

- Windows 11 current stable build.
- x64 and ARM64 systems where available.
- Single-monitor and multi-monitor setups.
- 100%, 125%, 150%, and 200% display scaling.
- Small, medium, and large desktop icon sizes.
- Light and dark Windows themes.
- Systems with OneDrive and at least one Tortoise-style tool installed.

## Core test areas

### Functional behavior
The feature should be validated for basic correctness and expected state transitions.

- Turning the mode on should display markers for matching desktop items.
- Turning the mode off should remove all markers immediately.
- Desktop folders that are currently open in File Explorer should be detected accurately.
- Items that are no longer open should no longer remain highlighted.
- Repeated activation and dismissal should not leave behind stale UI state.

### Crowded desktop scenarios
The feature should be tested under realistic icon-heavy conditions where its value is highest.

- Desktop layouts with 50 icons.
- Desktop layouts with 75 icons.
- Desktop layouts with 100 or more icons.
- Mixed desktops containing folders, files, and shortcuts.
- Layouts where icons are densely packed or visually similar.

### Visual clarity
The feature should remain understandable and useful across a range of desktop presentation conditions.

- Busy wallpapers.
- Simple or solid-color wallpapers.
- Light and dark themes.
- High DPI environments.
- Small icon layouts where marker visibility is more challenging.

### Stability and state changes
The feature should behave predictably across common desktop and Explorer changes.

- Rapid toggle on and off.
- Explorer restart while the mode is active.
- Desktop refresh events.
- Rearranging icons while the mode is active.
- Changes in scaling, monitor arrangement, or desktop layout during use.

## Example pass criteria
- No persistent marker remains after the mode is disabled.
- Open desktop folders are highlighted in the correct icon positions.
- Highlight updates remain accurate while the mode is active.
- The desktop remains selectable and usable while highlights are visible.
- Existing sync and version-control overlays still appear normally when the mode is inactive.
- The feature remains understandable and visually usable on crowded desktops.
