---
component: Stats Cards
category: Data Display
variants: [default, selected, hover, loading]
related: [cards]
---

# Stats Cards

> A compact, clickable summary tile that surfaces a single metric label, a count badge, and a prominent value to give users an at-a-glance status of a key dataset.

## Overview

Stats Cards are fixed-height (h-20) horizontal tiles arranged in a row, each pairing a labelled count badge with a large typographic value below it. They sit at the top of list and dashboard views, acting as interactive filters — clicking a card selects it and scopes the underlying data to that status. The selected state is distinguished by a blue border (`border-blue-500`) rather than a background change, keeping the card visually lightweight while clearly communicating focus.

## When to Use

- Displaying a small set of categorical totals on a list page (e.g., Total, Open, In Progress) where each category can also act as a filter.
- Showing a financial or numeric aggregate alongside a record count in the same tile (e.g., a currency value + item count badge).
- Providing a quick summary row above a data table or list so users can orient themselves before scanning rows.
- Communicating a loading skeleton while the underlying data is being fetched.

## When NOT to Use

- Showing rich metadata, icons, or multi-line descriptions per item — use [Cards](./cards.md) instead.
- Displaying a single prominent KPI that does not need to act as a filter and requires more visual hierarchy — use [Cards](./cards.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| default | Resting state with a white background and gray border; use for any card that is not currently selected. |
| hover | Gray-50 background (`bg-gray-50`) applied on pointer hover to confirm interactivity before a click is committed. |
| selected | Blue border (`border-blue-500`) replaces the default gray border; use to show which category is actively filtering the view. |
| loading | Shimmer skeleton replaces the label and value rows; use while data is fetching to prevent layout shift. |

## HTML Structure

```html
<!-- Stats card row — space cards evenly with flex -->
<div class="flex space-x-3 select-none">

  <!-- Default card -->
  <div class="h-20 p-3 flex-col flex justify-center flex-auto bg-white border shadow-xs cursor-pointer rounded-md border-gray-200">
    <div class="flex items-center justify-between text-base text-gray-400 font-medium whitespace-nowrap">
      <span class="text-gray-500 flex items-center space-x-1.5 min-w-0">
        <span class="truncate">Total</span>
      </span>
      <span class="text-blue-500 bg-blue-50 rounded-md leading-tight p-1.5">10057</span>
    </div>
    <div class="text-2xl font-semibold whitespace-nowrap text-gray-900">$2,567.00M</div>
  </div>

  <!-- Selected card — only the border class changes -->
  <div class="h-20 p-3 flex-col flex justify-center flex-auto bg-white border shadow-xs cursor-pointer rounded-md border-blue-500">
    <div class="flex items-center justify-between text-base text-gray-400 font-medium whitespace-nowrap">
      <span class="text-gray-500 flex items-center space-x-1.5 min-w-0">
        <span class="truncate">In Progress</span>
      </span>
      <span class="text-blue-500 bg-blue-50 rounded-md leading-tight p-1.5">891</span>
    </div>
    <div class="text-2xl font-semibold whitespace-nowrap text-gray-900">$456.00K</div>
  </div>

  <!-- Loading card — shimmer skeleton replaces content -->
  <div class="h-20 p-3 flex-col flex justify-center flex-auto bg-white border shadow-xs cursor-pointer rounded-md border-gray-200">
    <div class="flex flex-col gap-2">
      <div class="bg-gray-100 w-full animate-shimmer rounded-md h-4"></div>
      <div class="bg-gray-100 w-full animate-shimmer rounded-md h-7"></div>
    </div>
  </div>

</div>
```

## Dos & Don'ts

### Do

- Keep the label text short enough to fit on one line; the `truncate` class handles overflow but cutting off a label silently is confusing.
- Use the count badge (`text-blue-500 bg-blue-50`) consistently for the record count and reserve the large value slot for the aggregated numeric or currency figure.
- Apply `border-blue-500` only to the one card that is currently selected — never style multiple cards as selected simultaneously.
- Show the loading variant for every card in the row at the same time so the skeleton row height matches the loaded state and prevents layout shift.
- Wrap the card row in `select-none` to prevent accidental text selection on rapid clicks.

### Don't

- Do not remove `cursor-pointer` when the card is non-interactive — if a card must be read-only, revisit whether this component is the right choice.
- Do not stack stats cards vertically; they are designed as a horizontal filter row and lose their scanning utility when stacked.
- Do not place long prose or a secondary label inside the value slot (`text-2xl`) — that slot is strictly for a single formatted number or currency value.
- Do not mix selected state across multiple cards at once, as this breaks the single-filter mental model users rely on.

## Patterns & Rules

1. **Single selection at a time** — Only one card in a row may carry `border-blue-500` at any moment; selecting a new card deselects the previous one and updates the underlying dataset accordingly.
2. **Label truncation** — The label `<span>` carries both `truncate` and `min-w-0` to ensure long status names clip gracefully without breaking the flex layout.
3. **Count badge placement** — The count badge is always right-aligned inside the header row using `justify-between`; never place it below the value or beside it on the value row.
4. **Fixed height** — Cards use `h-20` to maintain a uniform row height across all states, including the loading skeleton, so the page does not reflow when data arrives.
5. **Shimmer loading** — The loading variant replaces both the header row and value row with `animate-shimmer` blocks sized `h-4` and `h-7` respectively to mirror the proportions of the real content.

## Accessibility

- Add `role="button"` and `tabindex="0"` to each card element so keyboard users can focus and activate it without a native `<button>` wrapper.
- The currently selected card should carry `aria-pressed="true"`; all others should carry `aria-pressed="false"` so screen readers announce selection state.
- Ensure the label text inside `<span class="truncate">` is never clipped in the DOM — `truncate` is a visual CSS truncation only, and the full text must remain in the markup for screen readers.
- Keyboard activation should follow the same behaviour as a click: `Enter` or `Space` selects the card and updates the filtered view.

## Related Components

- [Cards](./cards.md) — The general-purpose card component for richer content tiles that do not need to act as inline dataset filters.
