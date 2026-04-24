# Tech Spec: On-Demand Desktop Open-Item Highlighter

## Objective
Provide a PowerToys utility that temporarily highlights desktop items that are currently open, beginning with desktop folders in V1 and allowing room for later support of common file types. The feature should help users reorganize crowded desktops more efficiently by reducing repeated visual scanning and must operate as an on-demand inspection mode rather than a persistent desktop state. The design should avoid dependence on Windows shell icon overlays.

## Scope

### In scope
- Windows 11 desktop support on x64 and ARM64 systems.
- On-demand activation through a hotkey, tray command, or PowerToys UI entry point.
- Detection of desktop folders that are currently open in File Explorer.
- Temporary highlight rendering aligned to desktop icon positions while the mode is active.
- Immediate removal of all highlights when the mode is turned off.

### Out of scope
- Always-on highlighting or a persistent desktop state indicator.
- Implementation through `IShellIconOverlayIdentifier`.
- Broad detection of every open file type across every Windows application.
- Permanent modification of Explorer icon rendering or desktop icon appearance.
- V1 support for PDFs and Microsoft Office files unless explicitly added in a later phase.

## User flow
1. User activates the mode.
2. PowerToys enumerates current desktop items.
3. PowerToys detects which desktop folders are currently open.
4. PowerToys resolves the current icon positions of those desktop items.
5. PowerToys renders temporary highlights on matching icons.
6. User inspects the desktop and identifies items that are already open.
7. User turns the mode off.
8. All highlights disappear.

## Architecture

| Component | Responsibility |
|---|---|
| Activation controller | Handles hotkey registration, tray command handling, UI invocation, and active/inactive state transitions |
| Desktop indexer | Enumerates desktop items and builds a canonical path map for matching |
| Open-item detector | Identifies relevant Explorer windows and resolves whether they correspond to desktop items currently open |
| Desktop view adapter | Resolves desktop icon positions through supported shell view APIs |
| Highlight renderer | Draws temporary visual markers in a transparent layer above the desktop |
| State coordinator | Runs update checks and redraw logic while the mode is active |

## Detection strategy
The recommended V1 strategy is folder-first detection through open Explorer windows. `EnumWindows` can be used to enumerate top-level windows, after which Explorer-window inspection can determine which folder path each relevant window is currently displaying.

The open-item detector should compare those resolved paths against the indexed desktop contents and produce a set of active desktop paths. This keeps V1 focused on a tractable and high-value detection scenario rather than trying to identify every file type opened by every application.

## Icon position strategy
Desktop icon positions should be obtained through supported shell view access rather than fragile direct manipulation of the desktop list view. This keeps the implementation better aligned with Windows shell expectations and reduces the likelihood of layout-related breakage across desktop configurations.

The desktop view adapter should resolve icon bounds for known desktop items and provide those coordinates to the rendering layer. This allows highlight placement to remain tied to the actual desktop view instead of relying on static assumptions about icon layout.

## Rendering strategy
Rendering should use a temporary transparent visual layer positioned above the desktop while the mode is active. The layer should be lightweight, minimally intrusive, and limited to drawing markers aligned to known icon bounds.

Because this approach does not rely on shell overlay handlers, it avoids competing with common overlay-heavy applications such as sync clients and version-control tools. That makes it a better fit for an on-demand “show me what is open right now” workflow. 

## Candidate visual treatment
A strong candidate for V1 is a partial corner frame: a horizontal line above the icon plus a vertical line on the right side meeting at the top-right corner. This gives a distinct active-state cue without creating a heavy full-box treatment around every highlighted icon.

The visual treatment should remain legible at small icon sizes, across common wallpaper types, and on crowded desktops where many items may appear close together. It should also avoid obscuring icon labels or interfering with normal desktop interaction.

## V1 requirements
- Activation should feel near-instant on a typical Windows 11 desktop.
- The utility should correctly identify desktop folders that are currently open in File Explorer.
- Highlight rendering should remain aligned to desktop icon positions while the mode is active.
- Highlights should update while the mode is active as the open-item state changes.
- Turning the mode off should immediately remove all highlights and restore the normal desktop appearance.
- The feature should not interfere with existing Explorer overlays used by sync or version-control tools.
- The experience should remain usable on crowded desktops, across common icon sizes, DPI scales, and multi-monitor setups.

## Risks
- Transparent desktop-adjacent rendering may be difficult to implement cleanly across all Windows desktop states.
- Desktop icon positions can change because of sorting, alignment, scaling, desktop refreshes, or monitor configuration changes.
- Arbitrary file detection is substantially harder than folder detection and should not be treated as a launch assumption.
- Multi-monitor behavior, click-through handling, and desktop interaction edge cases will require careful QA.

## Acceptance criteria
- User can invoke the feature on demand.
- Open desktop folders are highlighted correctly.
- Highlights appear in the correct desktop positions for the matching items.
- Highlights update appropriately while the mode remains active.
- Highlights disappear immediately when the mode is disabled.
- Existing sync or version-control overlays remain unaffected because shell overlays are not used.
- The desktop remains usable while highlights are visible.
