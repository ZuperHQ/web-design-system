---
component: Tables
category: Data Display
variants: [default, row-states, loading, empty, bulk-selection]
related: [badges-and-tags, toolbar-row, empty-states, loading-shimmer, toast-snackbar]
---

# Tables

> Tables display structured, multi-column records in a scannable grid so users can read, compare, sort, and act on many items at once.

## Overview

The table component uses a fixed-layout `<table>` with a sticky, frosted-glass `<thead>` (achieved via `bg-opacity-50 backdrop-blur-md`) and compact 40px data rows separated by `border-b border-gray-200`. Each column header carries a `table-header-cell` class that positions a `column-resize-handle` affordance, enabling users to drag column boundaries to suit their workflow. Status values inside cells are rendered with inline badge spans rather than plain text, tying the table tightly to the Badges & Tags component.

## When to Use

- Listing operational records such as work orders, invoices, or customers where users need to compare multiple fields per item side by side.
- Displaying paginated or filtered result sets where bulk selection (via header and row checkboxes) drives a contextual toolbar action.
- Presenting sortable columns where field order communicates priority, such as sorting work orders by due date or customer name.
- Embedding a secondary record list inside a detail panel where horizontal space is sufficient for at least three columns.
- Replacing a card grid when users need to scan a specific column value (status, date, amount) across many rows simultaneously.

## When NOT to Use

- When there is only one meaningful field per item — use [Badges & Tags](./badges-and-tags.md) within a simple list instead.
- When records have deeply nested or variable-length content that does not compress into a fixed column — use a card-based layout with [Form Layout](./form-layout.md) patterns instead.
- When the dataset is always empty by design or the feature is not yet enabled — use [Empty States](./empty-states.md) as a standalone page section rather than embedding a zero-row table.

## Variants

| Variant | Description |
|---------|-------------|
| default | The standard interactive table with sortable header cells, per-row checkboxes, status badge cells, and an overflow action button; use this for all primary listing views. |
| row-states | A stripped-down table that illustrates the visual difference between a default (unselected) row and a selected (checked) row; reference this when implementing row-selection highlighting logic. |
| loading | All cell content is replaced with `bg-gray-200 animate-shimmer` placeholder bars and every interactive control is `disabled`; show this variant while the data fetch is in flight. |
| empty | A single full-width cell containing the text "No data found" in `text-gray-500`; display this variant after a successful fetch that returns zero records. |
| bulk-selection | Table with 3+ rows checked, header checkbox in checked/indeterminate state, and a snackbar action bar visible at the bottom of the container. Use when the user has selected one or more rows to perform a bulk action. |

## HTML Structure

