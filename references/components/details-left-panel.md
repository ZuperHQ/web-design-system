---
component: Details Left Panel
category: Application Layouts
variants: [default, with-cover-image, loading, collapsed]
related: [details-sidebar-nav, expansion-panel, breadcrumb, details-center-panel, details-page-layout]
---

# Details Left Panel

> A fixed-width left panel that surfaces a record's identity, status, quick actions, and structured field data in a single scrollable column on detail pages.

## Overview

The Details Left Panel is a `25rem`-wide vertical container that anchors the left side of a record detail view. It consists of a sticky header zone — containing the record avatar, title, status badge, location, and a row of quick-action buttons — followed by a scrollable body of collapsible accordion sections (Job Details, Description, Related Records, Other Details). Its role in the design system is to give every record type a consistent identity surface while keeping the main content area free for tabs and data panels.

## When to Use

- Displaying a work order, customer, property, or any record that has a primary identity (name/ID), a lifecycle status, and multiple sections of structured fields.
- When the user needs quick access to actions (status change, schedule, email, call, note) without leaving the record context.
- When a record has related sub-records (e.g., Properties linked to a Work Order) that should be browsable inline without full navigation.
- When field data is dense enough to warrant accordion grouping — splitting primary fields, description, and custom fields into separate expandable sections.
- As the left column in a two-column detail layout alongside a tabbed content area or a Details Sidebar Nav.

## When NOT to Use

- For brief, single-purpose flyouts or contextual previews — use [Drawer Panel](./sidebar-nav.md) instead, which is designed for temporary overlay contexts.
- When only a flat list of key-value fields is needed without identity, status, or actions — use [Form Layout](./form-layout.md) instead.
- When the record has no meaningful grouped sections; a single accordion with no collapsing behaviour adds unnecessary chrome.

## Variants

| Variant | Description |
|---------|-------------|
| default | Standard panel with avatar, title, status badge, action buttons, and accordion body sections. Use for all records that do not have an associated cover image. |
| with-cover-image | Prepends a `9rem`-tall cover image strip above the header, with view/edit/delete overlay controls. Use when a record type (e.g., property, asset) supports a representative photo. |
| loading | Replaces all content with `animate-pulse` shimmer blocks at the same structural positions. Use while the record data fetch is in flight to prevent layout shift. |
| collapsed | Panel shrinks to a `3.5rem`-wide strip containing only a `ti-chevron-right` expand-toggle button centred vertically at the top. Use this state in the full details page layout when the user has collapsed the left panel to maximise the centre content area. |

## HTML Structure

