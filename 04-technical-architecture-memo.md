# Technical Architecture Memo: On-Demand Desktop Open-Item Highlighter

## Overview
This memo describes a non-overlay implementation for a PowerToys utility that temporarily highlights open desktop items on demand. The design avoids `IShellIconOverlayIdentifier` and instead uses desktop-item indexing, open-window detection, shell-view position lookup, and a temporary rendering layer.

## System components
### Activation controller
Owns hotkey registration, tray command handling, and active/inactive state transitions.

### Desktop indexer
Enumerates files, folders, and shortcuts physically present on the user desktop and stores a canonical path map.

### Open-item detector
Enumerates relevant windows and resolves whether they correspond to desktop folders currently open in File Explorer.

### Desktop view adapter
Uses desktop shell view APIs to map desktop items to their current icon coordinates.

### Highlight renderer
Creates and maintains a temporary transparent drawing surface positioned above the desktop.

### State coordinator
Runs update ticks while the mode is active and triggers redraw only when necessary.

## Data flow
1. Activation controller receives On.
2. Desktop indexer builds current desktop path map.
3. Open-item detector builds current open desktop set.
4. Desktop view adapter resolves icon coordinates for desktop items.
5. Highlight renderer draws markers for the open-item subset.
6. State coordinator repeats detection and redraw while active.
7. Activation controller receives Off.
8. Renderer is destroyed and state is cleared.

## Key interfaces
```text
IActivationController
  Enable()
  Disable()
  Toggle()
  IsEnabled() -> bool

IDesktopIndexer
  Refresh()
  GetItems() -> list<DesktopItem>
  ContainsPath(path) -> bool

IOpenItemDetector
  GetOpenDesktopPaths(index) -> set<path>

IDesktopViewAdapter
  ResolveIconRects(items) -> map<path, rect>

IHighlightRenderer
  Show()
  Draw(openPaths, rectMap)
  Hide()
  Destroy()
```

## Pseudocode
```text
Enable():
    index.Refresh()
    openPaths = detector.GetOpenDesktopPaths(index)
    rects = desktopView.ResolveIconRects(index.GetItems())
    renderer.Show()
    renderer.Draw(openPaths, rects)
    StartTimer()

OnTimerTick():
    if not controller.IsEnabled():
        return
    if DesktopChanged():
        index.Refresh()
        rects = desktopView.ResolveIconRects(index.GetItems())
    latest = detector.GetOpenDesktopPaths(index)
    if latest != openPaths or LayoutChanged():
        openPaths = latest
        renderer.Draw(openPaths, rects)

Disable():
    StopTimer()
    renderer.Destroy()
```

## Implementation notes
- Keep V1 folder-first.
- Prefer supported shell APIs for desktop item/position handling.
- Keep renderer isolated so failures do not corrupt desktop state.
- Treat file detection as a later extension rather than a launch requirement.