```html
<!-- Outer scroll container — keeps table from breaking page layout -->
<div class="overflow-auto rounded-lg border border-border">
  <table class="w-full caption-bottom" style="table-layout:fixed;border-collapse:collapse;min-width:681px;">

    <!-- Sticky frosted header -->
    <thead class="sticky top-0 bg-white bg-opacity-50 backdrop-blur-md z-10 shadow-sm">
      <tr class="h-11">

        <!-- Checkbox column -->
        <th class="h-11 border-b border-gray-200 px-3 align-middle" style="width:35px;min-width:35px;max-width:35px;">
          <div class="flex items-center justify-center">
            <input type="checkbox" class="w-4 h-4 rounded border border-gray-300 cursor-pointer" />
          </div>
        </th>

        <!-- Sortable column header -->
        <th class="h-11 border-b border-gray-200 px-3 text-left align-middle font-medium text-gray-500 text-md relative table-header-cell"
            style="width:160px;min-width:160px;">
          <div class="flex items-center gap-2 cursor-pointer select-none pr-2 h-full">
            <span class="truncate mt-1">Work Order #</span>
            <!-- Active sort: text-blue-600; inactive sort: text-gray-200 -->
            <i class="mt-0.5 ti ti-sort-descending flex-shrink-0 text-2xl text-blue-600"></i>
          </div>
          <!-- Drag handle injected by resize logic -->
          <div class="column-resize-handle"></div>
        </th>

        <!-- Non-sortable column header -->
        <th class="h-11 border-b border-gray-200 px-3 text-left align-middle font-medium text-gray-500 text-md relative table-header-cell"
            style="width:130px;min-width:130px;">
          <div class="truncate mt-1 pr-2">Status</div>
          <div class="column-resize-handle"></div>
        </th>

        <!-- Actions column (no label) -->
        <th class="h-11 border-b border-gray-200 px-3 align-middle"
            style="width:66px;min-width:66px;max-width:66px;"></th>

      </tr>
    </thead>

    <tbody>

      <!-- Default data row -->
      <tr class="h-10 border-b">
        <td class="h-10 px-3 align-middle" style="width:35px;">
          <div class="flex items-center justify-center">
            <input type="checkbox" class="w-4 h-4 rounded border border-gray-300 cursor-pointer" />
          </div>
        </td>
        <td class="h-10 px-3 align-middle truncate text-base text-gray-600">WO-10432</td>
        <!-- Status cell uses inline badge -->
        <td class="h-10 px-3 align-middle">
          <span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default
                        bg-blue-50 text-blue-700 border-blue-200">Open</span>
        </td>
        <!-- Row overflow action -->
        <td class="h-10 px-3 align-middle" style="width:66px;">
          <button class="p-2 inline-flex items-center justify-center rounded-md hover:bg-gray-200">
            <i class="ti ti-dots text-base"></i>
          </button>
        </td>
      </tr>

      <!-- Loading shimmer row (loading variant) -->
      <!-- <tr class="h-10 border-b">
        <td class="h-10 px-3 align-middle" style="width:35px;">
          <div class="flex items-center justify-center">
            <input type="checkbox" disabled class="w-4 h-4 rounded border border-gray-200 opacity-50" />
          </div>
        </td>
        <td class="h-10 px-3 align-middle">
          <div class="h-4 w-full bg-gray-200 rounded animate-shimmer"></div>
        </td>
        <td class="h-10 px-3 align-middle">
          <div class="h-4 w-24 bg-gray-200 rounded animate-shimmer"></div>
        </td>
        <td class="h-10 px-3 align-middle" style="width:66px;">
          <button disabled class="p-2 inline-flex items-center justify-center rounded-md opacity-50">
            <i class="ti ti-dots text-base"></i>
          </button>
        </td>
      </tr> -->

      <!-- Empty state row (empty variant) -->
      <!-- <tr>
        <td class="h-36 text-center align-middle">
          <h4 class="font-medium text-gray-500 text-base">No data found</h4>
        </td>
      </tr> -->

    </tbody>
  </table>
</div>

<!-- Bulk-selection variant: relative container wraps the scrollable table + snackbar -->
<!-- <div class="relative overflow-hidden rounded-lg border border-border" style="height:310px">
  <div class="overflow-auto h-full">
    <table class="w-full caption-bottom" style="table-layout:fixed;border-collapse:collapse;min-width:681px;">
      <thead class="sticky top-0 bg-white bg-opacity-50 backdrop-blur-md z-10 shadow-sm">
        <tr class="h-11">
          <th class="h-11 border-b border-gray-200 px-3 align-middle" style="width:35px;min-width:35px;max-width:35px;">
            <div class="flex items-center justify-center">
              <!- - Header checkbox: checked (all selected) or indeterminate (some selected) - ->
              <input type="checkbox" checked class="w-4 h-4 rounded border border-gray-300 cursor-pointer" />
            </div>
          </th>
          <!- - … column headers … - ->
        </tr>
      </thead>
      <tbody>
        <!- - Selected row - ->
        <tr class="h-10 border-b bg-blue-50">
          <td class="h-10 px-3 align-middle" style="width:35px;">
            <div class="flex items-center justify-center">
              <input type="checkbox" checked class="w-4 h-4 rounded border border-gray-300 cursor-pointer" />
            </div>
          </td>
          <td class="h-10 px-3 align-middle truncate text-base text-gray-600">WO-10432</td>
          <!- - … cells … - ->
        </tr>
        <!- - Unselected row - ->
        <tr class="h-10 border-b">
          <!- - … cells … - ->
        </tr>
      </tbody>
    </table>
  </div>

  <!- - Bulk-action snackbar: anchored inside the container for demos; use position:fixed bottom-6 in production - ->
  <div class="absolute bottom-4 left-1/2 -translate-x-1/2 z-20">
    <div class="rounded-lg shadow-lg px-4 py-3 text-base text-white inline-flex items-center gap-x-3"
         style="background-color:#192d43">
      <span class="font-medium whitespace-nowrap">3 Job(s)</span>
      <button type="button" class="whitespace-nowrap text-white/80 hover:text-white cursor-pointer">Select All</button>
      <div class="w-px h-4 bg-white/30"></div>
      <button type="button" class="whitespace-nowrap text-white/80 hover:text-white cursor-pointer">Assign</button>
      <button type="button" class="whitespace-nowrap text-white/80 hover:text-white cursor-pointer">Export</button>
      <button type="button" class="whitespace-nowrap text-white/80 hover:text-white cursor-pointer">Delete</button>
      <div class="w-px h-4 bg-white/30"></div>
      <button type="button" class="flex items-center justify-center text-white/80 hover:text-white cursor-pointer" aria-label="Dismiss selection">
        <i class="ti ti-x text-lg"></i>
      </button>
    </div>
  </div>
</div> -->
```

## Dos & Don'ts

### Do

