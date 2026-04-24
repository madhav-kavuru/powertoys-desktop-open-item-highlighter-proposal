# Product Overview: On-Demand Desktop Open-Item Highlighter

## Overview
On-Demand Desktop Open-Item Highlighter is a proposed PowerToys utility that helps users quickly identify which desktop items are already open by temporarily highlighting them when requested. The feature is intended for people who use the desktop as an active workspace rather than as a minimal drop zone.

## User problem
On crowded desktops, it is difficult to tell at a glance which project folders are already open in File Explorer or which important items are already in use. Windows does not currently provide a temporary “show me what is active on the desktop right now” mode for this workflow.

The ultimate objective is to make reorganizing the desktop easier. By eventually supporting not only folders but also common files such as PDFs and Microsoft Office documents, the utility can reduce the repeated visual scanning and memory burden that crowded desktops create. Instead of repeatedly searching for items of interest and trying to remember their locations, users could invoke the feature, identify what is already open, and reorganize with less guesswork.

## Target users
- Power users who keep large numbers of items on the desktop, often 50–100 or more.
- Users who work across multiple project folders at the same time.
- Users with large or high-resolution displays where scanning many small desktop icons is tiring.
- Users who want a quick visual audit of active items rather than a permanent desktop state indicator.

## Core concept
The utility remains invisible until the user asks for it. Once activated, it temporarily highlights desktop items that are currently open and keeps those highlights updated while the mode is active. When the mode is dismissed, the desktop returns to its prior appearance.

## Product principles
- On-demand rather than always on.
- Focused on reducing clutter and cognitive effort on crowded desktops.
- Minimal visual noise when inactive and lightweight visual guidance when active.
- Fast to invoke, easy to inspect, and quick to dismiss.
- Designed without dependence on shell overlay slots.

## Why not shell overlays
Shell overlays are a poor fit for this use case because they are constrained, only one overlay can appear per icon, and many real systems already use those slots for sync and version-control status indicators. A temporary rendering layer is better aligned with the desired “show me now, then go away” workflow and avoids competing with other desktop overlay use cases.
