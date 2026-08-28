---
component: Cards
category: Data Display
variants: [address-card, record-card]
related: [badges-and-tags, stats-cards]
---

# Cards

> Cards are self-contained surface components that group related metadata and actions for a single entity, giving users a quick summary without navigating away.

## Overview

Cards in the Zuper design system appear as white, lightly bordered rounded containers (`rounded-lg`, `border-border`) that hold an icon-labeled header, a primary value, and optional hover-revealed action buttons. They serve two distinct roles: compact field-level data tiles used inside detail panels (the base card), and larger entity-level summaries such as the address card and record card. Together they provide a consistent pattern for surfacing structured data at a glance across the product.

## When to Use

- Displaying a single named field and its value inside a job or customer detail panel (e.g., Scheduled Date, Job Value, Tasks).
- Showing a customer or company summary — name, organisation, category, and financial figures — in a list or sidebar without opening the full record.
- Presenting a service address and billing address side-by-side with an inline map preview.
- Surfacing quick-action shortcuts (email, phone, edit) that should remain hidden until the user hovers, reducing visual noise.
- Grouping a small set of related read-only or editable metadata that does not warrant a full form layout.

## When NOT to Use

- Displaying aggregate counts or monetary totals for filtering a list — use [Stats Cards](./stats-cards.md) instead, which are designed for clickable summary metrics.
- Showing a simple label-value pair inline inside a form — use [Form Layout](./form-layout.md) instead, which provides consistent label alignment and spacing.

## Variants

| Variant | Description |
|---------|-------------|
| address-card | Use when you need to show service and billing addresses together with a map thumbnail; supports an inline edit action revealed on hover over the card header. |
| record-card | Use when summarising a CRM-style entity (customer, organisation) with an initials avatar, linked name, notes count, detail rows, and contextual email/phone actions that appear on hover. |

## HTML Structure