- Always wrap the table in `overflow-auto rounded-lg border border-border` so it scrolls horizontally on narrow viewports without breaking the page layout.
- Set `table-layout:fixed` and explicit `width`/`min-width` on each column so text cells truncate predictably instead of reflowing the grid.
- Use `truncate` on text data cells (`text-base text-gray-600`) and let the column width control visible length rather than wrapping content onto multiple lines.
- Show the loading variant during every async data fetch — replace shimmer rows with real rows only after the response resolves to prevent layout shift.
- Render status values with the appropriate badge color token (e.g., `bg-green-50 text-green-700 border-green-200` for Completed) so status meaning is communicated consistently across all tables.
- Apply `bg-blue-50` to the entire `<tr>` when a row is selected so selection state is readable without relying solely on the checkbox.
- Wrap the table in a `position:relative` container and use `position:absolute bottom-4 left-1/2 -translate-x-1/2` to anchor the snackbar within the scroll viewport during in-page demos; in production use `position:fixed bottom-6`.

### Don't

- Do not omit the `column-resize-handle` div from `table-header-cell` headers — removing it breaks the resize affordance and makes the column appear fixed to users who expect drag-to-resize behavior.
- Do not place free-form long-form text (notes, descriptions, addresses) directly in a cell without truncation — it collapses adjacent column widths and breaks the fixed-layout grid.
- Do not use the row-states variant in production views; it is a reference-only variant for documenting interaction states and should not appear in application screens.
- Do not style the overflow action button with a background at rest — it uses `hover:bg-gray-200` only, so adding a persistent background color conflicts with the row's visual hierarchy.
- Do not skip the `disabled` attribute and `opacity-50` class on shimmer row controls — leaving checkboxes and buttons interactive during loading allows erroneous user actions before data has arrived.
- Do not show the snackbar when zero rows are selected — it must only appear when at least one row checkbox is checked.
- Do not use the bulk-selection variant's `bg-blue-50` row highlight without also checking the row's checkbox — visual and data state must stay in sync.

## Patterns & Rules

1. **Sticky header with frosted glass** — Apply `sticky top-0 bg-white bg-opacity-50 backdrop-blur-md z-10 shadow-sm` to `<thead>` so column labels remain visible as the user scrolls through long record sets without fully obscuring the rows underneath.
2. **Active sort indicator color** — The sort icon uses `text-blue-600` when that column is the active sort key and `text-gray-200` (near-invisible) when inactive; never hide the icon entirely so the column remains identifiable as sortable.
3. **Fixed checkbox and action column widths** — The select column is always `width:35px;min-width:35px;max-width:35px;` and the actions column is always `width:66px;min-width:66px;max-width:66px;`; these widths are non-negotiable and must not be resized by the user.
4. **Loading shimmer uses `animate-shimmer` on `bg-gray-200` bars** — Replace every data cell's content with a `<div class="h-4 bg-gray-200 rounded animate-shimmer">` block; vary the `w-*` class (e.g., `w-full`, `w-24`, `w-28`) to mimic realistic content widths and reduce perceived layout jump on load.
5. **Empty state is table-native** — The empty variant places the "No data found" message inside a `<td class="h-36 text-center align-middle">` so column borders and the outer container remain structurally intact; do not replace the entire table with a standalone empty-state component unless the table itself is conditionally rendered.
6. **Bulk selection snackbar background** — Always use `background-color:#192d43` for the snackbar bar; never use `bg-gray-800` or `bg-black` as substitutes. The specific dark navy tone is the Zuper-established convention for bulk action bars.
7. **Header checkbox indeterminate state** — When some (but not all) rows are selected, set the header checkbox's `indeterminate` property to `true` in JavaScript (`el.indeterminate = true`); this cannot be expressed in HTML alone. Never leave the header checkbox unchecked when rows are selected.

## Accessibility

- The `<table>` element provides an implicit `role="table"` landmark; add an `aria-label` or `aria-labelledby` pointing to a visible heading so screen readers identify the table's purpose.
- The header checkbox should carry `aria-label="Select all rows"` and each row checkbox should carry `aria-label="Select row [identifier]"` to give screen reader users unambiguous selection targets.
- Column headers that trigger sorting must set `aria-sort="ascending"` or `aria-sort="descending"` on the active `<th>` and `aria-sort="none"` on inactive sortable headers so assistive technology announces the current sort state.
- Keyboard users navigate between cells with Tab; the overflow action button in each row must be reachable via Tab and activatable with Enter or Space, with focus returning to the button after the menu closes.
- During the loading variant, all `<input>` and `<button>` elements must carry both the `disabled` attribute and `aria-disabled="true"` so screen readers announce the interactive controls as unavailable.
- When rows are selected, the snackbar must receive focus or announce itself via `role="status"` or `aria-live="polite"` so keyboard and screen-reader users know contextual actions are available.
- The dismiss button (`ti-x`) in the snackbar must carry `aria-label="Dismiss selection"`.

## Related Components

- [Badges & Tags](./badges-and-tags.md) — Status values inside table cells are rendered as badge spans; consult this component for the full set of color tokens and semantic usage rules.
- [Empty States](./empty-states.md) — When a table search or filter yields zero results, the empty variant's "No data found" pattern aligns with the broader empty-state conventions defined here.
- [Loading Shimmer](./loading-shimmer.md) — The `animate-shimmer` animation and `bg-gray-200` placeholder bars used in the loading variant are part of the shared shimmer system documented in this component.
