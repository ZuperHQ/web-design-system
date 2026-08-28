---
component: Reorderable List
category: Application Layouts
variants: [with-toggles, items-only]
related: [kanban-column]
---

# Reorderable List

> A floating panel that lets users drag items into a custom order, optionally toggling each item's visibility, so they can personalise how content is arranged in the UI.

## Overview

The Reorderable List is a compact, bordered panel containing a scrollable list of drag-and-drop rows, each marked by a grip handle icon. It sits in the Application Layouts category and is used wherever a user needs to persistently customise the order or visibility of named items — such as tabs, columns, or sort criteria. A header with a close button and a footer "Reset to default" action bracket the list, giving users a clear entry and exit point.

## When to Use

- Letting users reorder tabs on a detail page (e.g. customising which tab appears first).
- Allowing users to show or hide individual tabs or panels within a view via per-row toggle controls.
- Configuring the priority order of sort criteria applied to a list or table.
- Surfacing a "Customize" panel triggered by a toolbar action where user preference must be saved across sessions.
- Presenting a small, bounded set of named items (typically 3–12) that benefit from manual sequencing.

## When NOT to Use

- When you need to visually arrange card-based content across status columns — use [Kanban Column](./kanban-column.md) instead.
- When sorting is a one-click, non-persistent action — use [Toolbar Row](./toolbar-row.md) sort controls instead.
- When the list exceeds a manageable scrollable length and items carry complex metadata — use [Tables](./tables.md) with column reordering instead.

## Variants

| Variant | Description |
|---------|-------------|
| with-toggles | Use when each item can be independently shown or hidden in addition to being reordered; each row carries a pill toggle indicating the item's active state. |
| items-only | Use when visibility is fixed and only the sequence matters; rows display a label and an optional secondary descriptor (e.g. sort direction) with no toggle control. |

## HTML Structure

```html
<!-- Reorderable List — with-toggles variant -->
<div class="select-none w-64 bg-white border border-border rounded-lg shadow-lg flex flex-col">

  <!-- Header -->
  <div class="flex items-center justify-between px-2.5 py-2 border-b border-border">
    <span class="text-base font-medium text-gray-700">Customize Tab</span>
    <button type="button" class="h-5 w-5 flex items-center justify-center rounded-md hover:bg-gray-100 text-gray-500 hover:text-gray-800 cursor-pointer">
      <i class="ti ti-x text-lg"></i>
    </button>
  </div>

  <!-- Drop list -->
  <div class="flex flex-col space-y-1.5 overflow-y-auto max-h-80 px-1.5 py-2 zuper-scrollbar">

    <!-- Item — toggle OFF (item hidden) -->
    <div class="flex items-center p-1.5 rounded-lg gap-x-3 hover:bg-gray-50 group/item cursor-default">
      <i class="ti ti-grip-vertical group-hover/item:text-gray-800 cursor-grab text-base flex-shrink-0 text-gray-500"></i>
      <div class="flex-1 min-w-0">
        <span class="text-md truncate leading-tight group-hover/item:text-gray-800 block text-gray-500">Tasks</span>
      </div>
      <!-- Toggle OFF: bg-gray-200, thumb at translate-x-[3px] -->
      <button type="button" class="relative inline-flex flex-shrink-0 items-center rounded-full transition-colors duration-200 cursor-pointer bg-gray-200" style="width:32px;height:18px">
        <span class="inline-block rounded-full bg-white shadow transform transition-transform duration-200 translate-x-[3px]" style="width:14px;height:14px"></span>
      </button>
    </div>

    <!-- Item — toggle ON (item visible) -->
    <div class="flex items-center p-1.5 rounded-lg gap-x-3 hover:bg-gray-50 group/item cursor-default">
      <i class="ti ti-grip-vertical group-hover/item:text-gray-800 cursor-grab text-base flex-shrink-0 text-gray-600"></i>
      <div class="flex-1 min-w-0">
        <span class="text-md truncate leading-tight group-hover/item:text-gray-800 block text-gray-600">Line Items</span>
      </div>
      <!-- Toggle ON: bg-gray-700, thumb at translate-x-[15px] -->
      <button type="button" class="relative inline-flex flex-shrink-0 items-center rounded-full transition-colors duration-200 cursor-pointer bg-gray-700" style="width:32px;height:18px">
        <span class="inline-block rounded-full bg-white shadow transform transition-transform duration-200 translate-x-[15px]" style="width:14px;height:14px"></span>
      </button>
    </div>

  </div>

  <!-- Footer -->
  <div class="border-t border-border p-1">
    <button type="button" class="w-full flex items-center justify-center gap-x-2 text-md text-gray-600 hover:text-gray-800 px-1 py-1.5 rounded-md hover:bg-gray-50 cursor-pointer">
      <i class="ti ti-refresh text-base"></i>
      Reset to default
    </button>
  </div>

</div>

<!-- Reorderable List — items-only variant -->
<div class="select-none w-64 bg-white border border-border rounded-lg shadow-lg flex flex-col">

  <!-- Header -->
  <div class="flex items-center justify-between px-2.5 py-2 border-b border-border">
    <span class="text-base font-medium text-gray-700">Sort Order</span>
    <button type="button" class="h-5 w-5 flex items-center justify-center rounded-md hover:bg-gray-100 text-gray-500 hover:text-gray-800 cursor-pointer">
      <i class="ti ti-x text-lg"></i>
    </button>
  </div>

  <!-- Drop list — no toggles -->
  <div class="flex flex-col space-y-1.5 px-1.5 py-2">

    <div class="flex items-center p-1.5 rounded-lg gap-x-3 hover:bg-gray-50 group/item cursor-default">
      <i class="ti ti-grip-vertical group-hover/item:text-gray-800 cursor-grab text-base flex-shrink-0 text-gray-600"></i>
      <div class="flex-1 min-w-0">
        <span class="text-md truncate leading-tight group-hover/item:text-gray-800 block text-gray-600">Due Date</span>
        <span class="text-sm truncate leading-tight block text-gray-400">Ascending</span>
      </div>
    </div>

    <div class="flex items-center p-1.5 rounded-lg gap-x-3 hover:bg-gray-50 group/item cursor-default">
      <i class="ti ti-grip-vertical group-hover/item:text-gray-800 cursor-grab text-base flex-shrink-0 text-gray-600"></i>
      <div class="flex-1 min-w-0">
        <span class="text-md truncate leading-tight group-hover/item:text-gray-800 block text-gray-600">Priority</span>
        <span class="text-sm truncate leading-tight block text-gray-400">Descending</span>
      </div>
    </div>

  </div>

  <!-- Footer -->
  <div class="border-t border-border p-1">
    <button type="button" class="w-full flex items-center justify-center gap-x-2 text-md text-gray-600 hover:text-gray-800 px-1 py-1.5 rounded-md hover:bg-gray-50 cursor-pointer">
      <i class="ti ti-refresh text-base"></i>
      Reset to default
    </button>
  </div>

</div>
```

