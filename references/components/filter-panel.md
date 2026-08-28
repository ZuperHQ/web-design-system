---
component: Filter Panel
category: Application Layouts
variants: [default]
related: [filter-chips, toolbar-row, drawer-panel]
---

# Filter Panel

> A floating panel that lets users build, combine, and manage structured field-operator-value filter rules to narrow down a data list.

## Overview

The Filter Panel is a bordered, rounded container (typically 24rem wide) that renders a stacked list of filter rows, each composed of a field selector, an operator selector, and a value input. It sits above the list view it controls — often triggered from a toolbar button — and supports two logical grouping modes (AND / OR) toggled via a segmented control in the header. Pinned filters appear in a dedicated section at the top, separated from regular filters, and the panel displays a count of active filters next to the title.

## When to Use

- When users need to apply multiple simultaneous conditions to filter a list (e.g., Status is Open AND Priority is High).
- When the set of filterable fields is large enough that inline chips or a simple search bar would be insufficient.
- When you need to support pinned filters that persist prominently across sessions for power users.
- When users must choose a logical operator (AND / OR) to combine multiple conditions.
- When a filter must be edited in-place with a multi-step form (field → operator → value → Apply).

## When NOT to Use

- When only one or two simple filters are needed — use [Filter Chips](./filter-chips.md) instead, which are lighter and always visible without a panel overlay.
- When filtering is keyword-based only — use [Search Input](./search-input.md) instead, which is purpose-built for free-text queries.

## Variants

| Variant | Description |
|---------|-------------|
| default | The standard panel used in all list views; supports both the populated state (one or more filter rows with pinned and normal sections) and the empty state (illustrated zero-filter prompt with an Add filter CTA). |

## HTML Structure

