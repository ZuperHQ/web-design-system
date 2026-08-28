---
component: Filter Chips
category: Navigation & Filtering
variants: [pinned]
related: [toolbar-row, search-input]
---

# Filter Chips

> Filter Chips are interactive inline controls that let users apply, inspect, and remove individual field-level filters directly from a list or table toolbar without opening a separate filter panel.

## Overview

Each chip is a compact, pill-shaped row divided into up to four clickable segments: a label (the field name on a gray background), an operator (e.g. "is", "contains", "within"), a value (the selected filter value in darker text), and an optional remove button (×). When no filter has been set yet, the chip renders in a dashed-border default state with a `ti-circle-dashed-plus` icon to invite interaction. When the filter row overflows its container, left and right arrow buttons appear over a gradient fade to reveal additional chips.

## When to Use

- On list views, tables, or kanban boards where users need to filter records by one or more fields simultaneously.
- When specific filters should always be visible and accessible without expanding a filter panel — i.e., "pinned" filters that belong to the primary workflow.
- When users need to see at a glance which filters are currently active and what values they have set.
- When users need to clear or change a single filter independently without resetting all active filters.
- When the set of filterable fields is known in advance and can be represented as a fixed row of chips.

## When NOT to Use

- When filtering is ad-hoc and users need to pick arbitrary fields on the fly — use [Select Dropdown](./select-dropdown.md) inside a filter-builder panel instead.
- When the only required input is a free-text keyword search — use [Search Input](./search-input.md) instead, which is purpose-built for that pattern.

## Variants

| Variant | Description |
|---------|-------------|
| pinned | The only supported variant; chips are always visible in the toolbar row and represent pre-configured, administrator- or system-defined filterable fields. Use this variant whenever filters must remain persistently accessible rather than toggled open from a button. |

## HTML Structure

```html
<!-- Scroll carousel wrapper (used when chips may overflow the container) -->
<div class="flex items-center space-x-2.5 relative" data-pinned-filter-carousel>

  <!-- Left scroll arrow (hidden until user scrolls right) -->
  <div data-pinned-filter-front class="absolute left-0 z-10 h-9 flex items-center justify-start w-10 rounded-l-md"
       style="display:none; background: linear-gradient(to right, #F1F5F9 80%, transparent 100%);">
    <button type="button" class="w-8 h-8 bg-white rounded-full border border-gray-300 flex items-center justify-center transition-all duration-200 hover:border-blue-500">
      <i class="ti ti-chevron-left text-gray-600 font-medium text-2xl"></i>
    </button>
  </div>

  <!-- Scrollable chip row -->
  <div class="flex items-center gap-3 overflow-x-auto scrollbar-hide rounded-md" data-pinned-filter-scroll>

    <!-- Default chip: no value set (dashed border, icon + label only) -->
    <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-dashed border-gray-300 hover:border-gray-400">
      <div class="h-full flex items-center justify-start bg-gray-50 rounded-lg text-gray-500 hover:text-gray-600" style="max-width:12.5rem;">
        <button type="button" class="h-full px-2 text-base flex items-center truncate hover:bg-white rounded-lg space-x-2">
          <i class="ti ti-circle-dashed-plus"></i>
          <span class="truncate leading-tight font-normal">Assigned To</span>
        </button>
      </div>
    </div>

    <!-- Active chip: operator set, no value -->
    <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-gray-200">
      <div class="px-2 rounded-l-lg text-gray-500 h-full flex items-center justify-start bg-gray-50" style="max-width:7.5rem;">
        <span class="text-base truncate leading-tight text-gray-500">Priority</span>
      </div>
      <div class="rounded-r-lg h-full flex items-center justify-start hover:bg-gray-50" style="max-width:6.5rem;">
        <button class="w-full h-full px-2 text-base flex items-center">
          <span class="truncate leading-tight text-gray-500 hover:text-gray-600">is not</span>
        </button>
      </div>
    </div>

    <!-- Active chip: label + operator + value + remove button -->
    <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-gray-200">
      <div class="px-2 rounded-l-lg text-gray-500 h-full flex items-center justify-start bg-gray-50" style="max-width:7.5rem;">
        <span class="text-base truncate leading-tight text-gray-500">Status</span>
      </div>
      <div class="h-full flex items-center justify-start hover:bg-gray-50" style="max-width:6.5rem;">
        <button class="w-full h-full px-2 text-base flex items-center">
          <span class="truncate leading-tight text-gray-500 hover:text-gray-600">is</span>
        </button>
      </div>
      <div class="h-full flex items-center justify-start hover:bg-gray-50" style="max-width:7.5rem;">
        <button class="w-full h-full px-2 text-base flex items-center">
          <span class="truncate text-gray-600 leading-tight">Open</span>
        </button>
      </div>
      <button type="button" class="text-gray-500 hover:text-gray-600 hover:bg-gray-50 p-2 h-full flex items-center justify-center rounded-r-lg">
        <i class="ti ti-x text-lg"></i>
      </button>
    </div>

    <!-- Active chip: multiple values selected -->
    <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-gray-200">
      <div class="px-2 rounded-l-lg text-gray-500 h-full flex items-center justify-start bg-gray-50" style="max-width:7.5rem;">
        <span class="text-base truncate leading-tight text-gray-500">Assigned To</span>
      </div>
      <div class="h-full flex items-center justify-start hover:bg-gray-50" style="max-width:6.5rem;">
        <button class="w-full h-full px-2 text-base flex items-center">
          <span class="truncate leading-tight text-gray-500 hover:text-gray-600">is</span>
        </button>
      </div>
      <div class="h-full flex items-center justify-start hover:bg-gray-50" style="max-width:7.5rem;">
        <button class="w-full h-full px-2 text-base flex items-center">
          <span class="truncate text-gray-600 leading-tight">3 selected</span>
        </button>
      </div>
      <button type="button" class="text-gray-500 hover:text-gray-600 hover:bg-gray-50 p-2 h-full flex items-center justify-center rounded-r-lg">
        <i class="ti ti-x text-lg"></i>
      </button>
    </div>

  </div>

  <!-- Right scroll arrow (shown when chips overflow right) -->
  <div data-pinned-filter-back class="absolute right-0 z-10 h-8 flex items-center justify-end w-10 rounded-r-md"
       style="background: linear-gradient(to left, #F1F5F9 80%, transparent 100%);">
    <button type="button" class="w-8 h-8 bg-white rounded-full border border-gray-300 text-gray-500 hover:text-gray-600 flex items-center justify-center transition-all duration-200 hover:border-gray-400">
      <i class="ti ti-chevron-right font-medium text-lg"></i>
    </button>
  </div>

</div>
```