## Dos & Don'ts

### ✅ Do

- Always include the header with a descriptive title and a close (`ti-x`) button so users know what they are configuring and can dismiss the panel.
- Use `select-none` on the root element to prevent accidental text selection during drag operations.
- Apply `group/item` and the corresponding `group-hover/item:` utilities on the row and its children so the grip handle and label react as a unit on hover.
- Include the footer "Reset to default" action whenever user-defined order can deviate from a system default.
- Use `overflow-y-auto` and `max-h-80` with `zuper-scrollbar` on the drop list when the item count may exceed the visible area.

### ❌ Don't

- Don't omit the `ti-grip-vertical` icon — removing it breaks the affordance that tells users the row is draggable.
- Don't mix items-only and with-toggles rows in the same list — inconsistent controls within a single panel create confusion about what each row's interaction does.
- Don't use this component as an inline, always-visible widget embedded in a page layout — it is designed as a floating panel triggered on demand, and persistent inline placement disrupts reading flow.
- Don't exceed the `w-64` container width without a deliberate layout reason; the panel is intentionally compact to overlay content non-destructively.
- Don't skip the `cursor-grab` class on the grip icon — without it there is no pointer cue that the row can be dragged.

## Patterns & Rules

1. **Toggle state encoding** — An OFF toggle uses `bg-gray-200` with the thumb at `translate-x-[3px]`; an ON toggle uses `bg-gray-700` with the thumb at `translate-x-[15px]`. Always pair the background colour change with the thumb translation so the state is readable without colour alone.
2. **Disabled-like label colour for hidden items** — When a row's toggle is OFF, its label and grip icon use `text-gray-500` instead of `text-gray-600` to visually de-emphasise items that are not currently shown.
3. **Scrollable vs. static drop list** — Add `overflow-y-auto max-h-80 zuper-scrollbar` to the drop list only in the with-toggles variant or whenever the item count is variable; for the items-only variant with a small fixed count, the plain `flex flex-col space-y-1.5 px-1.5 py-2` list without scroll constraints is sufficient.
4. **Footer is always present** — Every Reorderable List must include the footer reset button, providing an escape hatch if the user's custom order becomes unwieldy.
5. **Panel width is fixed at `w-64`** — The component is designed for a consistent 256 px width across all usages; do not make it fluid or stretch it to fill a parent container.

## Accessibility

- The root container must carry `role="listbox"` or the drag-and-drop library's equivalent ARIA role; each draggable row should carry `role="option"` and `aria-grabbed` to communicate drag state.
- Keyboard interaction must support `Tab` to focus rows, `Space` to pick up and release a row, and `ArrowUp`/`ArrowDown` to move a grabbed row within the list.
- Each toggle button must have an `aria-label` that names the item and its current state (e.g. `aria-label="Tasks, hidden"` / `aria-label="Line Items, visible"`) so screen readers convey both the item identity and its on/off status without relying on visual toggle position.

## Related Components

- [Kanban Column](./kanban-column.md) — Shares the drag-and-drop interaction model but operates on card-based data across status lanes rather than on a list of named configuration items.
