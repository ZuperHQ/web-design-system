---
component: Search Input
category: Navigation & Filtering
variants: [default, with-filters]
related: [toolbar-row, filter-chips, text-input]
---

# Search Input

> A compact, icon-prefixed text input that lets users instantly narrow a list view by typing a keyword query.

## Overview

The Search Input is a rounded, 32px-tall input field with a leading search icon and a contextual clear button that appears only when the field holds a value. It sits in the right-hand action cluster of the toolbar row, pairing naturally with the Columns toggle and view-switcher controls. Its border shifts from `border-gray-200` at rest to `border-gray-400` when active, giving clear visual feedback without relying on color alone.

## When to Use

- Filtering a data table, list, or kanban board where users need to locate a specific record by name or keyword.
- Placing alongside filter chips in a toolbar row to complement faceted filtering with a freeform text search.
- Any context where the result set is large enough that scrolling to find a record is impractical.
- Embedded in module-level toolbars (Jobs, Work Orders, Assets) where per-view searching is expected.

## When NOT to Use

- As a global site-wide search that navigates across modules — use a dedicated global search overlay instead.
- As a form field collecting user input to be saved — use [Text Input](./text-input.md) instead.
- When the list contains fewer than ~10 static items that a user can scan at a glance — the added chrome is unnecessary noise.

## Variants

| Variant | Description |
|---------|-------------|
| default | The rest state with placeholder text and a leading search icon; use this as the standard placement in any toolbar row. |
| with-filters | The active state when the field contains a typed value; a clear (`×`) button appears at the trailing end so users can reset the query without tabbing away. |

## HTML Structure

```html
<!-- Default (rest) -->
<div class="relative">
  <input
    type="text"
    placeholder="Search"
    class="peer min-w-60 ps-9 h-8 w-full rounded-lg border bg-white pl-3 pr-8 py-1 transition-[color,box-shadow] border-gray-200 outline-none focus:border-gray-400 text-gray-600"
  >
  <div class="text-gray-600 pointer-events-none absolute inset-y-0 start-0 flex items-center justify-center ps-3 peer-disabled:opacity-50">
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" width="16" height="16">
      <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
    </svg>
  </div>
</div>

<!-- With value (clear button visible) -->
<div class="relative">
  <input
    type="text"
    value="boiler"
    class="peer min-w-60 ps-9 h-8 w-full rounded-lg border bg-white pl-3 pr-8 py-1 transition-[color,box-shadow] border-gray-400 outline-none focus:border-gray-400 text-gray-600"
  >
  <div class="text-gray-600 pointer-events-none absolute inset-y-0 start-0 flex items-center justify-center ps-3 peer-disabled:opacity-50">
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" width="16" height="16">
      <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
    </svg>
  </div>
  <!-- Clear button — render only when input has a value -->
  <button class="text-gray-400 hover:text-gray-600 absolute inset-y-0 end-0 flex h-full w-9 items-center justify-center rounded-e-lg outline-none">
    <i class="ti ti-x text-lg"></i>
  </button>
</div>
```

## Dos & Don'ts

### Do

- Place the Search Input on the right side of the toolbar row, adjacent to the Columns and view-switcher controls.
- Show the clear button (`ti-x`) only when the input has a non-empty value, so users always know they can reset.
- Apply `min-w-60` to ensure the field is wide enough to display a meaningful query without truncation.
- Use `peer` and `peer-disabled:opacity-50` on the wrapper icon so the icon reflects the input's disabled state automatically.
- Filter results as the user types (debounced) rather than requiring a form submit, to reduce friction.

### Don't

- Remove the leading search icon — without it the input looks identical to a plain text field and users lose affordance context.
- Use this component for multi-line input or rich query builders — it breaks the fixed 32px height and alignment with the toolbar row.
- Stretch the input to fill the entire toolbar width — it crowds the filter and view controls that must share the same row.
- Change the placeholder text away from "Search" to a lengthy instruction like "Search by name or ID" — the icon already communicates intent, and long placeholder text gets clipped.
- Omit the `transition-[color,box-shadow]` class — losing the border transition makes focus feedback feel abrupt and inconsistent with the rest of the design system.

## Patterns & Rules

1. **Border state reflects focus** — The border is `border-gray-200` at rest and transitions to `border-gray-400` on focus or when a value is present; never use a colored (blue/primary) border for this component.
2. **Clear button is conditional** — Render the trailing `<button>` with `ti ti-x` only when the input value is non-empty; it must not occupy space in the rest state.
3. **Fixed height of 32px** — Always use `h-8` on the input; deviating breaks alignment with sibling toolbar controls such as icon buttons and the view-switcher segment.
4. **Peer-based icon opacity** — The search icon wrapper uses the Tailwind `peer` pattern so `peer-disabled:opacity-50` dims the icon automatically when the input is disabled, without extra JavaScript.
5. **Minimum width constraint** — Apply `min-w-60` (240px) to prevent the field from collapsing to an unusable width on narrower viewports; the toolbar row should reflow or scroll before the input shrinks below this threshold.

## Accessibility

- Add `aria-label="Search"` or a visually hidden `<label>` element associated via `for`/`id` — the placeholder alone is not a sufficient accessible label.
- The `Tab` key must move focus to the input; `Escape` should clear the value and return focus to the input or move it to the triggering element.
- The clear button must have `aria-label="Clear search"` so screen readers announce its purpose rather than just "button".
- The search icon wrapper uses `pointer-events-none` to keep it out of the tab order; do not add `tabindex` or interactive behavior to the icon container.

## Related Components

- [Text Input](./text-input.md) — The base form input for user-submitted data; use instead of Search Input whenever the value will be saved or sent as form data.
- [Toolbar Row](./toolbar-row.md) — The parent layout component that positions the Search Input alongside filter, column, and view controls.
- [Filter Chips](./filter-chips.md) — Paired with Search Input in the toolbar row to provide faceted, attribute-level filtering alongside freeform keyword search.