```html
<!-- BASE CARD — field tile with hover actions -->
<div class="bg-white border border-border flex flex-col group/card h-fit p-2.5 relative rounded-lg space-y-2">
  <div class="flex items-center justify-between gap-2">
    <div class="flex items-center space-x-1 min-w-0">
      <i class="flex-shrink-0 text-gray-500 text-lg ti ti-calendar-due"></i>
      <span class="text-md text-gray-500 leading-tight truncate">Scheduled Date</span>
    </div>
    <!-- Hover actions (opacity-0 by default, revealed via group-hover/card) -->
    <div class="flex items-center gap-0.5 flex-shrink-0 opacity-0 group-hover/card:opacity-100 transition-opacity duration-150 absolute right-2 bg-white">
      <button type="button" class="rounded flex items-center text-gray-500 hover:text-gray-800 transition-colors" title="Edit">
        <i class="leading-none p-1 text-md ti ti-pencil"></i>
      </button>
    </div>
  </div>
  <span class="font-medium leading-tight text-gray-800 text-lg">17-Jun → 28-Jun</span>
</div>

<!-- ADDRESS CARD -->
<div class="space-y-2 group/addr">
  <!-- Header with hover-revealed edit button -->
  <div class="p-1.5 flex items-center space-x-3">
    <div class="flex items-center gap-1.5 text-lg font-medium leading-tight text-gray-700">
      <i class="ti ti-current-location"></i>
      Address
    </div>
    <span class="inline-flex items-center space-x-3 invisible opacity-0 group-hover/addr:visible group-hover/addr:opacity-100 transition-opacity duration-150">
      <button type="button" class="p-1 flex items-center justify-center border border-border rounded-lg transition-colors duration-200 cursor-pointer text-gray-500 hover:text-gray-800 hover:bg-gray-100 bg-white" title="Edit">
        <i class="ti ti-pencil"></i>
      </button>
    </span>
  </div>
  <!-- Card body -->
  <div class="flex items-stretch rounded-xl bg-white border border-border overflow-hidden">
    <!-- Left: address content -->
    <div class="flex-1 p-4 min-w-0">
      <div class="grid grid-cols-2 space-x-2">
        <!-- Service Address -->
        <div class="flex flex-col space-y-1.5">
          <p class="text-base leading-tight text-gray-500">Service Address</p>
          <div class="flex flex-col space-y-1">
            <div class="flex items-center space-x-1.5">
              <p class="text-base text-gray-600 truncate leading-tight">John Doe</p>
              <div class="flex items-center space-x-1.5">
                <a class="cursor-pointer rounded-full flex items-center hover:text-gray-600 text-gray-500" href="tel:9998887776">
                  <i class="ti ti-phone text-base leading-none"></i>
                </a>
                <a class="rounded-full text-gray-500 flex items-center hover:text-gray-600" href="mailto:john@example.com">
                  <i class="ti ti-mail text-base leading-none"></i>
                </a>
              </div>
            </div>
            <p class="text-base text-gray-600 leading-relaxed">
              5/347, Ambedkar Main Rd,<br>Chennai, Tamil Nadu — 600096<br>IN
            </p>
          </div>
        </div>
        <!-- Billing Address (same structure as Service Address) -->
      </div>
      <!-- Maps link -->
      <div class="mt-1.5">
        <a class="inline-flex items-center gap-1.5 px-1.5 py-1 text-base border border-border rounded-lg text-gray-500 hover:text-gray-600 transition-colors cursor-pointer">
          <i class="ti ti-external-link text-base"></i>
          <span class="leading-tight">Maps</span>
        </a>
      </div>
    </div>
    <!-- Right: map preview -->
    <div class="w-2/5 flex-shrink-0 relative overflow-hidden rounded-r-xl group/map bg-gray-100">
      <div class="absolute inset-0 z-10 pointer-events-none flex items-center justify-center">
        <i class="ti ti-map-pin-share text-2xl text-gray-500 p-2 bg-white rounded-full opacity-0 scale-75 group-hover/map:opacity-100 group-hover/map:scale-100 transition-all duration-200 ease-out"></i>
      </div>
      <div class="absolute inset-0 transition-opacity duration-200 group-hover/map:opacity-30 bg-white opacity-0"></div>
      <div class="w-full h-full flex items-center justify-center text-gray-300">
        <i class="ti ti-map-2 text-4xl"></i>
      </div>
    </div>
  </div>
</div>

<!-- RECORD CARD -->
<div class="p-2.5 border border-border hover:border-gray-300 rounded-lg space-y-2.5 group/card">
  <!-- Header row -->
  <div class="flex items-center justify-between gap-2">
    <div class="relative flex items-center space-x-2.5 min-w-0 flex-1">
      <!-- Initials avatar -->
      <div class="inline-flex overflow-hidden rounded-md flex-shrink-0 border border-border">
        <div class="flex items-center justify-center overflow-hidden uppercase text-base leading-tight bg-gray-100 text-gray-600 h-5 min-w-5 flex-shrink-0">Z</div>
      </div>
      <!-- Name -->
      <button type="button" class="text-base text-gray-600 truncate hover:text-blue-500 cursor-pointer leading-tight text-left">Acme Corporation</button>
      <!-- Notes count -->
      <button type="button" class="px-1 py-0.5 flex items-center gap-x-1 shadow-sm justify-center border border-border text-gray-500 hover:text-gray-600 rounded-lg transition-opacity duration-200 shrink-0 cursor-pointer">
        <i class="ti ti-notes"></i>
        <span class="leading-tight text-base">1</span>
      </button>
    </div>
    <!-- Hover action buttons -->
    <div class="flex items-center space-x-2 flex-shrink-0 opacity-0 pointer-events-none transition-opacity duration-200 group-hover/card:opacity-100 group-hover/card:pointer-events-auto">
      <button type="button" class="flex flex-shrink-0 border border-gray-200 text-gray-500 hover:text-gray-700 hover:bg-gray-100 rounded-lg items-center justify-center h-7 w-7 cursor-pointer" title="Email">
        <em class="ti ti-mail text-lg"></em>
      </button>
      <button type="button" class="flex flex-shrink-0 border border-gray-200 text-gray-500 hover:text-gray-700 hover:bg-gray-100 rounded-lg items-center justify-center h-7 w-7 cursor-pointer" title="Phone">
        <em class="ti ti-phone text-lg"></em>
      </button>
    </div>
  </div>
  <!-- Detail rows -->
  <div class="flex items-center space-x-3 ml-1 text-gray-500">
    <i class="ti ti-building flex items-center justify-center text-base"></i>
    <button type="button" class="text-md leading-tight truncate min-w-0 hover:text-blue-500 text-left">Acme Organisation</button>
  </div>
  <div class="flex items-center space-x-3 ml-1 text-gray-500">
    <i class="ti ti-subtask flex items-center justify-center text-base"></i>
    <span class="text-md leading-tight truncate min-w-0">Residential</span>
  </div>
  <div class="flex items-center space-x-3 ml-1 text-gray-500">
    <i class="ti ti-coin flex items-center justify-center text-base"></i>
    <span class="text-md leading-tight truncate min-w-0">Credits: $24.00</span>
  </div>
  <div class="flex items-center space-x-3 ml-1 text-gray-500">
    <i class="ti ti-report-money flex items-center justify-center text-base"></i>
    <span class="text-md leading-tight truncate min-w-0">Receivables: $13,422.10</span>
  </div>
</div>
```

