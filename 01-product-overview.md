# Product Overview: On-Demand Desktop Open-Item Highlighter

## Overview
On-Demand Desktop Open-Item Highlighter is a proposed PowerToys utility that helps users quickly locate which desktop items are already open by temporarily highlighting them only when requested. The feature is intended for people who use the desktop as an active workspace rather than a minimal drop zone.

## User problem
On crowded desktops, it is difficult to tell at a glance which project folders are already open in Explorer or which important items are already in use. Windows does not currently provide a temporary "show me what is active on the desktop right now" mode for this workflow.  The ultimate objective is to make reorganizing the desktop easier on crowded, icon-heavy workspaces. By eventually highlighting the most common items besides folders—such as PDFs and Microsoft Office files (Word documents, spreadsheets, and PowerPoint presentations)—the utility can significantly reduce the cognitive and visual effort required to clean up. Users no longer have to repeatedly scan the desktop in search of each item of interest and remember where everything lives; instead, they can invoke the mode, see what is already open, and reorganize with less guesswork.

## Target users
- Power users who keep 50–100+ items on the desktop.
- Users who work across multiple open project folders.
- Users with large or high-resolution displays where scanning many small icons is tiring.
- Users who want a quick visual audit rather than a permanent desktop state.

## Core concept
The utility remains invisible until the user asks for it. After activation, it briefly highlights desktop items that are currently open and keeps those highlights updated while the mode is active. When the mode is turned off, the desktop returns to its prior appearance.

## Product principles
- On-demand, not always-on.
- No dependency on shell overlay slots.
- Clear benefit on crowded desktops.
- Minimal visual noise.
- Fast to invoke, fast to dismiss.

## Why not shell overlays
Shell overlays are a poor fit for this use case because they are constrained, only one overlay can appear per icon, and real systems often already use them for sync or version-control status. An independent temporary rendering layer is better aligned with the desired "show me now, then go away" workflow.
