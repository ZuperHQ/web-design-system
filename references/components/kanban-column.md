---
component: Kanban Column
category: Application Layouts
variants: [default]
related: [cards, reorderable-list]
---

# Kanban Column

> A scrollable vertical lane that groups record cards under a shared workflow status, letting users see workload at a glance and move items between stages by dragging.

## Overview

The Kanban Column is a composite component built from a sticky column header and a scrollable card list rendered on a `bg-slate-100` background. Each column header carries a status color dot, a label, a card-count badge, and an overflow menu, while the body stacks individual job cards separated by uniform spacing. It occupies a fixed width (typically `w-90` / `22.5rem`) within a horizontal board layout, making it the primary view for status-based workflow management in Zuper.

## When to Use

- Displaying jobs, work orders, or tasks grouped by their current workflow status (e.g., Scheduled, In Progress, Completed).
- Allowing dispatchers or managers to drag records from one status lane to another without opening each record individually.
- Presenting workload distribution across stages so team leads can spot bottlenecks at a glance.
- Supplementing a list or table view as an alternate board perspective toggled from the toolbar.
- Showing real-time loading states with shimmer cards while the column's data is being fetched.

## When NOT to Use

- Showing a flat, sortable list of records without status grouping — use [Tables](./tables.md) instead.
- Displaying summarized numeric metrics or KPIs per status — use [Stats Cards](./stats-cards.md) instead.
- Navigating between sections of the application — use [Sidebar Nav](./sidebar-nav.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| default | The standard column with a `bg-slate-100` container, a bordered header, and a padded card list; use this for all board layouts where columns represent a single workflow status. |

## HTML Structure

```html
<!-- Column wrapper: fixed width, slate background -->
<div class="bg-slate-100 rounded-lg overflow-hidden" style="width:22.5rem">

  <!-- Column header -->
  <div class="flex items-center justify-between px-3 py-2 bg-slate-100 border-b border-gray-200">
    <div class="flex items-center gap-2">
      <!-- Status color dot -->
      <div class="w-3 h-3 rounded-full bg-yellow-400"></div>
      <!-- Status label -->
      <span class="text-base font-medium text-gray-700">In Progress</span>
      <!-- Card count badge -->
      <span class="px-1.5 py-0.5 text-md border border-border rounded-lg bg-gray-50 text-gray-700 leading-tight">3</span>
    </div>
    <!-- Column overflow menu -->
    <button class="inline-flex items-center justify-center h-7 w-7 rounded-lg hover:bg-gray-200 text-gray-600">
      <i class="ti ti-dots text-base"></i>
    </button>
  </div>

  <!-- Card list body -->
  <div class="p-2 space-y-2">

    <!-- Default card state -->
    <div class="px-3 py-2 flex flex-col bg-white border border-gray-200 rounded-lg shadow-2xs transition-all duration-200 cursor-pointer hover:border-gray-300 hover:shadow-lg relative group">
      <!-- External link button (visible on hover) -->
      <button class="opacity-0 group-hover:opacity-100 absolute top-2 right-2 w-7 h-7 flex items-center justify-center border border-gray-300 rounded-md shadow-sm bg-white text-gray-500 hover:border-blue-500 hover:text-gray-600 transition-opacity duration-200 z-10">
        <i class="ti ti-external-link text-lg"></i>
      </button>
      <!-- Card header: ID + value -->
      <div class="space-y-2">
        <div class="flex justify-between items-center">
          <span class="text-gray-500 text-md leading-tight">JOB-1234</span>
          <span class="tabular-nums text-gray-500 text-base leading-tight group-hover:opacity-0 transition-opacity duration-200">$350.00</span>
        </div>
        <h4 class="text-gray-900 text-base truncate font-medium leading-tight">Fix HVAC Unit at Main Office</h4>
      </div>
      <!-- Card metadata rows -->
      <div class="space-y-2 mt-2">
        <div class="text-md flex items-center text-gray-600 space-x-2">
          <i class="ti ti-map-pin text-base flex-shrink-0"></i>
          <div class="truncate flex-1">123 Main St, New York</div>
        </div>
        <div class="text-md flex items-center text-gray-600 space-x-2">
          <i class="ti ti-user text-base flex-shrink-0"></i>
          <div class="truncate flex-1">John Doe</div>
        </div>
        <div class="text-md flex items-center text-gray-600 space-x-2">
          <i class="ti ti-calendar text-base flex-shrink-0"></i>
          <div class="truncate flex-1">Jun 17, 2026</div>
        </div>
      </div>
      <!-- Card footer: duration, notes count, priority badge -->
      <div class="flex items-center justify-between mt-2 pt-2 border-t border-gray-100">
        <div class="flex items-center space-x-4">
          <div class="flex items-center text-gray-600 space-x-2">
            <i class="ti ti-clock-hour-4 text-base py-0.5 rounded-full"></i>
            <span class="text-sm leading-tight">2h 30m</span>
          </div>
          <button class="flex items-center text-gray-600 hover:bg-gray-100 rounded-md p-1 space-x-1">
            <i class="ti ti-notes text-base"></i>
            <span class="text-sm leading-tight">3</span>
          </button>
        </div>
        <div class="flex items-center gap-1">
          <span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-orange-100 text-orange-700 border-orange-200">High</span>
        </div>
      </div>
    </div>

    <!-- Selected card state (blue border) -->
    <div class="px-3 py-2 flex flex-col bg-white border border-blue-500 rounded-lg shadow-2xs transition-all duration-200 cursor-pointer relative">
      <!-- ... same internal structure as default card ... -->
    </div>

    <!-- Drag placeholder state -->
    <div class="px-3 py-2 flex flex-col bg-white border-2 border-dashed border-gray-300 rounded-lg shadow-2xs opacity-80 pointer-events-none">
      <!-- ... card content ... -->
    </div>

    <!-- Shimmer / loading state -->
    <div class="px-3 py-2 flex flex-col bg-white border border-gray-200 rounded-lg shadow-2xs">
      <div class="space-y-2">
        <div class="flex justify-between items-center">
          <div class="h-3 w-16 rounded animate-shimmer"></div>
          <div class="h-3 w-12 rounded animate-shimmer"></div>
        </div>
        <div class="h-4 w-full rounded animate-shimmer"></div>
      </div>
      <div class="space-y-2 mt-2">
        <div class="h-3 w-3/4 rounded animate-shimmer"></div>
        <div class="h-3 w-1/2 rounded animate-shimmer"></div>
      </div>
      <div class="flex items-center space-x-4 mt-2 pt-2 border-t border-gray-100">
        <div class="h-3 w-14 rounded animate-shimmer"></div>
      </div>
    </div>

  </div>
</div>
```

## Dos & Don'ts

### Do

- Keep each column width at `22.5rem` (`w-90`) so cards remain legible and the board scrolls horizontally at predictable intervals.
- Always show the card count badge in the column header so users can assess workload without scrolling the card list.
- Use the shimmer variant for every card slot while data is loading rather than hiding the column entirely.
- Apply `border-blue-500` to a card only to indicate the currently selected record; reserve other border colors for hover (`border-gray-300`) and drag-placeholder (`border-dashed border-gray-300`).
- Truncate long card titles with `truncate` and show the full value via a `title` attribute tooltip.

### Don't

- Do not place more than one status per column — mixing statuses breaks the visual grouping that makes the board scannable.
- Do not remove the `border-t border-gray-100` footer separator from cards — without it, the priority badge and duration cluster lose visual separation from the metadata rows.
- Do not use the drag-placeholder state for anything other than the in-flight drag source; applying `pointer-events-none` and `opacity-80` to a visible card confuses users into thinking it is disabled.
- Do not omit the overflow menu button from the column header — it is the primary affordance for column-level actions like filtering or collapsing.
- Do not hard-code card content height; let cards grow naturally with their metadata rows so sparse cards (fewer fields) and dense cards coexist without forced whitespace.

## Patterns & Rules

1. **Status dot color** — The `w-3 h-3 rounded-full` dot in the column header must match the status color token used across the rest of the application (e.g., `bg-yellow-400` for In Progress, `bg-green-500` for Completed) to maintain cross-view consistency.
2. **Hover reveal pattern** — The external-link button (`opacity-0 group-hover:opacity-100`) and the monetary value (`group-hover:opacity-0`) swap visibility on hover so the action button does not obscure the value at rest, while still providing quick navigation.
3. **Overdue duration styling** — When a job's duration is past the scheduled window, apply `bg-red-100 text-red-500` to the clock icon and `text-red-500` to the duration text to signal urgency without adding a separate indicator.
4. **Card footer separator** — Always include `border-t border-gray-100` on the footer row to visually anchor the secondary metadata (duration, notes, priority) from the primary content above.
5. **Loading sequence** — Render shimmer cards (`animate-shimmer`) inside the real column shell (header with count badge showing a placeholder or zero) rather than a full-column skeleton, so the board layout does not shift when real data arrives.

## Accessibility

- The column container should carry `role="list"` and each card `role="listitem"` so assistive technologies announce the number of items in the lane.
- Keyboard users must be able to Tab into each card and press Enter to open it; draggable cards should additionally support Space to pick up and arrow keys to move between columns, following the ARIA drag-and-drop pattern.
- The status color dot alone is not sufficient to convey status — the text label (`In Progress`, `Completed`, etc.) must always accompany it so users who cannot distinguish color still receive the information.

## Related Components

- [Cards](./cards.md) — The individual job card rendered inside each column; the Kanban Column provides the layout container while the card component defines the content and interaction states.
- [Tables](./tables.md) — The flat-list alternative view for the same record set; toggling between table and board view is a common pattern in list toolbars.
- [Toolbar Row](./toolbar-row.md) — The view-switcher control (including the Kanban button) that lives above the board and lets users toggle between list, table, and board layouts.
