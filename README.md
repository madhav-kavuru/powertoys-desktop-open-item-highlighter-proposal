# On-Demand Desktop Open-Item Highlighter Proposal

This repository contains a proposal for a PowerToys utility that helps users quickly see which desktop items are already open by temporarily highlighting them on demand.

The idea is aimed at crowded-desktop workflows: a user invokes the feature, checks which desktop folders or supported files are active, and then dismisses the visual markers so the desktop returns to normal.

## Overview

The main recommendation in this proposal is to use **on-demand temporary rendering**, not shell icon overlays.

That direction was chosen because it:

- fits a quick “show me what is open right now” workflow,
- avoids shell overlay conflicts with tools like OneDrive and Tortoise clients,
- reduces permanent visual noise on the desktop,
- and better matches the optional utility model of PowerToys.

## What’s in this repo

- [00-github-issue.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/00-github-issue.md) — Feature request text for the PowerToys GitHub repo
- [01-product-overview.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/01-product-overview.md) — Product framing, user problem, target users, and core concept
- [02-tech-spec.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/02-tech-spec.md) — Functional scope, architecture, rendering direction, risks, and acceptance criteria
- [03-ux-design-note.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/03-ux-design-note.md) — Interaction model, visual behavior, UX constraints, and accessibility considerations
- [04-technical-architecture-memo.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/04-technical-architecture-memo.md) — System components, interfaces, pseudocode, and implementation notes
- [05-qa-test-plan.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/05-qa-test-plan.md) — Crowded-desktop QA coverage, environments, and pass criteria
- [06-alternatives-and-tradeoffs.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/06-alternatives-and-tradeoffs.md) — Comparison of shell overlays, always-on rendering, and on-demand rendering
- [07-implementation-phases.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/07-implementation-phases.md) — Suggested rollout from proposal alignment to future enhancements

## Who this is for

This repository is intended for:

- PowerToys maintainers evaluating the idea
- Developers estimating implementation complexity
- Designers reviewing UX implications
- Testers reviewing crowded-desktop validation needs

## Proposed feature direction

The proposed flow is:

1. The user activates the mode with a hotkey, tray action, or PowerToys command.
2. The utility detects which desktop items are currently open.
3. It temporarily draws lightweight markers aligned to those desktop icons.
4. The user inspects the desktop.
5. The mode is dismissed and the desktop returns to its normal appearance.

This proposal intentionally keeps **V1 focused on desktop folders first**, with broader file support treated as a later phase.

## Why this is not a shell-overlay proposal

This repository does **not** recommend implementing the feature primarily through Explorer shell icon overlays.

Instead, it recommends a temporary rendering layer because:

- shell overlays are constrained,
- only one overlay can win per icon,
- overlay-heavy systems already use those slots,
- and a temporary inspection mode is better served by a temporary visual layer.

## How to use this repo

A simple way to use this proposal pack:

1. Review the documents in this repository.
2. Open [00-github-issue.md](https://github.com/madhav-kavuru/powertoys-desktop-open-item-highlighter-proposal/blob/main/00-github-issue.md).
3. Copy the issue text into a new issue in the PowerToys GitHub repository.
4. Link back to the supporting documents in this repository as needed.

## Related issue

This proposal has been submitted to the PowerToys repository here:  
[https://github.com/microsoft/PowerToys/issues/47203](https://github.com/microsoft/PowerToys/issues/47203)

## Notes

This repository is a proposal and planning pack, not an implementation repository.

Its purpose is to make discussion, evaluation, and possible future implementation easier by separating the idea into product, technical, UX, QA, and tradeoff documents.
