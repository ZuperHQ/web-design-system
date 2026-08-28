---
component: Empty States
category: Feedback & Content
variants: [no-data, no-results]
related: [loading-shimmer, tables]
---

# Empty States

> The Empty States component communicates that a list, table, or panel contains no content, giving users context on why nothing appears and — where applicable — a direct action to remedy it.

## Overview

An empty state renders as a vertically centered block inside its parent container, pairing a large muted icon (`text-gray-300`, `font-size: 4rem`) with a short headline, an optional supporting sentence, and an optional call-to-action button. It sits inside the same surface that would ordinarily hold records — a table cell, a card body, or a panel — so the surrounding chrome (border, header, padding) remains visible. The component serves a dual design-system role: it prevents blank white voids that disorient users, and it turns a dead end into a recoverable moment.

## When to Use

- A data table returns zero rows because the module has no records yet — show the no-data variant with a "Create" action button so users know how to add their first record.
- A filter panel has no active filters — show the no-results variant inside the panel body to prompt users to add their first filter condition.
- A search or filter operation returns zero matches — replace the empty list body with the no-results variant and offer a "Clear filters" or "Try different keywords" suggestion.
- A detail drawer or side panel has no associated sub-records (e.g., no tasks on a new work order) — embed the no-data variant in that panel section.
- A page section is awaiting a feature that has not been configured — use the no-data variant with a descriptive supporting line rather than leaving blank space.

## When NOT to Use

- While data is loading — use [Tables](./tables.md) with the loading shimmer variant (`animate-shimmer` skeleton rows) instead; do not show an empty state before the fetch completes.
- When an error has occurred during a data fetch — use a dedicated error state with a retry action rather than an empty state, which implies the dataset is simply vacant.

## Variants

| Variant | Description |
|---------|-------------|
| no-data | Use when the module genuinely has no records — this is a first-run or fully cleared state. Pair with a primary "Create" action button so users can immediately add content. |
| no-results | Use when data exists but the current filter or search query matches nothing. Omit the "Create" action and instead offer an affordance to adjust or reset the query. |

## HTML Structure

```html
<!-- Standalone page section (no-data variant) -->
<div class="flex flex-col items-center justify-center py-16 text-center">
  <i class="ti ti-briefcase text-gray-300 mb-3" style="font-size:4rem"></i>
  <div class="text-base text-gray-600">No work orders found</div>
  <div class="text-sm text-gray-600 mt-1">Try adjusting your filters or create a new work order.</div>
  <button class="inline-flex items-center h-9 px-4 rounded-lg border border-gray-300 shadow-xs text-base text-gray-600 bg-white mt-4">
    Create Work Order
  </button>
</div>

<!-- Inside a table cell (no-data variant — minimal) -->
<table class="w-full" style="table-layout:fixed;border-collapse:collapse;">
  <tbody>
    <tr>
      <td class="h-36 text-center align-middle">
        <h4 class="font-medium text-gray-500 text-base">No data found</h4>
      </td>
    </tr>
  </tbody>
</table>

<!-- Inside a panel body (no-results variant) -->
<div class="flex flex-col justify-center space-y-2 items-center px-3 py-12">
  <i class="ti ti-adjustments-off text-gray-300 pb-2" style="font-size:3rem"></i>
  <p class="text-base text-gray-500 text-center">No filters added yet. Add a filter to narrow down your results.</p>
  <button type="button" class="flex space-x-2 w-fit mt-3 px-2 rounded-md py-1.5 cursor-pointer text-blue-500 hover:bg-blue-100">
    <div class="h-5 w-5 rounded-full flex justify-center items-center bg-blue-500">
      <i class="ti ti-plus text-white flex justify-center items-center text-sm"></i>
    </div>
    <span class="font-medium">Add filter</span>
  </button>
</div>
```

## Dos & Don'ts

### Do

- Choose an icon from the Tabler icon set (`ti ti-*`) that relates to the specific record type or context (e.g., `ti ti-briefcase` for work orders, `ti ti-adjustments-off` for filters).
- Keep the headline to five words or fewer and write it in sentence case — "No work orders found", not "THERE ARE NO WORK ORDERS".
- Include a supporting sentence only when the reason for emptiness is not obvious; one sentence is the maximum.
- Pair the no-data variant with a single call-to-action button styled with `border border-gray-300 shadow-xs` to remain visually subordinate to primary page actions.
- Size the icon at `font-size: 3rem` to `4rem` and color it `text-gray-300` so it reads as decorative, not alarming.

### Don't

- Do not show an empty state while data is still loading — the shimmer rows in the [Tables](./tables.md) component handle that state, and switching from empty to loaded causes layout shift.
- Do not place more than one call-to-action button inside an empty state — multiple actions dilute the single-next-step clarity that makes this component useful.
- Do not use error-tone colors (`text-red-*`, `bg-red-*`) for the icon or text — the empty state is informational, not a failure, and red creates false urgency.
- Do not embed lengthy instructional copy in the supporting sentence — if users need onboarding guidance, that belongs in a help tooltip or documentation link, not in the empty state body.
- Do not skip the icon in a no-data or no-results state that appears in a large open area; without the icon the white space looks broken rather than intentional.

## Patterns & Rules

1. **Icon–context pairing** — Always use an icon that matches the absent entity, not a generic placeholder. A filters panel uses `ti ti-adjustments-off`; a records list for work orders uses `ti ti-briefcase`. Consistent pairing trains users to read the icon as a content cue.
2. **Vertical centering inside the host surface** — Apply `flex flex-col items-center justify-center` directly on the empty state container and set an explicit vertical padding (`py-12` to `py-16`) rather than relying on the parent's height, so the block stays centred in both fixed-height and auto-height hosts.
3. **Single recoverable action** — When the empty state is actionable, expose exactly one button. Use the ghost/outline button style (`border border-gray-300 shadow-xs bg-white`) for create actions, and a text-link style (`text-blue-500 hover:bg-blue-100`) for filter or navigation actions.
4. **No empty state inside a loading container** — Gate the empty state render on the data fetch completing and the result set being confirmed empty; never render it as a default that data later replaces.
5. **Minimal variant for table cells** — When space is constrained (e.g., an inline table body), reduce the component to a single `<td class="h-36 text-center align-middle">` containing only the headline text — drop the icon and action button to avoid overflow in narrow column spans.

## Accessibility

- Wrap the empty state region in a `role="status"` attribute so screen readers announce when the container transitions from populated to empty without requiring user focus.
- The call-to-action button must have a visible focus ring and be reachable via Tab; do not suppress the browser default outline without providing a custom `focus-visible` replacement.
- The decorative icon (`<i class="ti ti-...">`) must carry `aria-hidden="true"` so screen readers skip it and announce only the headline and supporting text.

## Related Components

- [Tables](./tables.md) — Tables use the empty state component as their zero-row body variant; see the table docs for how to embed it inside a `<td>` spanning all columns.
- [Loading Shimmer](./loading-shimmer.md) — Loading shimmer replaces the empty state while a data fetch is in flight; the two components are mutually exclusive within the same container.
