# Lanhu UI Calibration Checklist

Use this checklist when a Lanhu UI review involves more than one small view or component.

## Default Invocation

The user should only need to name the skill and page, for example:

`Use lanhu-ui-review to correct the membership center page.`

Do not require the user to say "only UI" or list spacing, font, color, and alignment checks. Those are defaults of this skill.

Before doing UI calibration, verify that both Chrome control and Computer Use capabilities are installed/enabled. If either is missing, help the user install or enable the missing plugin first.

Before asking for a Lanhu link, check Chrome for an open Lanhu tab or page. If none is open, open `https://lanhuapp.com/` in Chrome automatically. Ask for the design source only when Lanhu opens but the specific design page cannot be determined.

## Measurement Capture

- Screen size and design artboard size.
- Safe-area/top inset and first visible element y position.
- Main image/banner x, y, width, height, fit behavior, and local asset name.
- Navigation icons: visual size, tap target, color/asset, x/y, and center alignment.
- Primary title/subtitle: text box x/y/size, font family, size, weight, line height, color, alignment.
- Repeated rows/chips/cards: outer viewport width, first item x, item width/height, internal padding, item gap, border, background, radius, shadow.
- Cards: x/y/width/height, selected/unselected variants, border width/color, gradient/background, radius, shadow, internal title/price/description positions.
- Buttons: x/y/width/height, radius, background, shadow, text size/weight/color, icon size, disabled/loading states.
- Bottom text/legal area: width, top gap, line height, color, link styles, bottom inset.

## Code Review Before Editing

- Identify the smallest screen, view, component, layout, style, or asset that owns the visual mismatch.
- Check whether constants, tokens, styles, dimensions, colors, or theme resources already exist for the same visual system.
- Check tests for assumptions around text, layout, default selected state, loading state, and enabled/disabled behavior.
- Check whether the file already has unrelated dirty changes; preserve them.

## Edit Guardrails

- Keep changes UI-only unless the user explicitly asks otherwise.
- Do not change state-management, controller, view-model, or state-machine logic for a visual mismatch.
- Do not change API models, endpoint names, database writes, purchase flow, entitlement checks, or product selection rules.
- Do not add hard-coded user-facing text without localization.
- Do not replace a working asset with a generated or approximate asset unless requested.
- Avoid broad refactors while calibrating a screen.

## Common UI Fixes

- Remove parent horizontal padding when the design viewport is full-width.
- Add child padding when only the item content is inset.
- Use the platform's alignment/stack/constraint tools when design coordinates require exact placement.
- Use stable dimensions to prevent text/loading/spinner states from shifting layout.
- Tune line-height behavior only when needed to match text box behavior.
- For icon/text vertical alignment, inspect the asset canvas and optical center; visual misalignment may come from transparent pixels inside the image.
- Keep shadows and borders separate when the design shows both.

## Validation

- Run the formatter for touched files, for example Dart format, SwiftFormat, ktlint, Prettier, or the project's equivalent.
- Run the targeted static check/compiler/linter for the touched feature when possible.
- Run the nearest UI, unit, component, snapshot, or instrumentation test that covers the changed screen.
- If there is an existing failing test outside the UI change, report the exact test and why it appears unrelated.

## Final Response Pattern

Always include a UI calibration summary after finishing. The summary should cover:

- Spacing: updated/matched/not verified, with key gaps or insets.
- Typography: updated/matched/not verified, with font sizes, weights, line heights, and colors.
- Layout and alignment: updated/matched/not verified, with key positions, dimensions, and alignment notes.
- Visual styling: updated/matched/not verified, with colors, borders, radii, shadows, gradients, and opacity.
- Assets: updated/matched/not verified, with image/icon names, sizes, and fit behavior.
- States: updated/matched/not verified, covering loading, empty, error, disabled, selected, pressed, and repeated item variants when relevant.
- Validation: commands run and results.
- Unverified/deferred: any design area not checked and the reason.

Keep it concise, but do not omit categories silently.
