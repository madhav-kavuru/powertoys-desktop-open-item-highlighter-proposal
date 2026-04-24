# Technical Architecture Memo: On-Demand Desktop Open-Item Highlighter

## Overview
This memo outlines a non-overlay implementation approach for an on-demand PowerToys utility that temporarily highlights open desktop items. The design avoids shell overlay handlers and instead combines desktop-item indexing, open-window detection, desktop icon position lookup, and a temporary rendering layer.

The goal of the architecture is to support a lightweight inspection mode that can identify open desktop items without permanently changing Explorer icon behavior or competing with existing overlay-based tools.

## System components

### Activation controller
The activation controller manages how the feature is invoked and dismissed. It owns hotkey registration, tray command handling, optional PowerToys UI entry points, and the active/inactive state of the mode.

### Desktop indexer
The desktop indexer enumerates items physically present on the user’s desktop and builds a canonical path map for matching. This includes folders, files, and shortcuts that may need to be checked against the currently open-item set.

### Open-item detector
The open-item detector identifies relevant windows and determines whether they correspond to desktop items that are currently open. In V1, this logic should remain focused on desktop folders opened in File Explorer rather than attempting to identify every file type opened by every application.

### Desktop view adapter
The desktop view adapter resolves the current visual position of desktop items by using supported shell-view access. Its role is to map desktop items to icon bounds so the renderer can place highlights accurately even when icon layout changes.

### Highlight renderer
The highlight renderer creates and maintains the temporary visual layer used to mark open items. It should draw lightweight visual indicators above the desktop without interfering with normal icon interaction or creating a persistent visual state.

### State coordinator
The state coordinator manages refresh timing while the mode is active. It determines when to re-check open items, when to refresh desktop layout information, and when redraw operations are necessary.

## Data flow
1. The activation controller receives an enable request.
2. The desktop indexer builds or refreshes the current desktop item map.
3. The open-item detector computes the set of desktop items that are currently open.
4. The desktop view adapter resolves icon positions for the indexed desktop items.
5. The highlight renderer draws markers for the subset of items that are currently open.
6. While the mode is active, the state coordinator repeats detection and redraw checks as needed.
7. The activation controller receives a disable request.
8. The renderer is destroyed and temporary state is cleared.

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

- Keep V1 focused on desktop folders first.
- Prefer supported shell APIs for desktop item and position handling.
- Keep the renderer isolated so failures do not corrupt desktop state.
- Treat support for PDFs, Office files, and other non-folder item types as later extensions rather than launch requirements.
- Optimize for correctness, low visual overhead, and safe dismissal of the temporary rendering layer.

