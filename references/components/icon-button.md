---
component: Icon Button
category: Interactive
variants: [default, ghost, danger]
related: [button]
---

# Icon Button

> A square, icon-only button that triggers a single action without a visible text label, saving space in dense or repeated UI contexts.

## Overview

The Icon Button is a fixed 9-unit (36 px) square button that contains a single Tabler icon centered within it. It carries a subtle border, light background, and drop shadow that match the Zuper design system's standard surface treatment, making it blend cleanly into toolbars, list rows, and detail panels while still being clearly interactive. Its primary role is to expose secondary or contextual actions — such as edit, delete, or overflow — without the visual weight of a full labeled button.

## When to Use

- In data table rows or list items where recurring actions (edit, delete, more options) must be compact and scannable.
- In toolbar or header areas where space is constrained and the icon's meaning is universally understood in context.
- When a single destructive action (delete, remove) must be exposed inline but kept visually recessive until needed.
- For overflow or contextual menus triggered by a three-dot (`ti-dots-vertical`) or close (`ti-x`) affordance.
- When the action is supplementary to a primary labeled button already present on the same surface.

## When NOT to Use

- When the action is the primary call-to-action on a page or panel — use [Button](./button.md) instead so the label communicates the action clearly.
- When the icon's meaning is ambiguous without a label — use [Button](./button.md) with an icon and text to avoid confusion.

## Variants

| Variant | Description |
|---------|-------------|
| default | Bordered, white-background button with a gray icon; use for neutral secondary actions such as edit, view, or overflow that sit alongside other controls. |
| ghost | Borderless button with padding only, rendered in muted gray; use for low-emphasis inline actions that should recede visually until hovered, such as pin or reorder controls within a dense form. |
| danger | Borderless or lightly bordered button with a red icon that deepens on hover and gains a red tinted background; use for irreversible destructive actions (delete, remove) to signal risk without the weight of a full danger button. |

## HTML Structure

```html
<!-- Default variant — bordered icon button -->
<button
  type="button"
  class="h-9 w-9 inline-flex justify-center items-center gap-x-2 px-2 rounded-lg shadow-2xs border bg-white text-gray-600 cursor-pointer"
  aria-label="Edit"
>
  <em class="ti ti-edit text-lg"></em>
</button>

<!-- Default variant — disabled state -->
<button
  type="button"
  class="h-9 w-9 inline-flex justify-center items-center gap-x-2 px-2 rounded-lg shadow-2xs border bg-white text-gray-600 opacity-50 pointer-events-none"
  aria-label="Edit"
  disabled
>
  <em class="ti ti-edit text-lg"></em>
</button>

<!-- Ghost variant — no border, muted gray icon -->
<button
  type="button"
  class="w-fit flex items-center justify-center cursor-pointer rounded-md p-1.5 text-gray-400 hover:text-gray-600 hover:bg-gray-200"
  aria-label="Pin filter"
>
  <!-- inline SVG or ti icon -->
</button>

<!-- Danger variant — red icon, red hover surface -->
<button
  type="button"
  class="w-fit flex items-center justify-center cursor-pointer rounded-md p-1.5 text-red-400 hover:text-red-500 hover:bg-red-50"
  aria-label="Delete"
>
  <em class="ti ti-trash text-lg"></em>
</button>
```

## Dos & Don'ts

### Do

- Always supply a descriptive `aria-label` that names the specific action, not the icon (e.g., `aria-label="Delete attachment"`, not `aria-label="trash"`).
- Use the `ti` icon size class `text-lg` inside default-variant buttons to keep the icon optically centered in the 36 px target.
- Pair a danger variant icon button with a confirmation step (modal or popover) before executing irreversible actions.
- Apply `opacity-50 pointer-events-none` and the `disabled` attribute together when disabling, so both visual and pointer feedback are consistent.
- Limit icon buttons in a single row to three or fewer to prevent toolbar overload; collapse extras behind an overflow (`ti-dots-vertical`) button.

### Don't

- Do not omit `aria-label` — icon-only buttons are completely opaque to screen readers without it, breaking accessibility.
- Do not use a danger variant for actions that are reversible — it trains users to expect irreversibility and erodes the signal when it matters.
- Do not mix the default bordered variant and the ghost variant within the same toolbar group; inconsistent affordances make the hierarchy unclear.
- Do not increase the button's fixed dimensions (`h-9 w-9`) for emphasis — use [Button](./button.md) with a label if the action needs more visual weight.
- Do not place two danger icon buttons adjacent to each other; if multiple destructive actions are needed, group them behind a single overflow menu.

## Patterns & Rules

1. **Fixed square sizing** — The default variant is always `h-9 w-9` (36 × 36 px); the ghost and danger variants use `p-1.5` padding around the icon instead. Do not mix sizing conventions within the same group.
2. **Hover state via background fill** — On hover the default variant switches `bg-white` to `bg-gray-50`; the danger variant introduces `hover:bg-red-50` and deepens the icon to `hover:text-red-500`. Never use an outline or border change alone as the sole hover signal.
3. **Icon semantics drive variant choice** — Choose the variant based on the consequence of the action: neutral consequence → default, no consequence → ghost, destructive consequence → danger.
4. **Disabled is pointer-blocking** — Add `pointer-events-none` alongside `opacity-50` to prevent mis-clicks on disabled icon buttons; `disabled` alone is insufficient for non-native interactive elements.
5. **Overflow icon as last resort** — When more than three icon buttons are needed in a row, collapse the least-used ones into an overflow button using `ti-dots-vertical` to preserve scanability.

## Accessibility

- Requires `aria-label` on every instance because there is no visible text label; the label must describe the action, not the icon name.
- Keyboard interaction: reachable via `Tab`, activated with `Enter` or `Space`; no arrow-key navigation unless inside a toolbar `role="toolbar"` with `aria-keyshortcuts`.
- Screen readers announce the button role and the `aria-label` value; do not add redundant `role="button"` on a native `<button>` element.

## Related Components

- [Button](./button.md) — The labeled equivalent; use when the action needs a visible text label for clarity or when it is the primary call-to-action on a surface.
