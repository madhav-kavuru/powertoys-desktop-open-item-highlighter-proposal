# Feature request: On-demand desktop open-item highlighter

## Summary
Propose a PowerToys utility that temporarily highlights desktop icons whose corresponding folders, and later possibly certain files, are currently open. The feature would be **on-demand only**: the user activates it with a hotkey, tray toggle, or command, the desktop briefly shows which desktop items are active, and the markers disappear when the mode is turned off.

## Problem
Some users treat the Windows desktop as a live workspace with dozens of active project folders, shortcuts, and files. When several Explorer windows are already open, there is no easy desktop-level way to see which desktop items are currently active, which can lead to repeated visual scanning and accidental duplicate opening.

This seems especially relevant for:
- users with crowded desktops,
- multi-project workflows,
- large or high-resolution displays with many small icons,
- and users who want a quick visual audit rather than a permanent status indicator.

## Proposed solution
Instead of making this a persistent always-on state, implement it as an **on-demand temporary highlight mode**:
- User invokes a hotkey, tray toggle, or PowerToys command.
- PowerToys detects which desktop folders are currently open in File Explorer.
- PowerToys resolves where those desktop icons are located.
- PowerToys draws temporary visual markers above those desktop icons using a separate rendering layer.
- When the user turns the mode off, the desktop returns to its normal appearance.

## Why avoid shell overlays
A persistent overlay-based design seems intuitive at first, but Windows shell icon overlays are a constrained mechanism, only one overlay can appear per icon, and common apps such as OneDrive, Dropbox, Box, and Tortoise tools already rely heavily on that system.

Because of that, an overlay-driven implementation would likely conflict with real-world user setups and fail inconsistently on machines that already use sync or version-control overlays.

This proposal therefore avoids the shell icon overlay approach entirely and instead uses a temporary rendering layer that is shown only when requested.

## Suggested V1 scope
- Windows 11 support.
- On-demand toggle only, no always-on mode.
- Folder-first detection in File Explorer.
- Temporary visual markers drawn independently of shell overlays.
- Automatic cleanup when the mode is turned off.

## Why this seems like a PowerToys fit
This feels aligned with the PowerToys model of optional, productivity-oriented utilities for power users rather than broad shell redesign. It appears most useful for a specific workflow niche, but that is also true of many existing PowerToys modules.

## Candidate visual treatment
A possible visual treatment is a partial corner frame rather than a full rectangle: for example, a horizontal line above the icon plus a vertical line on the right side meeting at the top-right corner. That may give a clear “active” signal without making the desktop feel overly boxed in.

## Supporting docs
Prepared supporting Markdown docs include:
- Product overview
- Tech spec
- Technical architecture memo
- QA test plan
- UX design note
- Alternatives and tradeoffs
- Implementation phases

If this seems directionally reasonable, those documents can be linked in follow-up or added directly in this issue.