```html
<!-- Filter Panel — default variant -->
<div class="bg-white border border-gray-200 rounded-lg overflow-hidden" style="width:24rem">

  <!-- Header -->
  <div class="flex flex-row items-center justify-between w-full px-3 py-3">
    <div class="flex items-center gap-3">
      <!-- Title with active-filter count -->
      <div class="text-lg font-medium">Filters <span>(2)</span></div>
      <!-- AND / OR logic toggle -->
      <div class="flex rounded-lg bg-gray-200 h-8 p-0.5">
        <button type="button" class="px-2 flex items-center justify-center rounded-lg h-7 font-medium text-sm bg-white text-gray-800">AND</button>
        <button type="button" class="px-2 flex items-center justify-center rounded-lg h-7 font-medium text-sm text-gray-500">OR</button>
      </div>
    </div>
    <div class="flex items-center gap-2">
      <button type="button" class="flex items-center text-base font-medium leading-tight text-blue-500 hover:bg-blue-100 rounded-md px-2 py-1.5">Clear all</button>
      <!-- Close button -->
      <button type="button" class="inline-flex items-center justify-center rounded-full p-1 hover:bg-gray-200">
        <!-- × icon -->
      </button>
    </div>
  </div>

  <!-- Scroll body -->
  <div class="flex flex-col w-full space-y-3 pb-3">

    <!-- Pinned Filters section -->
    <div class="flex flex-col w-full space-y-2.5">
      <div class="px-3 w-full flex flex-row justify-between items-center">
        <h2 class="text-base font-medium text-gray-500">Pinned Filters</h2>
        <!-- Pin count badge -->
        <span class="font-medium flex justify-center items-center text-base rounded-md border py-1 px-1.5 space-x-1 bg-blue-50 text-blue-500 border-blue-100">
          <!-- pin icon -->
          <span class="font-medium text-base leading-tight">1 / 5</span>
        </span>
      </div>
      <div class="px-3 w-full space-y-2">
        <!-- Collapsed filter row (value visible) -->
        <div class="w-full flex justify-center rounded-md items-center space-x-2 pt-3 pl-3 pr-4 pb-4 border group border-gray-200 bg-white hover:border-blue-500 cursor-default">
          <!-- Drag handle -->
          <div class="inline-flex cursor-move">
            <i class="ti ti-grip-vertical text-xl text-gray-400"></i>
          </div>
          <div class="flex flex-col w-full justify-center space-y-1">
            <!-- Row header: field label + hover actions -->
            <div class="flex items-center justify-between">
              <span class="text-base text-gray-500 leading-tight">Status</span>
              <div class="flex items-center space-x-1 mr-1 opacity-0 group-hover:opacity-100 transition-opacity duration-200">
                <!-- Pin button -->
                <button type="button" class="w-fit flex items-center justify-center cursor-pointer rounded-md p-1.5 text-gray-600"><!-- pin icon --></button>
                <!-- Delete button -->
                <button type="button" class="w-fit flex items-center justify-center cursor-pointer rounded-md p-1.5 text-red-400 hover:text-red-500 hover:bg-red-50"><!-- trash icon --></button>
              </div>
            </div>
            <!-- Collapsed value chip -->
            <div class="rounded-md border border-gray-200 cursor-pointer">
              <div class="flex items-center justify-between m-1 w-full">
                <div class="max-w-[15rem] truncate overflow-hidden">
                  <span class="ml-2 text-base leading-tight">is </span>
                  <span class="font-medium leading-tight">Open</span>
                </div>
                <div class="flex space-x-1 mr-2">
                  <button type="button" class="rounded-md text-gray-400 flex items-center p-1.5 hover:bg-gray-200 hover:text-gray-600">
                    <i class="ti ti-pencil text-xl font-normal"></i>
                  </button>
                  <button type="button" class="rounded-md text-red-400 flex items-center p-1.5 hover:bg-red-50 hover:text-red-500">
                    <i class="ti ti-x text-xl font-normal"></i>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Normal Filters section -->
    <div class="flex flex-col w-full space-y-2.5">
      <h2 class="px-3 text-base font-medium text-gray-500">Filters</h2>
      <div class="px-3 w-full space-y-2">
        <!-- Collapsed filter row (same structure as pinned row above) -->

        <!-- Edit form state (field being configured) -->
        <div class="w-full flex justify-center rounded-md items-center space-x-2 pt-3 pl-3 pr-4 pb-4 border group border-gray-200 bg-gray-50 cursor-default">
          <div class="flex flex-col w-full justify-center space-y-1">
            <div class="text-base text-red-500 opacity-0 group-hover:opacity-100 transition-opacity duration-200 flex justify-end">
              <span class="w-fit cursor-pointer mb-1 leading-tight">Remove</span>
            </div>
            <div class="flex flex-col space-y-2">
              <!-- Field selector -->
              <div class="h-9 w-full flex items-center justify-between rounded-md border border-gray-300 bg-white px-3 text-base text-gray-800 cursor-pointer">
                <span>Due Date</span>
                <i class="ti ti-chevron-down text-gray-500 text-sm"></i>
              </div>
              <!-- Operator selector -->
              <div class="h-9 w-full flex items-center justify-between rounded-md border border-gray-300 bg-white px-3 text-base text-gray-500 cursor-pointer">
                <span>is</span>
                <i class="ti ti-chevron-down text-gray-500 text-sm"></i>
              </div>
              <!-- Value selector -->
              <div class="h-9 w-full flex items-center justify-between rounded-md border border-gray-300 bg-white px-3 text-base text-gray-500 cursor-pointer">
                <span>This week</span>
                <i class="ti ti-calendar text-gray-400 text-xl"></i>
              </div>
              <!-- Apply -->
              <div class="flex cursor-pointer">
                <button type="button" class="bg-primary text-white border-none inline-flex items-center rounded-md shadow-sm focus:outline-none h-10 px-4 text-base font-medium">Apply</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Add filter button -->
    <div class="px-3">
      <button type="button" class="flex space-x-2 w-fit px-2 rounded-md py-1.5 cursor-pointer text-blue-500 hover:bg-blue-100">
        <div class="h-5 w-5 rounded-full flex justify-center items-center bg-blue-500">
          <i class="ti ti-plus text-white flex justify-center items-center text-sm"></i>
        </div>
        <span class="font-medium">Add filter</span>
      </button>
    </div>

  </div>
</div>

<!-- Empty state body (replaces scroll body when no filters exist) -->
<div class="flex flex-col justify-center space-y-2 items-center px-3 py-12">
  <i class="ti ti-adjustments-off text-gray-300 pb-2" style="font-size:3rem"></i>
  <p class="text-base text-gray-500 text-center">No filters added yet. Add a filter to narrow down your results.</p>
  <button type="button" class="flex space-x-2 w-fit mt-3 px-2 rounded-md py-1.5 cursor-pointer text-blue-500 hover:bg-blue-100">
    <div class="h-5 w-5 rounded-full flex justify-center items-center bg-blue-500">
      <i class="ti ti-plus text-white flex justify-center items-center text-sm"></i>
    </div>
    <span class="font-medium">Add filter</span>
  </button>
</div>
```

