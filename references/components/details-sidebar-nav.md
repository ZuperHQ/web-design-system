---
component: Details Right Sidebar Nav
category: Application Layouts
variants: [panel-open, panel-closed]
related: [details-left-panel, sidebar-nav, tab-bar, details-center-panel, details-page-layout]
---

# Details Right Sidebar Nav

> A collapsible icon strip docked to the right edge of a detail view that lets users switch between contextual panels — such as Attachments, Activity, or Workflows — without leaving the current record.

## Overview

The Details Sidebar Nav is a narrow vertical strip of icon buttons that sits on the right side of a record detail layout. Each icon represents a contextual panel; clicking one opens that panel to the left of the strip while the active icon receives a filled brand-color highlight (`bg-[#FCEDE8] text-[#1E293B]`). The strip also contains two pinned utility actions at the bottom — a Customize control and a collapse/expand toggle — giving users control over the sidebar's open state without losing their place in the record.

## When to Use

- On record detail pages (jobs, work orders, customers) where multiple contextual sections — attachments, activity feed, status history, assignments — need to be accessible without stacking them all in a single scroll column.
- When vertical space is at a premium and the main detail content should remain the dominant focus while secondary panels are available on demand.
- When the set of visible panels is user-customizable, since the Customize icon at the bottom of the strip supports panel reordering or visibility toggling.
- When the layout already uses a left-anchored main content area and you need a right-anchored supplemental navigation mechanism to balance it.
- When collapsibility is needed so power users can maximize the main content area by hiding the panel entirely with a single click.

## When NOT to Use

- When navigating between top-level pages or app sections — use [Sidebar Nav](./sidebar-nav.md) instead, which is designed for primary application-level navigation.
- When the secondary content sections are few (two or fewer) and always visible — use [Tab Bar](./tab-bar.md) instead, which offers horizontal tabs without the need for a collapsible sidebar mechanism.
- When the context is a modal or drawer rather than a full detail page — embedding this component inside an overlay creates unnecessary nesting complexity; use a flat [Tab Bar](./tab-bar.md) within the modal.

## Variants

| Variant | Description |
|---------|-------------|
| panel-open | The content panel is visible to the left of the icon strip; the active nav icon is highlighted in the brand color. Use this as the default loaded state when a record is first opened so users immediately see contextual content. |
| panel-closed | Only the icon strip is rendered; no content panel is shown. Use this when maximizing the main record content area is the priority, or when the user has explicitly collapsed the sidebar. This is the only state used inside the Full Details Page Layout — the right sidebar is always collapsed there. |

## HTML Structure

```html
<!-- Outer layout: content panel + icon nav strip side by side -->
<div class="flex border border-gray-200 rounded-lg overflow-hidden">

  <!-- Content panel (panel-open variant only; omit when panel is closed) -->
  <div class="overflow-hidden bg-white" style="width:24rem">
    <div class="h-full overflow-y-auto">
      <!-- Panel header -->
      <div class="border-b border-gray-200 px-4 py-2.5">
        <h6 class="text-lg font-medium text-gray-800 truncate">Attachments</h6>
      </div>
      <!-- Panel body content goes here -->
      <div class="p-3 space-y-2">
        <!-- Example attachment row -->
        <div class="flex items-center gap-3 p-2 rounded-lg hover:bg-gray-50 cursor-pointer group">
          <div class="h-9 w-9 rounded-lg bg-red-50 flex items-center justify-center shrink-0">
            <i class="ti ti-file-type-pdf text-xl text-red-500"></i>
          </div>
          <div class="flex-1 min-w-0">
            <div class="text-base text-gray-800 truncate leading-tight font-medium">filename.pdf</div>
            <div class="text-md text-gray-400 leading-tight">2.4 MB · Jun 12, 2026</div>
          </div>
          <button type="button" class="h-7 w-7 flex items-center justify-center rounded-md text-gray-400 hover:text-gray-600 hover:bg-gray-100 opacity-0 group-hover:opacity-100 transition-opacity">
            <i class="ti ti-dots-vertical text-lg"></i>
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Icon nav strip (always present) -->
  <div class="border-l overflow-y-auto overflow-x-hidden bg-white">
    <nav aria-label="Details Sidebar" class="px-1 py-2 flex flex-col h-full">

      <!-- Primary nav icons -->
      <div class="relative flex flex-col text-center flex-1 space-y-2">

        <!-- Active state -->
        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer bg-[#FCEDE8] text-[#1E293B]" title="Attachments">
          <i class="ti ti-paperclip text-xl"></i>
        </div>

        <!-- Inactive state -->
        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:text-gray-700 hover:bg-gray-100" title="Activity">
          <i class="ti ti-activity text-xl"></i>
        </div>

        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:text-gray-700 hover:bg-gray-100" title="Status History">
          <i class="ti ti-history text-xl"></i>
        </div>

        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:text-gray-700 hover:bg-gray-100" title="Assigned To">
          <i class="ti ti-users text-xl"></i>
        </div>

        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:text-gray-700 hover:bg-gray-100" title="Workflows">
          <i class="ti ti-git-branch text-xl"></i>
        </div>
      </div>

      <!-- Utility actions (Customize + Collapse/Expand toggle) -->
      <div class="text-center mt-auto flex flex-col items-center gap-1">
        <div class="mx-auto inline-flex h-8 w-8 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:text-gray-700 hover:bg-gray-100" title="Customize">
          <i class="ti ti-adjustments-horizontal text-xl"></i>
        </div>
        <!-- panel-open: collapse icon -->
        <div class="mx-auto inline-flex h-9 w-9 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-700 hover:bg-gray-100" title="Collapse">
          <i class="ti ti-layout-sidebar-right-collapse text-xl"></i>
        </div>
        <!-- panel-closed: expand icon (swap in when panel is closed) -->
        <!-- <div class="mx-auto inline-flex h-9 w-9 flex-shrink-0 items-center justify-center rounded-lg cursor-pointer text-gray-500 hover:bg-gray-100" title="Expand">
          <i class="ti ti-layout-sidebar-right-expand text-xl"></i>
        </div> -->
      </div>

    </nav>
  </div>

</div>
```

