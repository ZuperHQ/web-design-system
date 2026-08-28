---
component: Expansion Panel
category: Form & Layout
variants: [stacked, single]
related: [form-layout, drawer-panel]
---

# Expansion Panel

> A collapsible section component that shows or hides a group of related content under a labelled toggle, reducing visual clutter in dense detail views.

## Overview

The Expansion Panel renders as a bordered container with a chevron-toggle header and a body that animates open or closed via a max-height CSS transition. It is used throughout detail pages and sidebars to organise secondary information into named sections that users can reveal on demand. Multiple panels can be stacked vertically inside a shared container, each operating independently.

## When to Use

- Displaying grouped metadata fields (e.g. "Assigned To", "Customer", "Timelog Summary") in a record detail sidebar where vertical space is limited.
- Surfacing related data sets that users may not need every time, keeping the primary view uncluttered.
- Presenting section-level actions (add, edit, view) that only become relevant once a user decides to expand a section.
- Organising a long settings or configuration panel into logical, scannable labelled groups.

## When NOT to Use

- When all content must be visible at once without interaction — use [Form Layout](./form-layout.md) instead.
- When the hidden content is a full overlay or slide-in panel — use [Drawer Panel](./drawer-panel.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| stacked | Multiple `expansion-panel-item` blocks rendered sequentially inside a shared bordered container; each panel expands and collapses independently. Use when a detail view contains several distinct sections. |
| single | A single `expansion-panel-item` inside its own bordered container. Use when only one collapsible group is needed in an isolated region of the layout. |

## HTML Structure

```html
<!-- Stacked variant: shared container wrapping multiple panels -->
<div class="border border-border rounded-lg overflow-hidden">
  <div class="flex flex-col px-2 space-y-1.5 py-2">

    <!-- Panel (open state) -->
    <div class="bg-white group expansion-panel-item">
      <div class="h-9 py-1 flex items-center justify-between w-full bg-white select-none">
        <button type="button" class="expansion-toggle min-w-0 flex items-center space-x-1 pl-1 pr-1.5 py-1.5 rounded-lg hover:bg-gray-100 hover:text-gray-700 focus:outline-none text-left text-gray-700">
          <i class="ti ti-chevron-right flex-shrink-0 expansion-chevron" style="transform: rotate(90deg) translateY(0.5px) translateX(-1px);"></i>
          <span class="text-base font-medium leading-tight truncate">Section Title</span>
          <!-- Optional item count badge -->
          <span class="ml-1.5 text-md text-gray-500 shrink-0">(1)</span>
        </button>
        <!-- Hover-revealed action buttons -->
        <div class="flex items-center space-x-1 opacity-0 group-hover:opacity-100 transition-opacity">
          <button type="button" class="w-6 h-6 flex items-center justify-center rounded text-gray-500 hover:bg-gray-100 hover:text-gray-700">
            <i class="ti ti-plus text-base"></i>
          </button>
        </div>
      </div>
      <!-- Content area — add class "open" to expand -->
      <div class="expansion-content open">
        <div class="p-2 w-full">
          <!-- Panel body content goes here -->
        </div>
      </div>
    </div>

    <!-- Panel (closed state — no "open" class on expansion-content) -->
    <div class="bg-white group expansion-panel-item">
      <div class="h-9 py-1 flex items-center justify-between w-full bg-white select-none">
        <button type="button" class="expansion-toggle min-w-0 flex items-center space-x-1 pl-1 pr-1.5 py-1.5 rounded-lg hover:bg-gray-100 hover:text-gray-700 focus:outline-none text-left text-gray-700">
          <i class="ti ti-chevron-right flex-shrink-0 expansion-chevron"></i>
          <span class="text-base font-medium leading-tight truncate">Section Title</span>
        </button>
        <div class="flex items-center space-x-1 opacity-0 group-hover:opacity-100 transition-opacity">
          <button type="button" class="w-6 h-6 flex items-center justify-center rounded text-gray-500 hover:bg-gray-100 hover:text-gray-700">
            <i class="ti ti-pencil text-base"></i>
          </button>
        </div>
      </div>
      <div class="expansion-content">
        <div class="p-2 w-full">
          <!-- Panel body content goes here -->
        </div>
      </div>
    </div>

  </div>
</div>
```

## Dos & Don'ts

### Do

- Always place the `expansion-toggle` button as the direct trigger; the JavaScript listener targets this class to toggle `open` on the sibling `expansion-content`.
- Include an empty-state message inside `expansion-content` when the section has no data, so the panel body is never blank when expanded.
- Show section-level actions (add, edit, view) inside the `group-hover:opacity-100` container so they remain discoverable without cluttering the header at rest.
- Use the optional item-count badge (`text-md text-gray-500 shrink-0`) next to the label when the section aggregates a list, giving users a quick summary without expanding.
- Keep section labels short and noun-based (e.g. "Assigned To", "Customer") so they truncate gracefully at narrow widths.

### Don't

- Do not add `open` to `expansion-content` via inline style — the CSS transition relies on the class toggle to animate `max-height` from `0` to `600px`.
- Do not nest an `expansion-panel-item` inside another `expansion-panel-item` — multi-level nesting breaks the flat scannable structure the component is designed for.
- Do not remove `focus:outline-none` from `expansion-toggle` without providing a custom focus ring — the default browser outline is suppressed and must be replaced to maintain keyboard visibility.
- Do not place primary required fields inside a closed panel by default — content that users must interact with to complete a task should always be visible on load.
- Do not use the component as a navigation mechanism — each panel is for progressive disclosure of content, not for routing between views.

## Patterns & Rules

1. **Open/closed state via class** — Add the `open` class to `expansion-content` to expand the panel; remove it to collapse. The CSS transition animates `max-height` between `0` and `600px` over 250 ms, so content taller than 600 px will be clipped.
2. **Chevron rotation signals state** — When open, `expansion-chevron` is rotated 90 degrees via an inline `transform` style applied by the toggle handler; when closed the transform is cleared, pointing the chevron right.
3. **Group hover for contextual actions** — Header action buttons use `opacity-0 group-hover:opacity-100` so they are invisible at rest and revealed on hover. The `group` class must be on `expansion-panel-item`, not on the header row.
4. **Container handles visual grouping** — The outer `border border-border rounded-lg overflow-hidden` wrapper provides the card boundary; individual panels carry no border of their own, keeping the stacked layout seamless.
5. **Empty state is required** — When a panel section contains no items, render a styled empty-state row (e.g. `bg-gray-50 rounded-lg` with a `text-gray-500` message) inside `expansion-content` so users know the section loaded correctly rather than suspecting a rendering error.

## Accessibility

- The `expansion-toggle` button must have an `aria-expanded` attribute set to `"true"` when the panel is open and `"false"` when closed, so screen readers announce the current state.
- The `expansion-content` region should carry `role="region"` and an `aria-labelledby` pointing to the toggle button's id, associating the revealed content with its heading for assistive technologies.
- Keyboard interaction: **Tab** moves focus to the `expansion-toggle` button; **Enter** or **Space** activates the toggle to open or close the panel; **Tab** again moves focus into the expanded content.
- The chevron icon (`ti ti-chevron-right`) is decorative — ensure it carries `aria-hidden="true"` so screen readers do not announce the icon glyph name alongside the label text.

## Related Components

- [Form Layout](./form-layout.md) — Use when all fields must be statically visible without a show/hide interaction; Form Layout is the non-collapsible counterpart for structured data entry.
- [Drawer Panel](./drawer-panel.md) — Use when the revealed content warrants a full overlay or slide-in surface rather than inline vertical expansion within the page flow.
