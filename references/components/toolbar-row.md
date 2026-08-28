---
component: Toolbar Row
category: Navigation & Filtering
variants: [default-filters, active-filters, scroll-overflow-single, scroll-overflow-multiple]
related: [filter-chips, search-input]
---

# Toolbar Row

> A full-width bar that combines a filter trigger, pinned filter chips, a search input, and view-level actions into a single horizontal strip above a data list or grid.

## Overview

The Toolbar Row sits at the top of list and grid views, providing a unified surface for querying and configuring data. It is divided into three zones: a left zone for the filter button (with an optional active-filter count badge), a scrollable middle zone for pinned filter chips, and a right zone for search, column controls, and view-switcher buttons. All zones are always visible; the chip carousel scrolls independently without displacing the outer controls.

## When to Use

- Above any data table, list, or kanban board that supports column filtering and saved views.
- When users need to persist filter state as visible chips so the current query is always readable at a glance.
- When a page supports multiple view modes (e.g., List and Kanban) that the user can switch between in context.
- When the dataset is large enough that a search input and pinnable filters meaningfully reduce the result set.
- When the product team has defined at least one pinnable filter field for a given entity type.

## When NOT to Use

- For simple single-field lookups on a short static list — use [Text Input](./text-input.md) alone instead.
- As an in-form filtering mechanism inside a modal — use [Select Dropdown](./select-dropdown.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| default-filters | All pinned chips are in the dashed/empty state with no values set; use this as the initial render before any filters are applied. |
| active-filters | One or more chips carry a selected value; the filter button also renders a numeric badge showing the active filter count; use this once the user has applied at least one filter. |
| scroll-overflow-single | The chip carousel has overflowed in one direction only; a single chevron arrow appears on the overflowed side to indicate scrollability. |
| scroll-overflow-multiple | The chip carousel has overflowed in both directions; chevron arrows appear on both ends of the carousel, each fading into a gradient mask. |

## HTML Structure

```html
<!-- Toolbar Row wrapper -->
<div class="flex flex-wrap items-center justify-between gap-3 pt-2 select-none px-3 pb-2">

  <!-- Left zone: filter button -->
  <div class="flex flex-wrap items-center gap-3">

    <!-- Default state: no active filters -->
    <button class="flex items-center justify-center gap-2 whitespace-nowrap rounded-lg h-8 px-2 py-1 border border-gray-200 bg-white hover:bg-gray-50 hover:text-gray-600 text-gray-500">
      <!-- Filter icon SVG -->
      <div class="flex items-center gap-2 leading-tight">Filter</div>
    </button>

    <!-- Active state: filter with count badge -->
    <div class="flex items-center justify-center gap-2 whitespace-nowrap rounded-lg h-8 px-2 py-1 border border-gray-200 bg-white hover:bg-gray-50 hover:text-gray-600 text-gray-500 cursor-pointer">
      <!-- Filter icon SVG with badge circle -->
      <div class="flex items-center gap-2 leading-tight">
        1
        <button type="button" class="flex items-center font-medium text-gray-400 hover:text-gray-600 rounded-full">
          <i class="ti ti-x text-lg"></i>
        </button>
      </div>
    </div>

  </div>

  <!-- Middle zone: pinned filter chip carousel -->
  <div class="flex-1 pinned-filter-container overflow-x-auto overflow-y-hidden">
    <div class="flex items-center space-x-2.5 relative" data-pinned-filter-carousel>

      <!-- Left scroll arrow (visible when scrolled right) -->
      <div data-pinned-filter-front class="absolute left-0 z-10 h-9 flex items-center justify-start w-10 rounded-l-md" style="display:none; background: linear-gradient(to right, #F1F5F9 80%, transparent 100%);">
        <button type="button" class="w-8 h-8 bg-white rounded-full border border-gray-300 flex items-center justify-center transition-all duration-200 hover:border-blue-500">
          <i class="ti ti-chevron-left text-gray-600 font-medium text-2xl"></i>
        </button>
      </div>

      <!-- Scrollable chip row -->
      <div class="flex items-center gap-3 overflow-x-auto scrollbar-hide rounded-md" data-pinned-filter-scroll>

        <!-- Dashed chip (no value set) -->
        <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-dashed border-gray-300 hover:border-gray-400">
          <div class="h-full flex items-center justify-start bg-gray-50 rounded-lg max-w-50 text-gray-500 hover:text-gray-600">
            <button type="button" class="h-full px-2 text-base flex items-center truncate hover:bg-white rounded-lg space-x-2">
              <i class="ti ti-circle-dashed-plus"></i>
              <span class="truncate leading-tight font-normal">Job Category</span>
            </button>
          </div>
        </div>

        <!-- Active chip (label + operator + value + remove) -->
        <div class="border flex items-center rounded-lg h-8 divide-x divide-gray-200 bg-white w-fit flex-shrink-0 border-gray-200">
          <div class="h-full flex items-center justify-start bg-gray-50 px-2 max-w-30 rounded-l-lg">
            <span class="text-base truncate leading-tight text-gray-500">Job Priority</span>
          </div>
          <div class="max-w-26 h-full flex items-center justify-start hover:bg-gray-50">
            <button class="w-full h-full px-2 text-base flex items-center">
              <span class="truncate leading-tight text-gray-500 hover:text-gray-600">Contains</span>
            </button>
          </div>
          <div class="max-w-30 h-full flex items-center justify-start hover:bg-gray-50">
            <button class="w-full h-full px-2 text-base flex items-center">
              <span class="truncate text-gray-600 leading-tight">High</span>
            </button>
          </div>
          <button type="button" class="text-gray-500 hover:text-gray-600 hover:bg-gray-50 p-2 h-full flex items-center justify-center rounded-r-lg">
            <i class="ti ti-x text-lg"></i>
          </button>
        </div>

      </div>

      <!-- Right scroll arrow (visible when more chips overflow) -->
      <div data-pinned-filter-back class="absolute right-0 z-10 h-8 flex items-center justify-end w-10 rounded-r-md" style="background: linear-gradient(to left, #F1F5F9 80%, transparent 100%);">
        <button type="button" class="w-8 h-8 bg-white rounded-full border border-gray-300 text-gray-500 hover:text-gray-600 flex items-center justify-center transition-all duration-200 hover:border-gray-400">
          <i class="ti ti-chevron-right font-medium text-lg"></i>
        </button>
      </div>

    </div>
  </div>

  <!-- Right zone: view actions -->
  <div class="flex items-center space-x-3">

    <!-- Create New View button -->
    <button class="select-none bg-white border border-gray-200 gap-2 flex items-center justify-center px-2 h-8 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-50">
      <i class="ti ti-table-plus text-lg"></i>
      <span class="leading-tight">Create New View</span>
    </button>

    <!-- Search input -->
    <div class="relative">
      <input type="text" placeholder="Search" class="peer min-w-60 ps-9 h-8 w-full rounded-lg border bg-white pl-3 pr-8 py-1 transition-[color,box-shadow] border-gray-200 outline-none focus:border-gray-400 text-gray-600">
      <div class="text-gray-600 pointer-events-none absolute inset-y-0 start-0 flex items-center justify-center ps-3 peer-disabled:opacity-50">
        <!-- Search icon SVG -->
      </div>
    </div>

    <!-- Columns button -->
    <button class="flex items-center justify-center gap-2 text-gray-500 whitespace-nowrap rounded-lg h-8 px-2 py-1 border border-gray-200 bg-white hover:bg-gray-50 hover:text-gray-600">
      <i class="ti ti-columns-2 text-lg"></i>
      <span class="leading-tight">Columns</span>
    </button>

    <!-- View switcher (List / Kanban) -->
    <div class="flex rounded-lg bg-gray-200 h-8 p-0.5">
      <button class="px-1.5 flex items-center justify-center rounded-lg transition-all h-7 font-medium bg-white text-gray-800" title="List">
        <i class="ti ti-list text-lg"></i>
      </button>
      <button class="px-1.5 flex items-center justify-center rounded-lg transition-all h-7 font-medium hover:text-gray-600 text-gray-500" title="Kanban">
        <i class="ti ti-layout-kanban text-lg"></i>
      </button>
    </div>

  </div>

</div>
```

## Dos & Don'ts

### Do

- Always render all three zones (left, middle, right) even when the middle zone has no pinned chips; an empty carousel area maintains consistent row height.
- Show the numeric badge on the filter button whenever at least one filter has an applied value, so users can always tell how many filters are active without reading each chip.
- Use `flex-shrink-0` on every chip inside `data-pinned-filter-scroll` so chips never compress when the carousel is full.
- Limit pinned chip label text with `truncate` and `max-w-*` constraints so long field names do not break layout at narrow viewports.
- Display scroll arrows with gradient masks (`data-pinned-filter-front` / `data-pinned-filter-back`) only when actual overflow exists in that direction.

### Don't

- Do not place the Toolbar Row inside a scrollable container — it must sit flush at the top of the view at all times, or scroll arrows will behave incorrectly.
- Do not add more than one filter button to the left zone — multiple triggers create ambiguity about which set of filters each button controls.
- Do not hard-code chip widths; all chips rely on `w-fit` and `max-w-*` to fit their content while preventing overflow from breaking the row.
- Do not use solid borders on a chip that has no value; dashed `border-dashed border-gray-300` is the visual contract for "no value selected yet."
- Do not hide the right zone actions at any breakpoint where the toolbar is rendered — search and view controls are always required.

## Patterns & Rules

1. **Three-zone layout** — The toolbar always consists of left (filter trigger), middle (chip carousel), and right (search, columns, view switcher) zones separated by `justify-between`; this separation must be preserved at every viewport width.
2. **Chip state signals intent** — Dashed border (`border-dashed border-gray-300`) signals a pinned filter with no applied value; a solid border (`border-gray-200`) with a remove button signals an active filter; never mix these styles on the same chip.
3. **Carousel overflow affordance** — The `data-pinned-filter-front` and `data-pinned-filter-back` elements are toggled by scroll position; the left arrow is hidden by default (`display:none`) and revealed only when the user has scrolled right past the first chip.
4. **Filter count is authoritative** — The numeric label inside the filter button must equal the exact count of chips that currently have a value; clearing all chips must reset the button to its text-only "Filter" state without a badge.
5. **Chip carousel is independently scrollable** — `overflow-x-auto scrollbar-hide` on `data-pinned-filter-scroll` confines horizontal scrolling to the chip area only; the left and right zones must never scroll with it.

## Accessibility

- The filter button must carry `aria-label="Filter"` (or `aria-label="Filter, N active"` when filters are applied) because its label changes to a numeric count in the active state.
- Scroll arrow buttons (`data-pinned-filter-front` / `data-pinned-filter-back`) must have `aria-label="Scroll filters left"` / `aria-label="Scroll filters right"` since they contain only icon content.
- Each chip's remove button must have `aria-label="Remove [field name] filter"` so screen readers can identify which filter is being dismissed.
- Keyboard focus must cycle through the filter button, each chip's interactive segments, the scroll arrows (when visible), and then the right-zone controls in DOM order via Tab; no custom tab order is required.
- The view-switcher buttons use `title` attributes for tooltip text; supplement with `aria-pressed="true/false"` to convey the currently selected view mode to screen readers.

## Related Components

- [Filter Chips](./filter-chips.md) — The individual chip components that populate the carousel middle zone; each chip variant (dashed, active, multi-value) is documented there.
