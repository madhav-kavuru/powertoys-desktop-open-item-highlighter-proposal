# Alternatives and Tradeoffs

## Shell icon overlays
### Pros
- Feels native to Explorer.
- Conceptually simple at first glance.

### Cons
- Constrained system resource.
- One overlay per icon.
- Commonly conflicts with sync and version-control tools.
- Poor fit for a temporary inspection workflow.

## Always-on custom rendering
### Pros
- Avoids shell overlay slot conflict.
- Could provide continuous awareness.

### Cons
- Adds permanent visual noise.
- Harder to justify for casual users.
- More likely to become distracting on crowded desktops.

## On-demand temporary rendering
### Pros
- Best fit for quick inspection.
- Avoids shell overlay contention.
- Desktop returns to normal immediately after use.
- More aligned with PowerToys’ optional utility model.

### Cons
- More custom rendering work than shell overlays.
- Requires careful desktop integration and QA.

## Preferred option
On-demand temporary rendering is the preferred design because it solves the real user problem while avoiding the most common practical limitation of overlay-based approaches.
