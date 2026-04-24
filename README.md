# PowerToys Proposal: On-Demand Desktop Open-Item Highlighter

This repository contains a proposal pack for a possible new Microsoft PowerToys utility: an **on-demand desktop open-item highlighter**.

The idea is simple: when a user turns the feature on, PowerToys would temporarily highlight desktop icons whose corresponding folders, and later possibly certain files, are currently open. When the user turns the mode off, the markers disappear and the desktop returns to its normal appearance.

## Why this proposal exists
Some people use the Windows desktop as an active workspace with many project folders, shortcuts, and files visible at once. In that setup, it can be hard to tell which desktop items are already open, especially on crowded desktops or large displays with many small icons.

This proposal explores a lightweight utility that helps answer a single question quickly:

**Which desktop items are open right now?**

## Why this approach avoids shell overlays
The proposal is intentionally designed as an **on-demand temporary mode** rather than a persistent shell-overlay feature.

That choice is important because Windows shell icon overlays are limited, only one overlay can appear on an icon at a time, and common tools such as OneDrive, Dropbox, Box, and Tortoise clients already use that mechanism. An always-on overlay-based design would therefore be more likely to conflict with real user systems.

Instead, this proposal uses a temporary highlight-layer approach that appears only when the user requests it.

## Repository contents
This repository is organized as a proposal pack so reviewers can read it at different levels of detail.

| File | Purpose |
|---|---|
| `00-github-issue-draft.md` | Short issue text for opening the feature request on the PowerToys GitHub repo |
| `01-product-overview.md` | High-level explanation of the user problem, target users, and feature concept |
| `02-tech-spec.md` | Main feature specification covering scope, architecture, risks, and acceptance criteria |
| `03-ux-design-note.md` | User experience guidance for activation, visual behavior, and interaction constraints |
| `04-technical-architecture-memo.md` | Engineering-oriented memo with system components, interfaces, and pseudocode |
| `05-qa-test-plan.md` | Test plan focused on crowded desktops, scaling, overlays, and stability |
| `06-alternatives-and-tradeoffs.md` | Comparison of shell overlays, always-on rendering, and on-demand rendering |
| `07-implementation-phases.md` | Suggested phased development path from proposal to V1 |

## Recommended reading order
For a quick review, start with the issue draft, product overview, and tech spec. If the concept seems promising, continue with the architecture memo and QA test plan.

1. `00-github-issue-draft.md`
2. `01-product-overview.md`
3. `02-tech-spec.md`
4. `04-technical-architecture-memo.md`
5. `05-qa-test-plan.md`

## How to use this proposal pack
A practical submission path is:

1. Read `00-github-issue-draft.md` and adapt it for a PowerToys feature request.
2. Use `01-product-overview.md` and `02-tech-spec.md` as the main supporting documents.
3. Use `04-technical-architecture-memo.md` and `05-qa-test-plan.md` if reviewers want deeper technical detail.
4. Link these Markdown files from the PowerToys GitHub issue rather than pasting every document into the issue body.

## Notes
This repository is a proposal and planning package, not an implementation repository. It is meant to help present the concept clearly, explain why the on-demand approach is preferred, and make it easier for PowerToys maintainers or outside contributors to evaluate the feature.