## Dos & Don'ts

### ✅ Do

- Apply `group/card` on the root card element and use `group-hover/card:opacity-100` on action button containers so hover actions are revealed consistently.
- Use `truncate` and `min-w-0` on text inside flex containers to prevent layout overflow when names or values are long.
- Use `font-mono` on monetary values (e.g., `font-mono`) to keep decimal points and currency symbols visually aligned.
- Keep card width constrained with a fixed or max-width so detail rows do not stretch awkwardly in wide viewports.
- Use the `border-border` token for card borders and switch to `hover:border-gray-300` on clickable or hoverable cards to signal interactivity.

### ❌ Don't

- Do not embed deeply nested interactive components (dropdowns, date pickers) inside a card — the card hover state will conflict with those components' own focus management.
- Do not omit the `title` attribute from hover-only icon buttons — screen readers cannot infer the action from the icon alone, making them inaccessible.
- Do not use a record card to display aggregated statistics — the record card is designed for entity identity, and numeric summaries belong in [Stats Cards](./stats-cards.md).
- Do not hard-code inline `style="width:…"` for base field cards when a Tailwind width utility will suffice — keeping sizing in utility classes makes responsive overrides easier.
- Do not place more than two to three detail rows in a record card — beyond that, the card becomes a substitute for the full detail view and should link through instead.

## Patterns & Rules

1. **Group hover reveal** — All action buttons inside a card must start at `opacity-0 pointer-events-none` and be revealed via the Tailwind group-hover variant (`group-hover/card:opacity-100 group-hover/card:pointer-events-auto`), never shown by default, to keep the surface clean.
2. **Named group scoping** — Use named group variants (`group/card`, `group/addr`, `group/map`) whenever cards are nested or rendered in close proximity to avoid unintended hover bleed-through to sibling cards.
3. **Monetary formatting** — Any value representing money must use `font-mono` so currency symbols and decimal separators remain visually aligned across multiple cards.
4. **Initials avatar sizing** — The initials avatar in a record card uses `h-5 min-w-5` with `uppercase` text; do not increase the size, as it is calibrated to align with the `text-base` entity name on the same row.
5. **Map preview aspect** — In the address card, the map panel is `w-2/5 flex-shrink-0`; do not remove `flex-shrink-0` or the panel will collapse when address text is long.

## Accessibility

- Hover-only action buttons (email, phone, edit) must carry a descriptive `title` attribute; assistive technologies use this as the accessible name since no visible label is present.
- Cards that are fully clickable (clickable base card variant) must be a `<button>` or an `<a>` with an appropriate `href` — never a `<div>` with a click handler — so they are reachable and activatable via keyboard Tab and Enter.
- The notes count button in the record card header must be reachable via Tab and should convey both the icon meaning and the count in its accessible name (e.g., `aria-label="1 note"`).

## Related Components

- [Stats Cards](./stats-cards.md) — Stats cards are clickable metric tiles for filtering lists by aggregate count or value; use them when the card represents a summary that drives list filtering rather than an individual entity.
