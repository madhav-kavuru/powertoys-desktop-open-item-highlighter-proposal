# On-Demand Desktop Open-Item Highlighter Proposal

This repository contains a proposal pack for a PowerToys utility that helps users quickly identify which desktop items are currently open by temporarily highlighting them on demand.

The proposal is designed around a crowded-desktop workflow: the user invokes the feature, inspects which desktop folders or supported files are active, and then dismisses the visual markers so the desktop returns to normal.

## Proposal summary

The core recommendation in this proposal is **on-demand temporary rendering**, not shell icon overlays.

Why this direction was chosen:

- It fits a quick “show me what is open right now” workflow.
- It avoids shell overlay slot conflicts with tools like OneDrive and Tortoise clients.
- It reduces permanent visual noise on the desktop.
- It better matches the optional utility model of PowerToys.

## Repository contents

- [00-github-issue.md](./00-github-issue.md) — Feature request text formatted for creating a new PowerToys GitHub issue
- [01-product-overview.md](./01-product-overview.md) — Product framing, user problem, target users, and core concept
- [02-tech-spec.md](./02-tech-spec.md) — Functional scope, architecture, rendering direction, risks, and acceptance criteria
- [03-ux-design-note.md](./03-ux-design-note.md) — Interaction model, visual behavior, UX constraints, and accessibility considerations
- [04-technical-architecture-memo.md](./04-technical-architecture-memo.md) — System components, interfaces, pseudocode, and implementation notes
- [05-qa-test-plan.md](./05-qa-test-plan.md) — Crowded-desktop QA coverage, environments, and pass criteria
- [06-alternatives-and-tradeoffs.md](./06-alternatives-and-tradeoffs.md) — Comparison of shell overlays, always-on rendering, and on-demand rendering
- [07-implementation-phases.md](./07-implementation-phases.md) — Suggested rollout from proposal alignment to future enhancements

## Recommended reading order

If you want the shortest path through the proposal, read the files in this order:

1. [01-product-overview.md](./01-product-overview.md)
2. [02-tech-spec.md](./02-tech-spec.md)
3. [03-ux-design-note.md](./03-ux-design-note.md)
4. [04-technical-architecture-memo.md](./04-technical-architecture-memo.md)
5. [05-qa-test-plan.md](./05-qa-test-plan.md)
6. [06-alternatives-and-tradeoffs.md](./06-alternatives-and-tradeoffs.md)
7. [07-implementation-phases.md](./07-implementation-phases.md)

If you are preparing a submission issue first, start with [00-github-issue.md](./00-github-issue.md).

## Intended audience

This repository is meant for:

- PowerToys maintainers evaluating the idea
- Developers estimating implementation complexity
- Designers reviewing UX implications
- Testers reviewing crowded-desktop validation needs

## Proposed feature direction

The proposed feature behavior is:

1. User activates the mode with a hotkey, tray action, or PowerToys command.
2. The utility detects which desktop items are currently open.
3. It temporarily draws clear, lightweight markers aligned to those desktop icons.
4. The user inspects the desktop.
5. The mode is dismissed and the desktop returns to its prior appearance.

The proposal intentionally keeps **V1 focused on desktop folders first**, with broader file support treated as a later phase.

## Why this is not a shell-overlay proposal

This repository does **not** recommend implementing the feature primarily through Explorer shell icon overlays.

Instead, it recommends a temporary rendering layer because:

- shell overlays are constrained,
- only one overlay can win per icon,
- overlay-heavy systems already use those slots,
- and a temporary inspection mode is better served by a temporary visual layer.

## Submission workflow

A simple way to use this proposal pack:

1. Review the documents in this repository.
2. Open [00-github-issue.md](./00-github-issue.md).
3. Copy the issue text into a new issue in the PowerToys GitHub repository.
4. Link back to the supporting documents in this repository as needed.

## Notes

This repository is a proposal and planning pack, not an implementation repository.

It is intended to make discussion, evaluation, and possible future implementation easier by separating the idea into product, technical, UX, QA, and tradeoff documents.
