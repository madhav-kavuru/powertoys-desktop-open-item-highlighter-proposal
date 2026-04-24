# Tech Spec: On-Demand Desktop Open-Item Highlighter

## Objective
Provide a PowerToys utility that temporarily highlights desktop icons whose corresponding folders, and later optionally supported files, are currently open, so that users can more easily reorganize crowded desktops without repeatedly scanning for items of interest. The feature must work as an on-demand inspection mode and must not depend on Windows shell icon overlays.

## Scope
### In scope
- Windows 11 support.
- On-demand activation via hotkey, tray command, or PowerToys UI.
- Detection of desktop folders currently open in File Explorer.
- Temporary highlight rendering above desktop icon positions.
- Removal of all markers when mode is disabled.

### Out of scope
- Always-on highlighting.
- `IShellIconOverlayIdentifier` implementation.
- Broad support for every open file in every application.
- Permanent modifications to Explorer icon rendering.

## User flow
1. User activates the mode.
2. PowerToys enumerates current desktop items.
3. PowerToys detects which desktop folders are open.
4. PowerToys resolves their current icon positions.
5. PowerToys draws temporary markers on those icons.
6. User turns the mode off.
7. All markers disappear.

## Architecture
| Component | Responsibility |
|---|---|
| Activation controller | Hotkey, command, tray toggle, settings state |
| Desktop indexer | Enumerates desktop items and builds canonical path map |
| Open-item detector | Finds open Explorer windows and matches paths |
| Desktop view adapter | Resolves icon positions through shell view APIs |
| Highlight renderer | Draws temporary markers in a transparent layer |
| State coordinator | Runs update loop while mode is active |

## Detection strategy
The recommended V1 strategy is folder-first detection using Explorer windows. `EnumWindows` can enumerate top-level windows, and Explorer-window inspection can then be used to determine which folder path each relevant window currently displays. The open-item detector should compare those paths against the indexed desktop contents and produce a set of active desktop paths.

## Icon position strategy
Desktop icon positions should be obtained through supported shell view access rather than fragile direct manipulation of the desktop list view. Microsoft has documented `IFolderView`-based interaction with desktop items and has specifically reminded developers to use supported shell view APIs for desktop icon handling.

## Rendering strategy
Rendering should use a temporary transparent visual layer positioned above the desktop while the mode is active. The layer should be lightweight, click-through or minimally intrusive, and limited to drawing markers aligned to known icon bounds. Because this approach does not use shell overlay handlers, it avoids competing with common overlay-heavy apps such as sync clients and Tortoise tools.

## Candidate visual treatment
A recommended candidate is a partial corner frame: a horizontal line above the icon plus a vertical line on the right side meeting at the top-right corner. This gives a distinct "active" cue while avoiding a full heavy rectangle around every open icon.

## V1 requirements
- Activation latency should feel near-instant on a normal desktop.
- Highlight updates should occur while the mode is active.
- Turning the mode off must fully restore the desktop appearance.
- No interference with OneDrive-style sync overlays or other existing Explorer overlays.
- The feature should remain usable on crowded desktops, different icon sizes, and common DPI scales.

## Risks
- Transparent desktop-adjacent rendering can be tricky to implement cleanly.
- Desktop icon positions can change with sorting, alignment, scaling, or monitor changes.
- Arbitrary file detection is much harder than folder detection.
- Multi-monitor handling and click-through behavior require careful QA.

## Acceptance criteria
- User can invoke the feature on demand.
- Open desktop folders are highlighted correctly.
- Highlights disappear immediately when the mode is disabled.
- Existing sync or VCS overlays remain unaffected because shell overlays are not used.
- The desktop remains usable while highlights are visible.
