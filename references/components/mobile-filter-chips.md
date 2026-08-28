---
component: Mobile Filter Chips
category: Mobile
variants: [default, active, pinned]
related: [mobile-search-bar, toolbar-row, filter-chips]
replaces: Filter Chips
---

# Mobile Filter Chips

> Horizontally scrollable chip row with scroll-snap; adapts the desktop filter chip row for mobile.

## Overview

On mobile, filter chips render as a single horizontally scrollable row anchored directly below the search bar, with `overflow-x-auto scrollbar-hide` handling overflow through native touch-scroll rather than arrow-button affordances. Each chip is taller (`h-9`) and uses fully rounded pill shapes (`rounded-full`) compared to the desktop's `rounded-lg` chips, ensuring touch targets are comfortable without requiring precise pointer accuracy. Tapping any segment of an active chip — or tapping an unset chip — opens a bottom sheet rather than an inline popover, keeping the interaction model consistent with mobile OS conventions and avoiding viewport-obscuring dropdowns.

## When to Use

- On mobile list views, job boards, or asset grids where users need to narrow records by one or more fields without navigating away from the list.
- When one or more filters should always be visible above the list content so users can see active filter state at a glance — i.e., the "pinned" pattern carried over to mobile.
- When the set of filterable fields is pre-configured (not ad-hoc) and can be represented as a known row of chips that the user swipes through horizontally.
- When the user needs to clear a single active filter in one tap without opening a filter panel or resetting all filters.
- When the screen is narrow enough that displaying filter chips alongside a search bar in one row would crowd both components — use this stacked layout (search bar above, chip row below) instead.

## When NOT to Use

- When the user is on a tablet or desktop breakpoint — use [Filter Chips](./filter-chips.md) instead, which uses arrow-button carousel overflow and desktop-appropriate `h-8 rounded-lg` chips.
- When filter selection requires complex multi-field logic or the user must choose arbitrary fields on the fly — open a dedicated filter bottom sheet built with [Drawer Panel](./drawer-panel.md) instead.
- When the only required input is a keyword search — use the search bar's own input field rather than adding a chip row with no filter fields.

## Variants

| Variant | Description |
|---------|-------------|
| default | Chip has no operator or value set; renders with a dashed border (`border-dashed border-gray-300`) and a `ti-circle-dashed-plus` icon next to the label. Tapping opens a bottom sheet to choose an operator and value. Use this state when a pinned filter field has not yet been configured by the user. |
| active | Chip has an operator and value set; renders with a solid border (`border-gray-200`), shows label, operator, value, and a remove button. Tapping the label/operator/value segment re-opens the bottom sheet to edit; tapping the remove button clears the filter immediately. Use this state once the user has set a value for a filter field. |
| pinned | Same visual treatment as active or default, but the chip is always present in the row regardless of whether a value is set — it cannot be hidden or reordered by the user. Use this variant for administrator- or system-defined filters that must remain accessible at all times. |

## HTML Structure

```html
<!-- Framework-agnostic. Mobile-optimized class names. -->
<!-- Note: env(safe-area-inset-bottom) requires viewport-fit=cover in the meta tag -->

<!-- Outer wrapper: sits below the mobile search bar, full-width, white background with bottom border -->
<div class="bg-white border-b border-gray-200 py-2">

  <!-- Scrollable chip row: touch-scroll, no scrollbar, chips never wrap -->
  <div
    class="overflow-x-auto scrollbar-hide flex gap-2 px-4"
    role="group"
    aria-label="Active filters"
  >

    <!-- Default chip: no value set (dashed border, icon + label only) -->
    <button
      type="button"
      class="flex-shrink-0 flex items-center gap-1.5 h-9 px-3 rounded-full border border-dashed border-gray-300 bg-white text-gray-500 text-sm font-normal whitespace-nowrap active:bg-gray-50"
      aria-label="Set Assigned To filter"
    >
      <i class="ti ti-circle-dashed-plus text-base"></i>
      <span class="truncate">Assigned To</span>
    </button>

    <!-- Active chip: operator set, value not yet selected -->
    <div
      class="flex-shrink-0 flex items-center h-9 rounded-full border border-gray-200 bg-white divide-x divide-gray-200 overflow-hidden"
    >
      <!-- Label segment (non-interactive, gray background) -->
      <span class="h-full flex items-center px-3 bg-gray-50 text-gray-500 text-sm whitespace-nowrap">
        Priority
      </span>
      <!-- Operator segment (tappable, opens bottom sheet) -->
      <button
        type="button"
        class="h-full flex items-center px-3 text-sm text-gray-500 whitespace-nowrap bg-white active:bg-gray-50"
        aria-label="Change Priority operator, currently: is not"
      >
        is not
      </button>
    </div>

    <!-- Active chip: label + operator + value + remove button -->
    <div
      class="flex-shrink-0 flex items-center h-9 rounded-full border border-gray-200 bg-white divide-x divide-gray-200 overflow-hidden"
    >
      <!-- Label segment (non-interactive, gray background) -->
      <span class="h-full flex items-center px-3 bg-gray-50 text-gray-500 text-sm whitespace-nowrap">
        Status
      </span>
      <!-- Operator + value segment (tappable together, opens bottom sheet to edit) -->
      <button
        type="button"
        class="h-full flex items-center gap-1 px-3 text-sm whitespace-nowrap bg-white active:bg-gray-50"
        aria-label="Edit Status filter, currently: is Open"
      >
        <span class="text-gray-500">is</span>
        <span class="text-gray-700 font-medium">Open</span>
      </button>
      <!-- Remove button -->
      <button
        type="button"
        class="h-full flex items-center justify-center px-2.5 bg-white active:bg-gray-50"
        aria-label="Remove Status filter"
      >
        <i class="ti ti-x text-base text-gray-500"></i>
      </button>
    </div>

    <!-- Active chip: multiple values selected -->
    <div
      class="flex-shrink-0 flex items-center h-9 rounded-full border border-gray-200 bg-white divide-x divide-gray-200 overflow-hidden"
    >
      <!-- Label segment (non-interactive, gray background) -->
      <span class="h-full flex items-center px-3 bg-gray-50 text-gray-500 text-sm whitespace-nowrap">
        Assigned To
      </span>
      <!-- Operator + value segment (tappable together, opens bottom sheet to edit) -->
      <button
        type="button"
        class="h-full flex items-center gap-1 px-3 text-sm whitespace-nowrap bg-white active:bg-gray-50"
        aria-label="Edit Assigned To filter, currently: is 3 selected"
      >
        <span class="text-gray-500">is</span>
        <span class="text-gray-700 font-medium">3 selected</span>
      </button>
      <!-- Remove button -->
      <button
        type="button"
        class="h-full flex items-center justify-center px-2.5 bg-white active:bg-gray-50"
        aria-label="Remove Assigned To filter"
      >
        <i class="ti ti-x text-base text-gray-500"></i>
      </button>
    </div>

  </div>

</div>
```