## Dos & Don'ts

### ✅ Do

- Show the chip in its dashed default state (with `ti-circle-dashed-plus`) when no value has been selected yet — this visually distinguishes unset chips from active ones.
- Use `flex-shrink-0` on each chip so chips never compress or collapse when the row is narrow; rely on the scroll carousel instead.
- Display a human-readable summary like "3 selected" in the value segment when multiple values are chosen — never list all values inline.
- Truncate long label, operator, and value text with `truncate` and enforce `max-width` per segment so chips stay compact.
- Always include the remove button (`ti ti-x`) on chips that have a value set, so users can clear a filter in one click.

### ❌ Don't

- Do not remove the dashed border on default (unset) chips — the dashed style is a deliberate signal that the filter is available but inactive, and removing it makes the chip look broken.
- Do not allow chips to wrap to a second line — the row must stay single-height; if there are too many chips, the scroll carousel with arrow buttons handles overflow.
- Do not use Filter Chips for actions that are not filters (e.g. view-switcher tabs or bulk actions) — that role belongs to the Toggle & Segment component.
- Do not omit the `data-pinned-filter-carousel`, `data-pinned-filter-scroll`, `data-pinned-filter-front`, and `data-pinned-filter-back` data attributes — JavaScript behaviour for scroll detection depends on them.
- Do not place the value segment's text in a non-interactive `<span>` when the chip is active — it must be a `<button>` so users can click to change the value.

## Patterns & Rules

1. **Three-segment anatomy** — An active chip always follows the order: label (gray background, left-rounded) → operator (clickable, white background) → value (clickable, white background) → remove button (right-rounded). Deviating from this order breaks the visual grammar users rely on to scan multiple chips.
2. **Dashed border signals unset state** — The classes `border-dashed border-gray-300` replace the solid `border-gray-200` exactly when no operator or value has been set. Once a value is set the border becomes solid.
3. **Scroll overflow pattern** — When the chip row may exceed its container, wrap it in the carousel shell with `data-pinned-filter-carousel` and use gradient-fade + circular arrow buttons to indicate scrollability; never let the row scroll without these affordances.
4. **Max-width per segment** — Each segment enforces its own `max-width` (label: 7.5rem, operator: 6.5rem, value: 7.5rem) via inline style or utility class to prevent any single segment from consuming the full chip width.
5. **Summarise multi-select values** — When more than one value is selected, show "N selected" in the value segment rather than enumerating values. This keeps chip width predictable and avoids overflowing the toolbar row.

## Accessibility

- Each clickable segment (operator button, value button, remove button) must be a native `<button type="button">` so it receives focus and fires on Enter/Space without additional ARIA roles.
- The remove button should carry `aria-label="Remove [field name] filter"` so screen readers announce which filter is being cleared, not just a bare "×".
- Scroll arrow buttons must be reachable via Tab; when a scroll direction is unavailable (already at the start or end), the corresponding arrow button should be hidden or carry `disabled` and `aria-disabled="true"` to prevent confusing focus stops.
- The chip container row should carry `role="group"` with an `aria-label` such as "Active filters" so screen readers announce the region before reading individual chips.

## Related Components

- [Search Input](./search-input.md) — Sits alongside Filter Chips in the toolbar row and handles free-text keyword search; the two components are visually and functionally complementary but solve different filtering problems.
- [Toggle & Segment](./toggle-and-segment.md) — Used for mutually exclusive view or mode switching in the same toolbar area; unlike Filter Chips it does not carry operator/value semantics and cannot be cleared independently.