## Dos & Don'ts

### ✅ Do

- Always show the active filter count in the header title (e.g., `Filters (2)`) so users can see how many conditions are active without scrolling.
- Keep the AND / OR toggle in the header — it applies to the entire set of filters, not individual rows.
- Show the "Clear all" button only when at least one filter row exists; hide it in the empty state.
- Limit pinned filters to a maximum of 5 and display the current count as a `x / 5` badge next to the "Pinned Filters" heading.
- Use `bg-gray-50` as the background for a filter row that is in the edit/expand state to visually distinguish it from collapsed rows.

### ❌ Don't

- Don't open a new page or modal to configure a filter — the edit form (field → operator → value → Apply) must expand inline within the panel row, or it breaks the in-context editing pattern.
- Don't hide the drag handle (`ti-grip-vertical`) permanently — it must always be present on each row, as drag-to-reorder is a core interaction of this component.
- Don't place the Filter Panel inside another overlay or modal — it is already an overlay surface, and nesting it creates z-index and focus-trap conflicts.
- Don't omit the empty state illustration and prompt — a blank panel body with no affordance leaves users without a path to add their first filter.
- Don't skip the "Apply" button for filters that require value input — committing on blur causes accidental filter application and surprises the user.

## Patterns & Rules

1. **Collapsed vs. edit state** — Every filter row has two visual states: collapsed (shows field label + value chip with edit/remove icons) and edit (shows the stacked field/operator/value dropdowns on `bg-gray-50` with an Apply button). Only one row should be in the edit state at a time.
2. **Pinned vs. normal sections** — Pinned filters always render above the "Filters" section and retain their position across reloads. Regular filters can be promoted to pinned via the pin icon that appears on row hover, up to the 5-pin maximum.
3. **Logical operator scope** — The AND / OR segmented control in the header applies the selected operator between every filter row; mixed-operator logic (AND some, OR others) is not supported in this component.
4. **Drag-to-reorder** — Both pinned and normal filter rows are independently reorderable within their own section via the `ti-grip-vertical` drag handle. Dragging a pinned filter into the normal section unpins it automatically.
5. **Active count badge** — The count in `Filters (n)` reflects only applied (collapsed) filter rows; a row that is open in edit state and has not yet been Applied does not increment the count.

## Accessibility

- The panel container should have `role="dialog"` and `aria-labelledby` pointing to the "Filters" heading so screen readers announce its purpose when it opens.
- The AND / OR segmented control buttons must use `aria-pressed="true/false"` to communicate the currently selected logic mode to assistive technology.
- The close button requires `aria-label="Close filters"` since it contains only an SVG icon with no visible text.
- Focus should be trapped within the panel while it is open; pressing Escape should close the panel and return focus to the trigger element in the toolbar.
- Drag handles (`ti-grip-vertical`) should include `aria-roledescription="drag handle"` and support keyboard reordering via arrow keys as an alternative to pointer drag.

## Related Components

- [Filter Chips](./filter-chips.md) — Lightweight always-visible chips that display active filters inline below the toolbar; use as the collapsed representation of filters applied via the Filter Panel.
- [Toolbar Row](./toolbar-row.md) — The toolbar that hosts the "Filters" trigger button which opens this panel; the active filter count displayed in the toolbar button should stay in sync with the panel's header count.
