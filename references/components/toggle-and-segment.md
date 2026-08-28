---
component: Toggle & Segment
category: Interactive
variants: [segmented-toggle]
related: [checkbox-and-toggle, tab-bar]
---

# Toggle & Segment

> A segmented toggle lets users switch between a fixed set of mutually exclusive views or modes with a single tap, keeping the selection visually anchored in the UI.

## Overview

The segmented toggle renders as a pill-shaped container filled with a muted gray background, where each option is a button that slides a white active indicator to signal the current selection. It lives in the Interactive category of the Zuper design system and is the primary component for in-place view switching — such as toggling between related data sets — without navigating away or opening a dropdown.

## When to Use

- Switching between two or three closely related content views within the same panel, for example "Quotes" vs "Invoices".
- Filtering a list or table between a small number of mutually exclusive states where all options should be visible at once.
- Replacing a pair of radio buttons when horizontal space is available and the options benefit from a compact, pill-style presentation.
- Toggling a chart between time ranges (e.g., "Week / Month / Year") inline above the chart.

## When NOT to Use

- When the options navigate to distinct routes or full page contexts — use [Tab Bar](./tab-bar.md) instead, which is designed for navigation-level switching.
- When you need a binary on/off setting unrelated to view selection — use [Checkbox & Toggle](./checkbox-and-toggle.md) instead, which communicates a true/false state.
- When there are more than four options, as the toggle becomes crowded and hard to scan.

## Variants

| Variant | Description |
|---------|-------------|
| segmented-toggle | The only available variant; a fixed-height pill container with two or more buttons, one of which carries the active (white, elevated) treatment at any given time. Use this whenever you need mutually exclusive inline mode switching. |

## HTML Structure

```html
<!-- Segmented toggle — first option active -->
<div class="flex rounded-lg bg-gray-100 h-8 p-0.5">
  <button class="px-3 flex items-center justify-center rounded-lg transition-all h-7 text-md font-medium bg-white text-gray-600">
    Quotes
  </button>
  <button class="px-3 flex items-center justify-center rounded-lg transition-all h-7 text-md font-medium text-gray-500">
    Invoices
  </button>
</div>

<!-- Segmented toggle — second option active -->
<div class="flex rounded-lg bg-gray-100 h-8 p-0.5">
  <button class="px-3 flex items-center justify-center rounded-lg transition-all h-7 text-md font-medium text-gray-500">
    Quotes
  </button>
  <button class="px-3 flex items-center justify-center rounded-lg transition-all h-7 text-md font-medium bg-white text-gray-600">
    Invoices
  </button>
</div>
```

## Dos & Don'ts

### Do

- Keep option labels to one or two words so each button remains compact and readable at the fixed `h-7` height.
- Ensure exactly one option is always active; there is no valid "nothing selected" state for this component.
- Use `transition-all` on every button so the active indicator slides smoothly when the user switches selection.
- Limit the segmented toggle to two or three options to preserve the visual clarity of the pill layout.

### Don't

- Do not apply `bg-white text-gray-600` to more than one button at a time — having two active-looking options breaks the mutually exclusive contract and confuses users.
- Do not use this component for binary on/off settings — the toggle switch inside [Checkbox & Toggle](./checkbox-and-toggle.md) communicates that semantic correctly.
- Do not stretch the container to full width unless the content clearly benefits from it; the component is designed to hug its content naturally.
- Do not nest icons-only buttons without accessible labels, as the component has no built-in tooltip mechanism.

## Patterns & Rules

1. **Active button styling** — The active button receives `bg-white text-gray-600` and sits inside the `bg-gray-100` pill at `h-7`, creating a subtle raised appearance via the white fill. Inactive buttons use `text-gray-500` with no background.
2. **Container sizing** — The wrapper always uses `h-8 p-0.5` so the inner buttons fit at `h-7` with a uniform half-pixel inset on all sides.
3. **Mutual exclusivity** — Exactly one button must carry the active classes at all times; toggling another option must remove the active classes from the previously selected button before applying them to the new one.
4. **Label parity** — All option labels should be similar in length and grammatical form (all nouns, all verbs) so the pill remains visually balanced when no option is active.
5. **Transition consistency** — Every button inside the container must include `transition-all` to ensure the color shift animates uniformly across all options on each interaction.

## Accessibility

- The wrapper `<div>` should carry `role="group"` and an `aria-label` describing the purpose of the toggle (e.g., `aria-label="View mode"`).
- The active button must have `aria-pressed="true"`; all inactive buttons must have `aria-pressed="false"` so screen readers announce the current selection.
- Users must be able to move focus between buttons with `Tab` / `Shift+Tab` and activate the focused button with `Enter` or `Space`.
- Screen readers should announce each button label alongside its pressed state, for example "Quotes, pressed" and "Invoices, not pressed".

## Related Components

- [Checkbox & Toggle](./checkbox-and-toggle.md) — Use the toggle switch variant for binary on/off settings that are not about switching between named views.
- [Tab Bar](./tab-bar.md) — Use for top-level navigation between full page sections when selection changes the route rather than filtering or swapping content within a panel.