```html
<!-- Root panel: fixed width, full height, flex column, clipped overflow -->
<div class="bg-white border border-border flex flex-col overflow-hidden" style="width:25rem; border-radius:4px">

  <!-- [with-cover-image variant only] Cover image strip -->
  <div class="w-full shrink-0 overflow-hidden relative" style="height:9rem">
    <img src="..." alt="..." class="w-full h-full object-cover" />
    <!-- Hover controls (view / edit / delete) -->
    <div class="absolute right-0 top-0 pr-2 pt-2 flex items-center space-x-1.5">
      <button type="button" class="w-7 h-7 flex items-center justify-center rounded-lg border border-gray-200 bg-white text-gray-500 shadow-sm cursor-pointer">
        <i class="ti ti-eye text-base"></i>
      </button>
      <button type="button" class="w-7 h-7 flex items-center justify-center rounded-lg border border-gray-200 bg-white text-gray-500 shadow-sm cursor-pointer">
        <i class="ti ti-photo-edit text-base"></i>
      </button>
      <button type="button" class="w-7 h-7 flex items-center justify-center rounded-lg border border-gray-200 bg-white text-gray-500 hover:text-red-500 hover:bg-red-50 hover:border-red-200 shadow-sm cursor-pointer">
        <i class="ti ti-trash text-base"></i>
      </button>
    </div>
  </div>

  <!-- Sticky record header -->
  <div class="bg-white w-full flex flex-col gap-4 p-4 border-b shrink-0">
    <!-- Avatar + title + status -->
    <div class="flex gap-3">
      <span class="select-none flex shrink-0 justify-center items-center bg-gray-100 border border-gray-200 font-medium text-xl text-gray-800 uppercase rounded-full" style="height:3.75rem; width:3.75rem">A</span>
      <div class="flex flex-col justify-center gap-y-2 w-full truncate">
        <div class="flex items-center justify-between space-x-5">
          <h1 class="font-medium text-lg leading-tight text-gray-800 truncate" title="WO-10432 — Roof Repair">WO-10432 — Roof Repair</h1>
          <span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default text-blue-700 bg-blue-50 border-blue-200 shrink-0">Open</span>
        </div>
        <!-- Location sub-label -->
        <div class="flex items-center gap-1">
          <span class="inline-flex items-center gap-x-1 text-md text-gray-500">
            <i class="ti ti-map-pin flex-shrink-0"></i>
            <span class="truncate leading-tight">123 Main St, New York, NY 10001</span>
          </span>
        </div>
      </div>
    </div>
    <!-- Quick-action button row -->
    <div class="select-none flex flex-wrap items-center space-x-2">
      <!-- Status-change button (labelled) -->
      <button type="button" class="h-9 px-2 flex justify-center items-center gap-x-1 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none">
        <i class="ti ti-status-change pointer-events-none"></i>
        <span class="text-base leading-tight">Open</span>
      </button>
      <!-- Icon-only action buttons -->
      <button type="button" class="h-9 w-9 inline-flex justify-center items-center px-2 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none" aria-label="Schedule">
        <i class="ti ti-calendar-plus text-2xl pointer-events-none"></i>
      </button>
      <button type="button" class="h-9 w-9 inline-flex justify-center items-center px-2 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none" aria-label="Email">
        <i class="ti ti-mail text-2xl pointer-events-none"></i>
      </button>
      <button type="button" class="h-9 w-9 inline-flex justify-center items-center px-2 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none" aria-label="Call">
        <i class="ti ti-phone text-2xl pointer-events-none"></i>
      </button>
      <button type="button" class="h-9 w-9 inline-flex justify-center items-center px-2 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none" aria-label="Note">
        <i class="ti ti-note text-2xl pointer-events-none"></i>
      </button>
      <button type="button" class="h-9 w-9 inline-flex justify-center items-center px-2 rounded-lg shadow border cursor-pointer bg-white hover:bg-gray-50 focus:outline-none" aria-label="More options">
        <i class="ti ti-dots-vertical text-2xl pointer-events-none"></i>
      </button>
    </div>
  </div>

  <!-- Scrollable body -->
  <div class="pl-2.5 pr-2.5 flex flex-col gap-1 overflow-y-auto">

    <!-- Accordion section (expanded state shown) -->
    <div class="bg-white mt-2 group">
      <!-- Accordion header: sticky within scroll container -->
      <div class="h-9 gap-2 flex py-1 justify-between items-center w-full bg-white sticky top-0 z-10">
        <button type="button" class="px-1 pr-1.5 py-1.5 flex items-center gap-x-1 hover:bg-gray-100 text-gray-700 rounded-lg focus:outline-none" aria-expanded="true">
          <i class="ti ti-chevron-right" style="transform:rotate(90deg)"></i>
          <span class="text-base font-medium leading-tight">Job Details</span>
        </button>
        <!-- Section-level edit button: visible on group hover -->
        <button type="button" class="w-7 h-7 text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded-md opacity-0 group-hover:opacity-100 transition-opacity" aria-label="Edit Job Details">
          <i class="ti ti-pencil text-lg"></i>
        </button>
      </div>

      <!-- Accordion body: 5-column grid, label col-span-2 / value col-span-3 -->
      <div class="p-2 pb-4 border-b">
        <div class="grid grid-cols-5 gap-4 gap-y-5 items-baseline">

          <!-- String field -->
          <div class="col-span-2"><div class="text-gray-500 text-base truncate leading-tight" title="Customer">Customer</div></div>
          <div class="col-span-3 group/field flex items-start space-x-1.5">
            <div class="min-w-0 overflow-hidden"><div class="text-base text-gray-800 truncate leading-tight">Acme Corp</div></div>
            <button type="button" class="w-5 h-5 flex items-center justify-center text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded-md opacity-0 group-hover/field:opacity-100 transition-opacity shrink-0" aria-label="Edit Customer">
              <i class="ti ti-pencil text-sm"></i>
            </button>
          </div>

          <!-- Badge/status field -->
          <div class="col-span-2"><div class="text-gray-500 text-base truncate leading-tight">Priority</div></div>
          <div class="col-span-3 group/field flex items-start space-x-1.5">
            <div class="min-w-0 overflow-hidden">
              <div class="flex flex-nowrap items-center gap-1 group/batch">
                <span class="px-1.5 py-1 leading-tight rounded-md font-medium inline-flex items-center border text-sm min-w-0 bg-orange-50 text-orange-700 border-orange-200">High</span>
              </div>
            </div>
          </div>

          <!-- Linked record field -->
          <div class="col-span-2"><div class="text-gray-500 text-base truncate leading-tight">Property</div></div>
          <div class="col-span-3 group/field flex items-start space-x-1.5">
            <div class="min-w-0 overflow-hidden">
              <div class="flex flex-wrap items-center gap-1">
                <button type="button" class="group/tag-link inline-flex items-center gap-1 min-w-0 max-w-full text-base text-gray-800 text-left cursor-pointer leading-tight">
                  <span class="truncate group-hover/tag-link:underline">123 Main St</span>
                  <i class="ti ti-chevron-right text-sm shrink-0 text-gray-400 group-hover/tag-link:text-gray-600"></i>
                </button>
              </div>
            </div>
          </div>

          <!-- Empty field (add action) -->
          <div class="col-span-2"><div class="text-gray-500 text-base truncate leading-tight">Category</div></div>
          <div class="col-span-3">
            <button type="button" class="inline-flex items-center space-x-1 text-md font-medium text-blue-500 hover:text-blue-600 hover:bg-blue-50 px-1 py-0.5 rounded-md cursor-pointer">
              <i class="ti ti-plus"></i>
              <span class="leading-tight">Add</span>
            </button>
          </div>

        </div>
      </div>
    </div>

    <!-- Related records accordion section -->
    <div class="bg-white group">
      <div class="h-9 py-1 flex items-center justify-between w-full bg-white sticky top-0 z-10">
        <button type="button" class="px-1 pr-1.5 py-1.5 flex items-center gap-x-1 hover:bg-gray-100 text-gray-700 rounded-lg focus:outline-none" aria-expanded="true">
          <i class="ti ti-chevron-right" style="transform:rotate(90deg)"></i>
          <span class="text-base font-medium leading-tight truncate">Properties (1)</span>
        </button>
      </div>
      <div class="pb-4 border-b space-y-2 px-0.5 pt-1">
        <button type="button" class="w-full rounded-lg border border-gray-200 bg-gray-50 p-2 text-left cursor-pointer hover:bg-gray-100 transition-colors">
          <div class="flex items-start gap-2.5">
            <div class="h-8 w-8 rounded-md bg-gray-200 text-gray-500 flex items-center justify-center font-medium text-xl shrink-0 uppercase">A</div>
            <div class="min-w-0 flex-1">
              <div class="text-base text-gray-800 font-medium truncate leading-tight">Acme HQ Building</div>
              <div class="mt-1 text-gray-500 text-md leading-snug">123 Main St, New York</div>
            </div>
          </div>
        </button>
      </div>
    </div>

  </div>
</div>
```

