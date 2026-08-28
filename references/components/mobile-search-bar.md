---
component: Mobile Search Bar
category: Mobile
variants: [default, with-active-filter-badge]
related: [mobile-filter-chips, search-input, toolbar-row]
replaces: Toolbar Row
---

# Mobile Search Bar

> Simplified sticky top search bar with filter icon; replaces the multi-group desktop toolbar on mobile.

## Overview

The Mobile Search Bar is a single-row, full-width strip pinned to the top of list and grid views on mobile. It collapses the desktop Toolbar Row's three-zone layout — filter trigger, chip carousel, and right-zone actions — into two elements: a horizontally stretching search input and a filter icon button showing an active-filter badge when needed. Because touch viewports cannot accommodate horizontal chip carousels at usable sizes, active filter state is communicated through the badge count on the filter button rather than inline chips; tapping the button opens a full-screen or bottom-sheet filter panel instead. The bar sits flush with the top of the content area and uses `border-b` to anchor it visually before the list begins.

## When to Use

- At the top of any mobile list view, kanban board, or data grid that also uses the [Toolbar Row](./toolbar-row.md) on desktop.
- When the user needs to keyword-search a large dataset from a touch device and trigger column or field-level filters without the filter panel open.
- When active filter state must be communicated at a glance without inline chips — a badge count on the filter icon serves this role.
- When the mobile view needs a persistent, always-visible search affordance that does not scroll away with the list content.
- When transitioning a view from desktop to mobile and the three-zone Toolbar Row would not fit legibly within a 360–430 px viewport.

## When NOT to Use

- When building for desktop or tablet landscape — use [Toolbar Row](./toolbar-row.md) instead, which exposes filter chips inline and supports multi-column view controls.
- When the list is short, static, and non-filterable (fewer than 20 items with no server-side query) — use a plain [Search Input](./search-input.md) without the filter button.
- When the page already renders a full-screen filter panel that the user must close before returning to the list — do not double up with the Mobile Search Bar's filter trigger on the same screen.

## Variants

| Variant | Description |
|---------|-------------|
| default | No filters are currently active; the filter icon button has no badge; use this as the initial render state before the user has applied any filters. |
| with-active-filter-badge | One or more filters are active; a small numeric badge overlays the top-right corner of the filter icon button to indicate the count; use this whenever at least one filter value is set. |

## HTML Structure

```html
<!-- Mobile Search Bar — sticky top bar, sits inside the view's scroll container header -->
<!-- Requires viewport-fit=cover in the meta tag for safe-area support -->
<div class="bg-white border-b border-gray-200 px-4 py-2 flex items-center gap-2 select-none sticky top-0 z-10">

  <!-- Search input: stretches to fill remaining space -->
  <div class="relative flex-1">
    <input
      type="search"
      inputmode="search"
      placeholder="Search"
      aria-label="Search"
      class="w-full h-11 rounded-xl border border-gray-200 bg-gray-50 pl-10 pr-4 text-base text-gray-700 outline-none focus:border-gray-400 focus:bg-white transition-colors"
    >
    <!-- Search icon: pointer-events-none so taps reach the input -->
    <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center justify-center pl-3 text-gray-400">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
      </svg>
    </div>
  </div>

  <!-- Filter button: default state (no active filters) -->
  <button
    type="button"
    aria-label="Filter"
    class="relative flex items-center justify-center h-11 w-11 rounded-xl border border-gray-200 bg-gray-50 text-gray-500 flex-shrink-0"
  >
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"/>
    </svg>
  </button>

  <!-- Filter button: with-active-filter-badge state (N filters active) -->
  <!--
  <button
    type="button"
    aria-label="Filter, 2 active"
    class="relative flex items-center justify-center h-11 w-11 rounded-xl border border-blue-300 bg-blue-50 text-blue-600 flex-shrink-0"
  >
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <polygon points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"/>
    </svg>
    <span
      class="absolute -top-1.5 -right-1.5 flex items-center justify-center h-5 min-w-5 px-1 rounded-full bg-blue-600 text-white text-xs font-semibold leading-none"
      aria-hidden="true"
    >
      2
    </span>
  </button>
  -->

</div>
```