## Dos & Don'ts

### Do

- Always provide a `title` attribute on every nav icon so a tooltip identifies the panel on hover for users who cannot read icon-only labels.
- Apply the active state classes (`bg-[#FCEDE8] text-[#1E293B]`) to exactly one icon at a time so the current open panel is unambiguous.
- Keep the Customize and collapse/expand icons pinned to the bottom of the strip (`mt-auto`) so they are consistently reachable regardless of how many panel icons are above them.
- Swap the collapse icon (`ti-layout-sidebar-right-collapse`) for the expand icon (`ti-layout-sidebar-right-expand`) when the panel is closed, and vice versa, so the toggle communicates the available action rather than the current state.
- Use `overflow-y-auto` on both the content panel and the icon strip independently so each scrolls on its own axis when content exceeds the container height.
- In the Full Details Page Layout, always render the right sidebar in the `panel-closed` (icon-strip-only) state at `width:3rem`. Never expand the content panel within that layout.

### Don't

- Do not apply the active highlight to the Customize or collapse/expand icons — those are utility actions, not panel selectors, and highlighting them misleads users about which panel is open.
- Do not remove the `border-l` separator between the content panel and the icon strip; without it the two regions blur together and the strip loses its distinct identity.
- Do not place more than seven or eight icons in the primary nav area without providing scroll or overflow handling — the strip has a fixed height and icons will clip off screen without `overflow-y-auto`.
- Do not replace `title` attributes with tooltip components that require JavaScript if the icon strip is the only affordance for identifying panel names; accessible tooltips or `aria-label` must still be present.
- Do not render the content panel `div` as an empty container when the panel is closed — remove it from the DOM entirely so the strip occupies the full right edge and `justify-end` alignment works correctly.
- Do not render the content panel inside the Full Details Page Layout; only the icon strip (`width:3rem`) is shown there.

## Patterns & Rules

1. **Single active icon** — Only one icon in the primary nav section may carry the active state at a time. Clicking an already-active icon does not deactivate it; instead, use the collapse toggle at the bottom to hide the panel while preserving which section was last open.
2. **Panel width is fixed** — The content panel uses a fixed width of `24rem` (class `style="width:24rem"` or `w-96`) to prevent layout reflow when switching between panels. Do not make this width dynamic based on content.
3. **Utility icons are always inactive** — The Customize (`ti-adjustments-horizontal`) and collapse/expand icons at the bottom of the strip never receive the brand-color active treatment; they are always styled as `text-gray-500` in the closed state and `text-gray-700` in the open state for the collapse icon only.
4. **Icon strip stays visible when panel is closed** — When the user collapses the panel, the icon strip remains visible against the right edge of the layout (`justify-end` on the outer container). This preserves one-click access to re-open any panel.
5. **Customize icon opens panel reordering** — The `ti-adjustments-horizontal` icon at the bottom of the strip should always trigger a customization flow (reorder, show/hide panels). Do not repurpose it for unrelated settings actions.
6. **Width in full layout** — When embedded in `#details-page-layout`, the sidebar uses `width:3rem; flex-shrink:0` (icon strip only). The `24rem` content panel is only ever shown in the standalone sidebar (e.g., in a dedicated attachments drawer).

## Accessibility

- The `<nav>` element must carry `aria-label="Details Sidebar"` to distinguish it from other navigation landmarks on the page.
- Each icon button must have a `title` attribute (or `aria-label`) matching the panel name it opens, since the icon strip contains no visible text labels.
- Keyboard users must be able to Tab through all icon buttons in order; the active icon should also be reachable and activatable with Enter or Space.
- When the panel opens or closes, focus should remain on the toggle icon that triggered the change so the user does not lose their position in the keyboard sequence.
- Icon elements (`<i>`) are decorative and should have `aria-hidden="true"` when a parent button already carries an `aria-label`; this prevents screen readers from announcing raw icon class names.

## Related Components

- [Sidebar Nav](./sidebar-nav.md) — The primary application navigation strip; use it for top-level page routing rather than in-record panel switching.
- [Tab Bar](./tab-bar.md) — Horizontal tab navigation for switching between sections within a page; prefer it over Details Right Sidebar Nav when the panels are always visible and collapsibility is not required.
- [Full Details Page Layout](./details-page-layout.md) — The three-column shell that embeds this component in its `panel-closed` state as the right edge of the layout.
