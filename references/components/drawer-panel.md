---
component: Drawer Panel
category: Overlay
variants: [full-panel, slide-in]
related: [modal-dialog, details-left-panel]
---

# Drawer Panel

> A resizable panel that slides in from the right edge of the screen to display entity detail content without navigating away from the current page.

## Overview

The Drawer Panel is a floating white card anchored to the right side of the viewport, rendered with a soft left-side shadow (`-4px 0 24px 0 rgba(0,0,0,0.12)`) and a 12px border radius to visually lift it above the page. It contains a fixed header bar with an entity icon, title, and action buttons, then a scrollable content area where entity detail components are dynamically loaded. Its primary role in the design system is to give users quick-access context on a list item without losing their place in the parent list.

## When to Use

- Previewing a work order, job, or customer record selected from a data table or list view while keeping the list visible in the background.
- Navigating between related records in sequence using prev/next controls without committing to a full-page navigation.
- Displaying a child entity reached via a breadcrumb trail (e.g., opening a contact from within a customer's panel).
- Showing a loading shimmer state while entity detail data is being fetched asynchronously.

## When NOT to Use

- When the task requires the user's full attention and the background content should be blocked — use [Modal Dialog](./modal-dialog.md) instead.
- When the detail content is a static, page-level secondary panel that is always visible as part of the layout — use [Details Left Panel](./details-left-panel.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| full-panel | A tall panel occupying the full height of the content area, used when displaying a complete entity detail view with tabs, fields, and action buttons. Choose this when the user will spend significant time interacting with the panel content. |
| slide-in | A narrower panel that animates in from the right with a CSS transform transition (`transition: transform 0.3s ease`), inset from the viewport edges by 12px. Choose this for quick-preview contexts where the panel should feel lightweight and dismissible. |

## HTML Structure

```html
<!-- Drawer Panel — slide-in variant (inset from viewport edges) -->
<div class="absolute bg-white flex flex-col"
     style="top:12px;bottom:12px;right:12px;width:22rem;border-radius:12px;
            box-shadow:-4px 0 24px 0 rgba(0,0,0,0.12),0 4px 12px 0 rgba(0,0,0,0.08);
            transition:transform 0.3s ease;overflow:hidden">

  <!-- Resize handle (left edge, col-resize cursor) -->
  <div style="position:absolute;left:0;top:0;bottom:0;width:6px;cursor:col-resize;z-index:10;"></div>

  <!-- Header — simple (no navigation) -->
  <div class="flex items-center gap-2 px-4 py-2.5 border-b border-gray-200 min-h-[52px] flex-shrink-0">
    <i class="ti ti-clipboard-list text-xl text-gray-500 flex-shrink-0"></i>
    <span class="flex-1 text-base font-semibold text-gray-900 truncate ml-1.5">WO-10432 — HVAC Inspection</span>
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 text-gray-600 flex-shrink-0" title="Open in current tab">
      <i class="ti ti-arrows-maximize text-xl"></i>
    </button>
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 text-gray-600 flex-shrink-0" title="Open in new tab">
      <i class="ti ti-external-link text-xl"></i>
    </button>
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 text-gray-600 flex-shrink-0" title="Close">
      <i class="ti ti-x text-xl"></i>
    </button>
  </div>

  <!-- Scrollable content area -->
  <div class="flex-1 overflow-hidden" style="position:relative">
    <div style="position:absolute;inset:0;overflow-y:auto" class="zuper-scrollbar p-4 space-y-3 text-base">
      <!-- Entity detail component loaded here -->
    </div>
  </div>
</div>

<!-- Header — with prev/next navigation (add inside the header bar) -->
<!--
  <div class="flex items-center gap-0.5 flex-shrink-0">
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 text-gray-600 flex-shrink-0" title="Previous">
      <i class="ti ti-chevron-up text-xl"></i>
    </button>
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 text-gray-600 flex-shrink-0" title="Next">
      <i class="ti ti-chevron-down text-xl"></i>
    </button>
  </div>
-->

<!-- Header — breadcrumb (navigated from parent entity) -->
<!--
  <div class="flex items-center gap-0.5 flex-1 overflow-hidden">
    <button class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 flex-shrink-0 cursor-pointer" title="Acme Corp">
      <i class="ti ti-user text-xl text-primary"></i>
    </button>
    <i class="ti ti-chevron-right text-xs text-gray-400 flex-shrink-0"></i>
    <i class="ti ti-clipboard-list text-xl text-gray-500 flex-shrink-0 ml-1"></i>
    <span class="text-base font-semibold text-gray-900 truncate whitespace-nowrap ml-1.5">WO-10432 — HVAC Inspection</span>
  </div>
-->

<!-- Loading shimmer state (replaces content area) -->
<!--
  <div class="flex flex-col px-4 pt-4 gap-4 overflow-hidden animate-pulse">
    <div class="flex gap-3 pb-2 border-b border-gray-100">
      <div class="h-5 w-20 bg-gray-200 rounded"></div>
      <div class="h-5 w-24 bg-gray-200 rounded"></div>
    </div>
    <div class="flex items-center gap-3 pt-1">
      <div class="h-12 w-12 bg-gray-200 rounded-full flex-shrink-0"></div>
      <div class="flex flex-col gap-1.5 flex-1">
        <div class="h-4 w-[55%] bg-gray-200 rounded"></div>
        <div class="h-3 w-[35%] bg-gray-200 rounded"></div>
      </div>
    </div>
  </div>
-->
```

## Dos & Don'ts

### Do

- Always include the 6px resize handle div on the left edge so users can adjust the panel width.
- Use the `zuper-scrollbar` class on the inner scroll container to keep scrollbar styling consistent with the design system.
- Include at minimum the close (`ti-x`) button in every header so users always have a clear dismiss path.
- Use `animate-pulse` on the shimmer skeleton while data loads rather than showing an empty or partially populated panel.
- Apply `border-b border-gray-200` to the header to visually separate it from the scrollable content area.

### Don't

- Do not place the drawer outside a `position:relative` container — it uses absolute positioning and will escape its intended bounds if the parent stacking context is not set.
- Do not omit the `flex-shrink-0` class from header elements — without it, long entity titles collapse action buttons out of view.
- Do not use the drawer for destructive multi-step workflows such as delete confirmations — this breaks user expectations for a lightweight preview surface.
- Do not hard-code a fixed width without allowing the resize handle to function — this removes a key usability affordance for users on smaller screens.
- Do not stack multiple open drawers simultaneously without a clear breadcrumb trail in the header — users lose navigation context.

## Patterns & Rules

1. **Header height is always 52px minimum** — The `min-h-[52px]` constraint on the header ensures consistent vertical alignment of icon, title, and action buttons regardless of title length. Titles that exceed available width truncate with `truncate` and never wrap to a second line.
2. **Shadow defines elevation, not a backdrop** — The drawer uses a directional box-shadow (`-4px 0 24px 0 rgba(0,0,0,0.12), 0 4px 12px 0 rgba(0,0,0,0.08)`) instead of a backdrop overlay, so the background page remains interactive while the panel is open.
3. **Slide-in animation uses transform only** — The `drawer-demo-closed` class applies `transform: translateX(calc(100% + 12px))` to slide the panel off-screen; toggling this class drives the `transition: transform 0.3s ease` animation. Do not animate `left`/`right` properties, as they cause layout recalculations.
4. **Breadcrumb header replaces prev/next controls** — When the drawer is opened by following a relationship link from a parent entity, use the breadcrumb header variant (parent icon + chevron-right + current icon + title) instead of prev/next navigation, because there is no sibling list to traverse.
5. **Content area uses an inner absolute scroll container** — The `flex-1 overflow-hidden` outer div combined with an inner `position:absolute;inset:0;overflow-y:auto` div ensures the scrollable region fills exactly the remaining height below the header without causing the panel itself to grow or scroll.

## Accessibility

- The panel root element should carry `role="dialog"` and `aria-modal="false"` (the background remains interactive, so this is not a true modal).
- Add `aria-label` or `aria-labelledby` referencing the header title `<span>` so screen readers announce the panel's subject on focus entry.
- The close button must have `title="Close"` and an equivalent `aria-label="Close"` attribute; pressing Escape should trigger the same close action.
- Prev/next navigation buttons require `aria-label="Previous record"` and `aria-label="Next record"` respectively — chevron icons alone convey no meaning to assistive technology.
- The resize handle div should have `role="separator"` and `aria-orientation="vertical"` so screen readers expose it as a resizable boundary rather than an empty interactive region.

## Related Components

- [Modal Dialog](./modal-dialog.md) — Use instead of the Drawer Panel when the user must complete an action or confirm a decision before returning to the background page; unlike the drawer, the modal blocks background interaction with a backdrop overlay.
- [Details Left Panel](./details-left-panel.md) — A persistent, always-visible secondary panel used for layout-level detail views; unlike the Drawer Panel, it does not slide in on demand and is part of the page structure rather than a temporary overlay.
