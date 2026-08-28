---
component: Full Details Page Layout
category: Application Layouts
variants: [left-expanded, left-collapsed, both-panels-open]
related: [details-left-panel, details-center-panel, details-right-sidebar-nav]
---

# Full Details Page Layout

> The three-column shell that composes the Details Left Panel, Details Center Panel, and Details Right Sidebar Nav into a single record detail view.

## Overview

The Full Details Page Layout is a `flex flex-row overflow-hidden` container that fills the viewport height and arranges three columns side by side: the Details Left Panel on the left, the Details Center Panel in the centre, and the Details Right Sidebar Nav on the right. The right sidebar is always rendered in its collapsed, icon-strip-only state (`width:3rem`) within this layout. The left panel can toggle between expanded (`22rem`) and collapsed (`3.5rem`). When the user opens a right sidebar content panel, the right region widens to include a `24rem` content panel alongside the `3rem` icon strip.

## When to Use

- When building any record detail page (work order, customer, property, invoice) that requires all three columns — record identity on the left, tabbed content in the centre, contextual panels on the right.
- When the record warrants a persistent left panel for identity and field data plus a centre area for tabbed content exploration.

## When NOT to Use

- For list or table views, dashboards, or settings pages that do not follow the three-column detail pattern.
- When only two columns are needed — compose the Details Left Panel and Details Center Panel directly without this layout wrapper.

## Variants

| Variant | Description |
|---------|-------------|
| left-expanded | Left panel at `22rem`, centre panel `flex-1`, right sidebar icon strip `3rem`. Default state when a record is first opened. |
| left-collapsed | Left panel collapses to `3.5rem` (expand toggle only), centre panel expands to fill, right sidebar icon strip `3rem`. Use when the user collapses the left panel to maximise the centre content area. |
| both-panels-open | Left panel `22rem`, centre panel `flex-1`, right side = attachments content panel `24rem` + icon strip. Use when the user opens a right sidebar content panel. |

## HTML Structure

```html
<!-- Outer shell: flex row, full height, overflow clipped -->
<div class="flex flex-row overflow-hidden border border-gray-200 rounded-lg bg-theme-light" style="height:580px">
  <!-- In production use h-screen or h-full instead of a fixed height -->

  <!-- Left panel: expanded (left-expanded variant) -->
  <div class="flex flex-col bg-white border-r border-gray-200 flex-shrink-0 overflow-hidden" style="width:22rem">
    <!-- See Details Left Panel for inner markup -->
  </div>

  <!-- Left panel: collapsed (left-collapsed variant — swap in place of expanded) -->
  <!--
  <div class="flex flex-col items-center justify-start pt-3 bg-white border-r border-gray-200 flex-shrink-0" style="width:3.5rem">
    <button type="button"
      class="h-8 w-8 flex items-center justify-center rounded-lg text-gray-500 hover:text-gray-700 hover:bg-gray-100 cursor-pointer"
      title="Expand panel"
      aria-expanded="false">
      <i class="ti ti-chevron-right text-xl"></i>
    </button>
  </div>
  -->

  <!-- Centre column: always flex-1 min-w-0 -->
  <div class="flex-1 min-w-0 flex flex-col overflow-hidden">
    <!-- See Details Center Panel for inner markup -->
  </div>

  <!-- Right sidebar: icon strip only (left-expanded and left-collapsed variants) -->
  <div class="flex-shrink-0 bg-white border-l border-gray-200 overflow-y-auto overflow-x-hidden" style="width:3rem">
    <!-- See Details Right Sidebar Nav (panel-closed) for inner markup -->
  </div>

  <!-- Right sidebar: content panel open (both-panels-open variant — swap in place of icon-strip-only) -->
  <!--
  <div class="flex flex-row flex-shrink-0 bg-white border-l border-gray-200 overflow-hidden">
    <div class="overflow-hidden bg-white" style="width:24rem">
      <div class="h-full overflow-y-auto">
        <!- - Panel header - ->
        <div class="border-b border-gray-200 px-4 py-2.5">
          <h6 class="text-lg font-medium text-gray-800 truncate">Attachments</h6>
        </div>
        <!- - Panel body - ->
        <div class="p-3 space-y-2">
          <!- - attachment rows … - ->
        </div>
      </div>
    </div>
    <div class="border-l border-gray-200 overflow-y-auto overflow-x-hidden bg-white" style="width:3rem">
      <!- - Icon strip (same as panel-closed) - ->
    </div>
  </div>
  -->

</div>
```

## Dos & Don'ts

### Do

- Use `flex-1 min-w-0` for the centre column so it fills whatever space remains between the left panel and right sidebar as those columns resize.
- Always render the right sidebar as `width:3rem` (icon strip only) in this layout; a full sidebar content panel belongs in the both-panels-open variant's right region.
- Apply `overflow-hidden` to the outer container and to each column independently so columns do not bleed into each other during transitions.
- Use `bg-theme-light` as the `background-color` of the outer container — it is the "gutter" color visible between panels during a width transition.
- Animate left-panel expand/collapse with `transition-all duration-200` on the panel's `width` so the centre column expands smoothly as a flex sibling.

### Don't

- Never use `position:absolute` for any of the three columns — all columns use the flex row layout.
- Do not set a fixed width on the centre column; it must always be `flex-1 min-w-0`.
- Do not expand the right sidebar content panel inside this layout's main flow — only the icon strip is always present here; the content panel opens as an additional flex child in the both-panels-open variant.
- Do not use `h-screen` in the design-system demo container — use `style="height:580px"` there; reserve `h-screen` or `h-full` for production.

## Patterns & Rules

1. **Column widths** — Left expanded: `22rem`. Left collapsed: `3.5rem`. Centre: `flex-1 min-w-0`. Right icon strip: `3rem`. Right content panel (both-panels-open only): `24rem` + `3rem` icon strip alongside it.
2. **Right sidebar is always collapsed** — Within this layout the icon strip is always the outermost right element at `3rem`. Opening a right panel adds a `24rem` content div to the left of the strip, keeping the strip at its fixed position.
3. **Height** — In the design-system demo use `style="height:580px"` on the outer container. In production use `h-screen` or `h-full` so the layout fills the viewport.
4. **Border separators** — Left panel: `border-r border-gray-200`. Right sidebar: `border-l border-gray-200`. The centre column has no explicit border — it relies on the neighbouring panels' borders for visual separation.
5. **Left-panel collapse transition** — Apply `transition-all duration-200` to the left panel element so the width change animates smoothly. The centre column expands automatically because it is a `flex-1` sibling; no additional animation is needed there.

## Accessibility

- Wrap the left panel in an `<aside>` element and the centre column in a `<main>` element so landmark regions are correctly identified by assistive technologies.
- The left panel's collapse toggle must carry `aria-expanded="true|false"` reflecting the current open/closed state.
- The right sidebar `<nav>` must carry `aria-label="Details Sidebar"` to distinguish it from other navigation landmarks on the page.
- When the left panel collapses or expands, announce the change via an `aria-live="polite"` region or by moving focus to the toggle button so keyboard users are not disoriented.

## Related Components

- [Details Left Panel](./details-left-panel.md) — The left column providing record identity, status, quick actions, and accordion field data.
- [Details Center Panel](./details-center-panel.md) — The centre column with tabbed navigation and structured content sections.
- [Details Right Sidebar Nav](./details-sidebar-nav.md) — The right icon strip for switching contextual panels; always in `panel-closed` state within this layout.
