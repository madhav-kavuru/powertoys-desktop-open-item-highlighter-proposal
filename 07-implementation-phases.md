# Implementation Phases

## Overview
A phased implementation plan helps keep the proposal realistic and reduces the risk of overcommitting too early. The recommended path is to confirm product direction first, prove the core technical approach in a focused prototype, deliver a narrow V1 centered on desktop folders, and then expand only after the core interaction is validated.

This sequencing supports a practical rollout while keeping the proposal aligned with the real user problem.

## Phase 1: Proposal alignment
The first phase is to confirm that the feature direction is worth pursuing and that the proposed interaction model fits PowerToys.

Key goals:
- Validate maintainer interest in the problem and the proposed utility.
- Confirm that on-demand temporary rendering is the preferred direction.
- Align on the decision to avoid shell overlays.
- Lock V1 scope to desktop folders only.

## Phase 2: Feasibility prototype
The second phase is to prove that the core technical approach is workable before investing in full implementation.

Key goals:
- Detect desktop folders that are currently open in File Explorer.
- Build a reliable desktop item index.
- Resolve current desktop icon coordinates.
- Demonstrate a temporary rendering layer aligned to desktop items.
- Validate that the concept can work without disrupting normal desktop behavior.

## Phase 3: V1 implementation
Once feasibility is established, the third phase is to build a usable first version with a narrow and disciplined scope.

Key goals:
- Add supported activation paths such as hotkey, tray command, or PowerToys entry point.
- Implement a stable update loop for active-mode refresh.
- Apply the initial visual treatment for highlighted items.
- Add cleanup, error handling, and safe disable behavior.
- Ensure the mode behaves consistently during normal desktop use.

## Phase 4: QA hardening
The fourth phase is to strengthen the implementation across realistic desktop conditions and edge cases.

Key goals:
- Test crowded desktop layouts with large icon counts.
- Test common scaling levels and icon sizes.
- Test single-monitor and multi-monitor setups.
- Test coexistence with tools such as OneDrive and Tortoise-based clients.
- Fix layout, rendering, and refresh edge cases discovered during validation.

## Phase 5: Future enhancements
After V1 is stable, later phases can expand capability without changing the core interaction model.

Possible enhancements:
- Limited support for common desktop file types such as PDFs and Microsoft Office documents.
- Additional visual styles or marker options.
- Contrast-aware or wallpaper-aware marker selection.
- More settings, customization, and UX polish.
- Broader detection logic if future scope justifies it.