## Dos & Don'ts

### ✅ Do

- Use `h-9` (36px) as the minimum chip height so the touch target is large enough to tap comfortably; the remove button inside an active chip must also be at least 36px tall with enough horizontal padding (`px-2.5`) to prevent mis-taps.
- Use native touch-scroll (`overflow-x-auto scrollbar-hide`) for chip row overflow — on mobile this is more discoverable and performant than arrow-button carousel controls, which require precise taps.
- Open a bottom sheet to handle operator and value selection when any chip segment is tapped; never open a desktop-style dropdown or inline popover that may be obscured by the virtual keyboard.
- Use `whitespace-nowrap` on chip text and `flex-shrink-0` on each chip so the row scrolls rather than compresses or wraps chips to a second line.
- Show "N selected" in the value slot when multiple values are active — this keeps each chip's width predictable as screen real estate is limited.

### ❌ Don't

- Do not rely on `:hover` states to reveal the remove button or any other chip action — there is no hover on touch devices; the remove button must always be visible on active chips.
- Do not place the chip row and search bar side-by-side in the same horizontal row on mobile — stack them vertically (search bar above, chip row below) so both remain fully usable at small widths.
- Do not use `rounded-lg` chip shapes from the desktop variant — mobile chips must use `rounded-full` to match the pill shape convention of mobile OS filter patterns and increase perceived tap area.
- Do not allow the chip row to push below the fold or scroll vertically with the list content — it must remain sticky below the search bar so users can always adjust filters without scrolling back to the top.
- Do not open a full-page route or modal dialog to handle filter value selection — use a bottom sheet so the user retains spatial context of the list underneath.

## Patterns & Rules

1. **Pill shape over rounded rectangle** — Mobile chips use `rounded-full` instead of the desktop's `rounded-lg`. This matches native mobile chip conventions (iOS/Android) and increases the perceived tap area at the ends of the chip where the remove button sits.
2. **Native scroll replaces arrow carousel** — The desktop carousel pattern (gradient fade + circular arrow buttons) is dropped on mobile. `overflow-x-auto scrollbar-hide` with `flex-shrink-0` chips gives native momentum scrolling on iOS and Android without JavaScript scroll listeners.
3. **Active-state instead of hover-state** — Every interactive chip segment uses `active:bg-gray-50` for tap feedback. Never use `hover:` variants as the sole visual feedback mechanism on mobile components.
4. **Operator and value share one tap target on mobile** — Unlike the desktop where operator and value are separate clickable segments, on mobile they are merged into a single `<button>` that opens the bottom sheet editor. This prevents the two segments from being too narrow to tap accurately on a small screen.
5. **Dashed border signals unset state** — Default (unset) chips use `border-dashed border-gray-300` exactly as on desktop; once any value is saved the border switches to solid `border-gray-200`. This rule is shared with the desktop variant and must not be overridden on mobile.

## Accessibility

- The chip row container must carry `role="group"` and `aria-label="Active filters"` so screen readers announce the region before reading individual chips.
- Each unset (default) chip must be a single `<button>` with `aria-label="Set [Field Name] filter"` — the `ti-circle-dashed-plus` icon is decorative and must not be read aloud.
- Each active chip's operator+value button must carry a descriptive `aria-label` such as `"Edit Status filter, currently: is Open"` so VoiceOver and TalkBack users know the current filter value before activating the button.
- Each remove button must carry `aria-label="Remove [Field Name] filter"` — do not rely on the bare `ti-x` icon to convey its purpose to assistive technology.
- Swipe-to-scroll on the chip row is handled natively by the browser's touch scroll; no custom swipe gesture handler is needed, and no additional ARIA properties are required for the scroll container itself.

## Related Components

- [Filter Chips](./filter-chips.md) — Desktop counterpart; uses `h-8 rounded-lg` chips, an arrow-button carousel for overflow, and inline popover segments. Use for web app development at tablet and desktop breakpoints instead of this component.
- [Drawer Panel](./drawer-panel.md) — The bottom sheet pattern used to handle operator and value selection when a Mobile Filter Chip is tapped; tightly coupled with this component on mobile.
- [Search Input](./search-input.md) — Sits in the row directly above the Mobile Filter Chips and handles free-text keyword search; the two components are stacked vertically and are visually and functionally complementary on mobile list views.
