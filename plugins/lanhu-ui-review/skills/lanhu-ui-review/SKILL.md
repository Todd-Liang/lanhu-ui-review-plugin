---
name: lanhu-ui-review
description: Calibrate app UI against Lanhu design specs across mobile or web codebases. Use when the user says "use lanhu-ui-review to calibrate/fix/check/correct <page>", mentions Lanhu, asks for UI review, UI calibration, pixel check, design-to-code correction, or strict design matching. Useful for Flutter, iOS, Android, web, or other client UI work where Codex must find the Lanhu design, inspect element measurements, update presentation code, and avoid business logic changes.
---

# Lanhu UI Review

## Goal

Perform a design-to-implementation UI calibration pass against a Lanhu screen. Treat the Lanhu design as the source of truth for spacing, sizing, typography, color, alignment, radius, shadow, and asset usage.

This skill is for UI-only work. Do not change API calls, state machines, repositories, navigation behavior, purchase logic, persistence, analytics, or feature semantics unless the user explicitly expands the scope.

## Prerequisites

This skill requires both Chrome control and Computer Use capabilities:

- Chrome control: needed to detect/open Lanhu tabs, navigate Lanhu, and inspect browser state.
- Computer Use: needed to click Lanhu design layers/elements and read visual inspector details when browser DOM access is not enough.

Before starting calibration:

1. Check whether Chrome control and Computer Use tools/skills are available in the current Codex environment.
2. If either capability is missing, do not proceed with UI calibration yet.
3. Help the user install or enable the missing OpenAI bundled Chrome and Computer Use plugins, then ask them to start a new thread or reload the environment so the tools are available.
4. Continue only after both capabilities are available, unless the user explicitly approves a reduced screenshot-based fallback.

## Workflow

1. Resolve the target page and Lanhu design.
   - Treat prompts like "use lanhu-ui-review to correct membership center page" as complete enough to start.
   - Infer the target screen, view, component, or layout from the page name and project files.
   - Check Chrome for an open Lanhu page before asking the user for anything. Search current and open tabs for Lanhu-related URLs or page titles when the available tool supports it.
   - If a Lanhu page is found, use Chrome or Computer Use to inspect it.
   - If no Lanhu page is open, use Chrome to open `https://lanhuapp.com/` automatically.
   - After opening Lanhu, continue if a specific design page is available. If Chrome only shows the Lanhu home/login/project list and the target design cannot be determined, ask the user to select the design page or provide the design link/screenshot.
   - Ask one concise question only when the target page or design source cannot be determined.

2. Collect design measurements before editing.
   - Click Lanhu elements to capture x/y, width/height, font family, font size, font weight, line height, color, border, radius, shadow, opacity, and image asset dimensions.
   - Measure relationships, not only individual elements: top gaps, left/right insets, center alignment, text/icon alignment, card-to-card gaps, scroll viewport width, safe-area offsets, and bottom legal/action spacing.
   - Record enough values in the working notes to justify the UI changes.

3. Inspect implementation structure.
   - Locate the screen, view, component, layout, XML/storyboard, style, asset, and nearby tests that own the mismatch.
   - Follow the current project's architecture and platform conventions. Keep rendering, state, data access, and business rules in their existing layers.
   - Prefer existing design tokens, style resources, components, assets, localization, and layout patterns unless they conflict with the design.

4. Edit only presentation code needed for visual parity.
   - Safe changes: padding, constraints, dimensions, colors, text styles, font weights, line heights, border radius, borders, shadows, alignment, asset sizing, scroll/container width, and visual loading/error states.
   - Avoid changes to business logic, state controllers/view models, DTOs/models, repositories/services, API parameters, database schema, product selection rules, entitlement checks, or localization meaning.
   - Keep text localized using the project's localization system. If new user-facing text is unavoidable, update every required locale/resource file and regenerate generated localization code if the project uses it.

5. Validate.
   - Run the formatter for touched files if the platform has one.
   - Run the targeted linter/analyzer/compiler check for the touched feature when possible.
   - Run relevant UI/unit/snapshot tests when available.
   - If a broader test fails for unrelated pre-existing business expectations, report that separately and do not hide it.

6. Report succinctly.
   - Include a UI calibration summary that lists every checked calibration category and the result.
   - For each category, state the main design values used, what was changed, or that no change was needed.
   - Include any category that could not be verified and why.
   - Mention validation commands and results.
   - Mention any known unrelated failures or warnings.
   - Do not claim exact visual parity if no screenshot/manual visual check was performed.

## Lanhu Inspection Notes

When using Chrome or Computer Use:

- Click individual design layers for exact values instead of estimating from screenshots.
- Inspect nested text runs when a label mixes font sizes or weights.
- Check whether a visible row/strip is full-screen width or intentionally inset.
- Check whether borders belong to the container or each repeated item.
- Re-open or re-click elements after scrolling; Lanhu panels can keep stale selection data.

## Default Review Scope

Always check these without requiring the user to spell them out:

- Spacing: page insets, section gaps, row gaps, card padding, safe-area offsets, and bottom spacing.
- Typography: font size, font weight, line height, letter spacing, text color, alignment, and truncation.
- Layout: x/y position, width/height, center alignment, baseline/optical alignment, scrollable viewport width, and responsive behavior.
- Visual styling: background colors, gradients, borders, border widths, radius, shadows, opacity, and selected/unselected states.
- Assets: correct image/icon, rendered size, fit mode, transparent canvas causing optical offset, and local asset naming.
- States: loading, empty, error, disabled, selected, pressed, and repeated item variants when visible in the design or existing UI.

## Final Calibration Summary

After finishing UI calibration, show a concise checklist-style summary covering all default review categories:

- Spacing
- Typography
- Layout and alignment
- Visual styling
- Assets
- States
- Validation
- Unverified or deferred items

For each item, include the result such as "updated", "matched/no change", or "not verified", plus the key values or reason when useful. This summary is required even for small UI corrections.

## Implementation Notes

- Set explicit letter spacing to zero when the design has no letter spacing and local code previously drifted.
- Use explicit heights for fixed-format UI such as buttons, cards, chips, tab bars, and loading placeholders.
- Use cover/content-scale-fill only when the design image fills a fixed viewport; use contain/aspect-fit when the full image must remain visible.
- For repeated visual items, preserve per-item decoration if the design shows each item with its own border/background.
- For marquees or horizontal strips, distinguish the viewport width from item padding. A full-width marquee can still contain bordered items with their own internal padding.
- Use the project's established asset-loading pattern instead of introducing a new one for a visual-only fix.

## Reference Checklist

For detailed review prompts and common UI checkpoints, read `references/ui-calibration-checklist.md` when starting a non-trivial calibration pass.
