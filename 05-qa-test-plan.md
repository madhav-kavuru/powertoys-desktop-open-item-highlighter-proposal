# QA Test Plan: On-Demand Desktop Open-Item Highlighter

## Objective
Validate that the utility correctly highlights open desktop items on demand, remains visually useful on crowded desktops, and does not interfere with normal desktop interaction or third-party sync overlays.

## Test environments
- Windows 11 current stable build.
- Single-monitor and multi-monitor setups.
- 100%, 125%, 150%, and 200% scaling.
- Small, medium, and large desktop icon sizes.
- Systems with OneDrive and at least one Tortoise-style tool installed.

## Core test areas
### Functional
- Toggle on shows markers.
- Toggle off removes markers.
- Open desktop folders are detected accurately.
- Closed folders are no longer highlighted.

### Crowded desktop
- 50 icons.
- 75 icons.
- 100+ icons.
- Mixed folders, files, and shortcuts.

### Visual
- Busy wallpaper.
- Solid wallpaper.
- Light and dark themes.
- High DPI and small icons.

### Stability
- Rapid toggle on/off.
- Explorer restart.
- Desktop refresh.
- Rearranging icons while mode is active.

## Example pass criteria
- No persistent marker remains after disable.
- OneDrive or Tortoise overlays still appear normally when the mode is inactive.
- The desktop remains selectable and usable while the mode is active.