## Dos & Don'ts

### ✅ Do

- Make the search input at least `h-11` (44 px) tall and the filter button `h-11 w-11` so both are reachable without precision tapping.
- Apply `sticky top-0 z-10` to the bar wrapper so it remains visible as the list below scrolls; the user should never need to scroll back to the top to search.
- Set `inputmode="search"` and `type="search"` on the input so iOS and Android activate the correct keyboard with a Search action key.
- Use `bg-gray-50` as the input resting background and transition to `bg-white` on focus — this gives clear visual feedback without relying on border-color change alone on high-brightness displays.
- Update the filter button's `aria-label` to `"Filter, N active"` and render the badge whenever `N >= 1`; clear both when filters are reset.

### ❌ Don't

- Do not render the full filter chip carousel from the desktop Toolbar Row inside this component — chips at `h-8` are below the 44 px touch target minimum and the horizontal carousel is cramped at mobile widths.
- Do not use `:hover` states to reveal the filter icon or any other control — mobile browsers do not emit hover events reliably, and touch users will never see hover-only affordances.
- Do not place the Mobile Search Bar inside a scrollable div — it must be `sticky` or `fixed` relative to the viewport, or it will scroll away with the list content.
- Do not omit the `border-b` separator — without it the bar visually merges with list cards when both have white backgrounds, making the viewport boundary ambiguous.
- Do not show a badge value higher than 99; cap display at "99+" if the count somehow exceeds that so the badge does not overflow its rounded-full container.

## Patterns & Rules

1. **Two-element layout, no wrapping** — The bar holds exactly two children: a `flex-1` search input and a `flex-shrink-0` filter button. No view-switcher, columns button, or chip row belongs here; those controls live in dedicated mobile panels reached from within the filter sheet.
2. **Badge encodes active filter count** — The numeric badge on the filter button is the sole on-screen signal that filters are active; its value must equal the count of filters with an applied value, matching the same count logic used by the desktop Toolbar Row's filter badge.
3. **Filter button state change on activation** — When the badge is visible, the button border shifts from `border-gray-200` to `border-blue-300` and the background from `bg-gray-50` to `bg-blue-50` so the active state is distinguishable by color as well as by count.
4. **Safe-area padding on the parent view** — The bar itself does not need safe-area insets because it sits at the top; however, the list container below it must account for `pb-[max(1rem,env(safe-area-inset-bottom))]` so list items are not clipped by the home indicator on notched devices.
5. **No horizontal scroll in the bar** — Unlike the Toolbar Row's chip carousel, this component never introduces horizontal overflow; `overflow-hidden` on the wrapper prevents any child from accidentally causing sideways scrolling in the view.

## Accessibility

- The search input must carry `aria-label="Search"` in addition to the `placeholder` attribute, since `placeholder` alone is not a reliable accessible label across screen readers.
- The filter button must have its `aria-label` updated dynamically: `"Filter"` when no filters are active and `"Filter, N active"` (e.g. `"Filter, 3 active"`) when a badge is shown, so VoiceOver and TalkBack announce the current filter state without the user needing to locate the badge.
- The badge `<span>` must carry `aria-hidden="true"` because the count is already embedded in the button's `aria-label`; without this, screen readers double-announce the number.
- Both the search input and the filter button must be reachable by sequential focus (Tab on Bluetooth keyboards, linear swipe on iOS VoiceOver) in DOM order — input first, button second — with no `tabindex` manipulation required.
- Swipe-to-dismiss on the filter panel opened by the button is a touch-only affordance; the panel must also expose a labeled close button so keyboard and switch-access users can dismiss it.

## Related Components

- [Toolbar Row](./toolbar-row.md) — Desktop counterpart; provides the full three-zone layout with inline filter chips, search input, column controls, and view switcher. Use for any breakpoint wider than the mobile threshold.
- [Filter Chips](./filter-chips.md) — The chip components that appear inside the filter panel triggered by this bar's filter button; not rendered inline on mobile but still drive the underlying filter state.
- [Search Input](./search-input.md) — The standalone search input component used in non-filterable contexts; use when no filter button is needed alongside the search field.
