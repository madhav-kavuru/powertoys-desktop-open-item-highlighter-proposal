# Alternatives and Tradeoffs

## Overview
This proposal considers three broad implementation directions: shell icon overlays, always-on custom rendering, and on-demand temporary rendering. Each approach can highlight desktop state in some form, but they differ significantly in how well they fit the actual user problem, how much visual noise they create, and how safely they coexist with the existing Windows desktop environment.

The main question is not simply which option is technically possible, but which option best supports quick desktop inspection and easier desktop reorganization.

## Shell icon overlays

### Advantages
- Feels superficially native to Explorer.
- Seems conceptually simple at first glance.
- Reuses an existing visual model that users may already recognize from sync and version-control tools.

### Drawbacks
- Shell overlay availability is constrained.
- Only one overlay can appear per icon at a time.
- Overlay slots are often already used by sync and version-control applications.
- The model is a poor fit for a temporary, on-demand inspection workflow.
- It ties the feature to a part of the shell that is already heavily contested.

## Always-on custom rendering

### Advantages
- Avoids shell overlay slot conflicts.
- Could provide continuous awareness of desktop item state.
- Does not depend on Explorer’s overlay mechanisms.

### Drawbacks
- Adds permanent visual noise to the desktop.
- Is harder to justify for users who only need occasional inspection.
- Can become distracting or fatiguing on crowded desktops.
- Moves the concept away from a lightweight utility and toward an always-present desktop layer.

## On-demand temporary rendering

### Advantages
- Best matches the intended “inspect, then dismiss” workflow.
- Avoids shell overlay contention.
- Keeps the desktop unchanged when the feature is not in use.
- Reduces persistent visual clutter.
- Aligns well with the optional, utility-oriented design philosophy of PowerToys.

### Drawbacks
- Requires more custom rendering work than a simple overlay-based concept.
- Depends on reliable desktop integration and accurate icon position handling.
- Requires careful QA across different desktop layouts and display conditions.

## Preferred direction
On-demand temporary rendering is the preferred option because it solves the actual user problem more directly than the alternatives. The goal is not to create a permanent status layer on the desktop, but to give users a fast and lightweight way to identify what is already open when they need to reorganize or inspect a crowded workspace.

This approach also avoids the main practical limitation of shell overlay strategies while preserving a cleaner desktop experience when the feature is inactive.