## Dos & Don'ts

### Do

- Keep the header zone (`shrink-0`) strictly non-scrollable so the record identity and actions remain visible as the user scrolls the body.
- Use the `sticky top-0 z-10` accordion header pattern so section labels stay visible when scrolling within a long section body.
- Apply the `group` / `group-hover:opacity-100` pattern for inline edit pencil buttons — they should appear on hover, not occupy permanent space.
- Always provide `title` attributes on truncated text nodes (`h1`, label `div`) so the full value is accessible on hover.
- Show a count in parentheses in the accordion label when a related-records section has a known quantity (e.g., "Properties (1)").
- In the full details page layout, allow the panel to collapse to a `3.5rem`-wide strip (`width:3.5rem; flex-shrink:0`) so the centre column gains the reclaimed space. The expand toggle (`ti-chevron-right`) must remain visible and centred.
- Keep all key-value record fields in the left panel. It is the canonical location for field data. If a center panel tab specifically requires fields, they must be enclosed in a `rounded-lg border border-border` card with each field rendered as a vertical label-above-value stack — never replicated with the `grid-cols-5` side-by-side layout used here.

### Don't

- Do not remove the `overflow-y-auto` from the scrollable body and place it on the outer panel — this breaks the sticky accordion headers.
- Do not place the cover-image strip inside the header `shrink-0` zone; it belongs above it so the header buttons remain at a stable position.
- Do not use the loading variant for partial updates — it replaces the entire panel and causes disorienting layout shifts if only one section is refreshing.
- Do not add more than six action buttons to the quick-action row; beyond that, move lower-priority actions behind the `ti-dots-vertical` overflow menu.
- Do not omit `aria-label` on icon-only action buttons — screen readers cannot infer intent from the icon class name alone.
- Do not remove the left panel from the DOM when it is collapsed — keep a `3.5rem` strip so the expand affordance is always one click away.
- Do not use the `25rem` width from the standalone variant inside the full details page layout; use `22rem` (`style='width:22rem'`) in the 3-column layout to leave room for the centre and right columns.
- Do not move key-value fields to the center panel to reduce left panel length — consolidate field sections instead. Fields shown in the center panel must use the card + vertical-stack layout, not the `grid-cols-5` pattern from this component.

