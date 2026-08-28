---
component: Loading Shimmer
category: Feedback & Content
variants: [table, cards]
related: [empty-states, tables, cards]
---

# Loading Shimmer

> A skeleton-screen component that fills the space of loading content with animated gray placeholder bars, preventing layout shift and communicating progress to the user.

## Overview

Loading Shimmer renders `bg-gray-200` (tables) or `bg-gray-100` (cards) rounded rectangles that match the dimensions of real content, animated with a left-to-right highlight sweep via the `animate-shimmer` class. It sits in the Feedback & Content category alongside empty states and toasts, acting as the first visual state a user sees before data resolves. Shimmer blocks mirror the structure of the real layout so the page feels stable and predictable during network requests.

## When to Use

- When a table is fetching its rows on initial page load and you need to preserve column structure.
- When a card grid (stats cards, info-metric cards) is loading and the card count is known or estimable.
- When a detail drawer or panel (such as an EDD panel) is opening and its field layout is fixed.
- When a background refresh could take more than 300 ms and a spinner would feel too disruptive.
- When you want to avoid cumulative layout shift by reserving the exact space that real content will occupy.

## When NOT to Use

- When data is already present and only a subset is refreshing — use an inline spinner overlay instead of replacing visible content with shimmer.
- When the page has no data at all and the user needs guidance on next steps — use [Empty States](./empty-states.md) instead.
- When an action button triggers a mutation and the user needs to see immediate confirmation — use [Toast / Snackbar](./toast-snackbar.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| table | Use when replacing a data table during load; shimmer blocks fill `th` and `td` cells at their actual column widths, preserving the `border-b`, row height (`h-10`/`h-11`), and disabled checkbox/action-button chrome. |
| cards | Use when replacing card layouts (info-metric or stats cards) during load; shimmer blocks use `bg-gray-100` rather than `bg-gray-200` and are arranged in a `flex flex-col gap-2` to match the card's internal spacing. |

## HTML Structure

```html
<!-- TABLE VARIANT -->
<!-- Wrap in the same overflow container used by the real table -->
<div class="overflow-auto rounded-lg border border-border">
  <table class="w-full caption-bottom" style="table-layout:fixed;border-collapse:collapse;min-width:520px">
    <thead class="sticky top-0 bg-white/50 backdrop-blur-md z-10 shadow-sm">
      <tr class="h-11">
        <!-- Checkbox column -->
        <th class="h-11 border-b border-gray-200 px-3 w-[35px]">
          <div class="flex items-center justify-center">
            <input type="checkbox" disabled class="size-4 shrink-0 rounded-[4px] border shadow-xs disabled:cursor-not-allowed disabled:opacity-50" />
          </div>
        </th>
        <!-- Shimmer placeholder for each header column -->
        <th class="h-11 border-b border-gray-200 px-3" style="width:160px;min-width:160px;">
          <div class="h-4 w-28 bg-gray-200 rounded animate-shimmer"></div>
        </th>
        <th class="h-11 border-b border-gray-200 px-3" style="width:160px;min-width:160px;">
          <div class="h-4 w-20 bg-gray-200 rounded animate-shimmer"></div>
        </th>
        <th class="h-11 border-b border-gray-200 px-3" style="width:130px;min-width:130px;">
          <div class="h-4 w-16 bg-gray-200 rounded animate-shimmer"></div>
        </th>
        <!-- Actions column -->
        <th class="h-11 border-b border-gray-200 px-3 w-[66px]">
          <div class="flex items-center justify-center">
            <button disabled class="p-2 inline-flex items-center justify-center rounded-md opacity-50">
              <!-- three-dots icon -->
            </button>
          </div>
        </th>
      </tr>
    </thead>
    <tbody>
      <!-- Repeat this row pattern for as many skeleton rows as needed -->
      <tr class="h-10 border-b">
        <td class="h-10 px-3 align-middle w-[35px]">
          <div class="flex items-center justify-center">
            <input type="checkbox" disabled class="size-4 shrink-0 rounded-[4px] border shadow-xs disabled:opacity-50" />
          </div>
        </td>
        <td class="h-10 px-3 align-middle"><div class="h-4 w-full bg-gray-200 rounded animate-shimmer"></div></td>
        <td class="h-10 px-3 align-middle"><div class="h-4 w-full bg-gray-200 rounded animate-shimmer"></div></td>
        <td class="h-10 px-3 align-middle"><div class="h-4 w-24 bg-gray-200 rounded animate-shimmer"></div></td>
        <td class="h-10 px-3 align-middle w-[66px]">
          <div class="flex items-center justify-center">
            <button disabled class="p-2 inline-flex items-center justify-center rounded-md opacity-50">
              <!-- three-dots icon -->
            </button>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>

<!-- CARDS VARIANT — Info-metric card shimmer -->
<div class="bg-white border border-border flex flex-col h-fit p-2.5 rounded-lg space-y-2" style="width:12.5rem">
  <div class="flex items-center space-x-1">
    <div class="h-4 w-4 rounded animate-shimmer flex-shrink-0"></div>
    <div class="h-3 w-24 rounded animate-shimmer"></div>
  </div>
  <div class="h-5 w-28 rounded animate-shimmer"></div>
</div>

<!-- CARDS VARIANT — Stats card shimmer -->
<div class="h-20 p-3 flex-col flex justify-center flex-auto bg-white border shadow-xs cursor-pointer rounded-md border-gray-200" style="width:12.5rem">
  <div class="flex flex-col gap-2">
    <div class="bg-gray-100 w-full animate-shimmer rounded-md h-4"></div>
    <div class="bg-gray-100 w-full animate-shimmer rounded-md h-7"></div>
  </div>
</div>

<!-- EDD / DETAIL PANEL SHIMMER (animate-pulse approach) -->
<div class="flex flex-col px-4 pt-4 gap-4 overflow-hidden animate-pulse">
  <!-- Tab bar skeleton -->
  <div class="flex gap-3 pb-2 border-b border-gray-100">
    <div class="h-5 w-20 bg-gray-200 rounded"></div>
    <div class="h-5 w-24 bg-gray-200 rounded"></div>
    <div class="h-5 w-16 bg-gray-200 rounded"></div>
  </div>
  <!-- Hero block skeleton -->
  <div class="flex items-center gap-3 pt-1">
    <div class="h-12 w-12 bg-gray-200 rounded-full flex-shrink-0"></div>
    <div class="flex flex-col gap-1.5 flex-1">
      <div class="h-4 w-[55%] bg-gray-200 rounded"></div>
      <div class="h-3 w-[35%] bg-gray-200 rounded"></div>
    </div>
  </div>
  <!-- Field rows skeleton -->
  <div class="flex flex-col gap-4 mt-1">
    <div class="flex flex-col gap-1">
      <div class="h-2.5 w-[40%] bg-gray-200 rounded"></div>
      <div class="h-3.5 w-[55%] bg-gray-200 rounded"></div>
    </div>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Match shimmer block dimensions as closely as possible to the real content they replace, so the layout does not reflow when data loads.
- Use `bg-gray-200` with `animate-shimmer` inside tables and `bg-gray-100` with `animate-shimmer` inside card surfaces to respect the surface contrast hierarchy.
- Render at least as many skeleton rows as the page's default page size so the list area looks full.
- Disable interactive controls (checkboxes, action buttons) inside shimmer rows by adding the `disabled` attribute and `opacity-50`.
- Remove all shimmer nodes from the DOM the moment real data arrives, so the animated gradient does not continue running needlessly.

### Don't

- Do not use shimmer for indeterminate operations with no known end time — use a spinner or progress indicator instead, as perpetual shimmer misleads users about impending content arrival.
- Do not mix shimmer and real rows in the same table simultaneously — it creates visual inconsistency and confuses screen readers parsing live region updates.
- Do not omit the `rounded` class from shimmer bars — bare rectangles without border-radius break the soft visual language of the design system.
- Do not use shimmer inside modal dialogs for content that has already been partially loaded — partial shimmer inside a focused layer creates unnecessary cognitive load.
- Do not set shimmer bar widths all to `w-full` in every cell of the same column — vary widths (e.g., `w-full`, `w-24`, `w-28`) to simulate realistic text length variation.

## Patterns & Rules

1. **Structural fidelity** — Every shimmer layout must mirror the exact DOM skeleton of the real component it replaces, including column widths, padding, row heights, and any sticky header wrappers.
2. **Color by surface** — Use `bg-gray-200` on white table surfaces and `bg-gray-100` on white card surfaces; never use a darker shade that would contrast more than the actual data text.
3. **Animation class** — Apply `animate-shimmer` (the custom `@keyframes shimmer` sweep) for individual bars inside tables and cards; use Tailwind's `animate-pulse` only for composite panel shimmers (EDD-style) where the whole container fades in and out together.
4. **Disabled chrome** — Checkboxes and action buttons rendered inside shimmer rows must always carry `disabled` and `opacity-50` so they are visually inert and excluded from keyboard focus order.
5. **Row count** — Render exactly the number of skeleton rows that matches the expected page-size default (typically 5–10) to prevent blank space below the shimmer or an oversized loading region.

## Accessibility

- Add `aria-busy="true"` to the table or card container while shimmer is active so assistive technologies announce that the region is loading.
- Shimmer bars are purely decorative; add `aria-hidden="true"` to each shimmer `div` so screen readers skip the meaningless placeholder rectangles.
- Disabled checkboxes and buttons inside shimmer rows are correctly excluded from the tab sequence via the `disabled` attribute — no additional `tabindex="-1"` is required.
- When shimmer is replaced by real content, update the container to `aria-busy="false"` and optionally add a visually hidden live-region announcement (e.g., "Table loaded") for screen reader users.

## Related Components

- [Tables](./tables.md) — The table variant of Loading Shimmer is the direct loading state for this component; both share identical column structure, row heights, and border styles.
- [Stats Cards](./stats-cards.md) — The cards variant mirrors the stats card and info-metric card layouts; always keep shimmer dimensions in sync when card dimensions change.
- [Empty States](./empty-states.md) — Replaces Loading Shimmer after a successful fetch that returns zero results; never show both simultaneously.