## Patterns & Rules

1. **5-column field grid** — Label columns always span 2 of 5 (`col-span-2`) and value columns always span 3 of 5 (`col-span-3`). Do not vary this ratio within a single accordion body; consistent column alignment makes the panel scannable.
2. **Accordion chevron rotation** — An expanded section rotates the `ti-chevron-right` icon 90 degrees via inline `transform: rotate(90deg)`. Collapsed sections have no rotation. Do not swap icon glyphs; use transform only.
3. **Inline field editing** — Individual field values show a `ti-pencil` button on `group-hover/field`. Section-level editing uses a larger pencil (`w-7 h-7`) on `group-hover` of the accordion container. Both use `opacity-0 → opacity-100 transition-opacity` rather than `display:none` to keep layout stable.
4. **Avatar initials** — The record avatar is a circular `span` (`rounded-full`) at `3.75rem × 3.75rem`, not an `img` tag, so it gracefully renders initials when no photo is available. The cover-image variant supplements this; it does not replace the avatar.
5. **Related record cards** — Related records render as full-width `button` elements with `rounded-lg border border-gray-200 bg-gray-50` so they are keyboard-navigable and look distinct from field rows without requiring a separate component.
6. **Collapsed width** — The collapsed state uses `width:3.5rem; flex-shrink:0` not `display:none`. The expand toggle (`ti-chevron-right`) is centred inside an `h-8 w-8 rounded-lg` button with `hover:bg-gray-100`.

## Accessibility

- The accordion toggle button must carry `aria-expanded="true|false"` reflecting the current open/closed state.
- Icon-only action buttons in the quick-action row require explicit `aria-label` values (e.g., `aria-label="Schedule"`, `aria-label="Send email"`).
- Truncated text nodes (record title, field labels, related record names) must have a matching `title` attribute so pointer users can read the full value on hover.
- The scrollable body (`overflow-y-auto`) should be reachable by keyboard; ensure the panel itself is not excluded from the tab order when embedded in a layout.
- The loading variant's shimmer containers should carry `aria-busy="true"` on the panel root and `aria-hidden="true"` on individual shimmer blocks so assistive technologies announce the loading state without enumerating empty placeholders.

## Related Components

- [Details Sidebar Nav](./sidebar-nav.md) — The complementary right-side navigation panel used alongside this component in the two-column detail layout; it provides tab-level navigation while this component provides record identity and field data.
- [Expansion Panel](./expansion-panel.md) — The standalone accordion primitive; the accordion sections inside this component follow the same open/close pattern but are scoped to the panel's scrollable body.
- [Breadcrumb](./breadcrumb.md) — Typically rendered above the detail layout that contains this component, providing path context back to the list view.
- [Details Center Panel](./details-center-panel.md) — The centre column that expands to fill the space when the left panel is collapsed.
- [Full Details Page Layout](./details-page-layout.md) — The three-column layout that composes the left panel, centre panel, and right sidebar into a single record detail view.
