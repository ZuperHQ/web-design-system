---
component: Mobile Card
category: Mobile
variants: [record-card, address-card]
related: [mobile-button, badges-and-tags, cards]
replaces: Cards
---

# Mobile Card

> Full-width touch-optimized card with an always-visible action strip; adapts the desktop card for mobile.

## Overview

Mobile Cards are white, rounded (`rounded-xl`) containers with a soft shadow (`shadow-xs`) that stretch to full viewport width and present entity metadata in vertically stacked detail rows. Unlike their desktop counterparts, they never rely on hover to reveal actions; instead, every card carries a permanent bottom action strip with equal-width tap targets separated by hairline dividers. This eliminates the `group-hover` opacity patterns used on desktop and ensures every action is immediately reachable with a single tap on any touch device.

## When to Use

- Displaying work orders or jobs in a mobile list view where each card must show status, assignee, address, and scheduled time at a glance.
- Showing a contact or customer summary (name, role, phone, address) in a field technician's job detail screen, where Call and Navigate actions must be one tap away.
- Rendering entity-level summaries inside a scrollable feed where the card occupies the full available width and actions must never depend on a secondary gesture.
- Replacing desktop record cards or base field-tile cards in any view that is rendered inside the mobile app shell.
- Surfacing contextual quick actions (Call, Email, Navigate, More) that a technician needs while in the field without opening a full detail screen.

## When NOT to Use

- Building for the web app or desktop breakpoints — use [Cards](./cards.md) instead, which uses hover-revealed actions and constrained widths suited to multi-column layouts.
- Displaying aggregate counts or filtered metric totals — use [Stats Cards](./stats-cards.md) instead, which are designed as clickable summary tiles that drive list filtering.
- Showing a simple single-field label-value pair that does not need an action strip — use a plain detail row inside the screen body rather than a full card container.

## Variants

| Variant | Description |
|---------|-------------|
| record-card | Use when summarising a work order or job entity: shows a title/ID, a status badge in the header, two to four icon-prefixed detail rows (assignee, address, time), and a three-button action strip (e.g. Call, Email, More). |
| address-card | Use when the card's primary content is a contact or location: shows a name, a role or category badge, address and phone detail rows, and an action strip tailored to location-first actions (e.g. Call, Navigate, More). |

## HTML Structure

```html
<!-- Note: env(safe-area-inset-bottom) requires viewport-fit=cover in the meta tag -->
<!-- <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> -->

<!-- RECORD CARD — work order / job entity -->
<div class="bg-white rounded-xl shadow-xs overflow-hidden">
  <!-- Header row: title + status badge -->
  <div class="px-4 pt-3.5 pb-2.5 flex justify-between items-start">
    <div>
      <div class="font-semibold text-base text-gray-900 mb-0.5">WO-20482</div>
      <div class="text-sm text-gray-500 font-normal">AC Installation</div>
    </div>
    <!-- Status badge — color matches job status -->
    <span class="bg-emerald-100 text-emerald-800 text-xs font-semibold px-2 py-0.5 rounded-full whitespace-nowrap">In Progress</span>
  </div>

  <!-- Detail rows: icon + value -->
  <div class="px-4 pb-3 flex flex-col gap-1.5">
    <div class="flex items-center gap-2">
      <i class="ti ti-user text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">John Smith</span>
    </div>
    <div class="flex items-center gap-2">
      <i class="ti ti-map-pin text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">42 Birch Ave, Suite 4B</span>
    </div>
    <div class="flex items-center gap-2">
      <i class="ti ti-clock text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">Today, 2:00 PM – 4:00 PM</span>
    </div>
  </div>

  <!-- Action strip — always visible, never hidden behind hover -->
  <div class="border-t border-gray-100 flex">
    <!-- Each button must be at minimum h-11 (44px) to meet touch target requirements -->
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5 border-r border-gray-100"
      aria-label="Call John Smith">
      <i class="ti ti-phone text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">Call</span>
    </button>
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5 border-r border-gray-100"
      aria-label="Email John Smith">
      <i class="ti ti-mail text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">Email</span>
    </button>
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5"
      aria-label="More actions for WO-20482">
      <i class="ti ti-dots text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">More</span>
    </button>
  </div>
</div>


<!-- ADDRESS CARD — contact / location entity -->
<div class="bg-white rounded-xl shadow-xs overflow-hidden">
  <!-- Header row: name + role badge -->
  <div class="px-4 pt-3.5 pb-2.5 flex justify-between items-start">
    <div>
      <div class="font-semibold text-base text-gray-900 mb-0.5">Sarah Okafor</div>
      <div class="text-sm text-gray-500 font-normal">Site Contact</div>
    </div>
    <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2 py-0.5 rounded-full whitespace-nowrap">Primary</span>
  </div>

  <!-- Detail rows -->
  <div class="px-4 pb-3 flex flex-col gap-1.5">
    <div class="flex items-center gap-2">
      <i class="ti ti-map-pin text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">88 Harbor View Rd, Boston MA 02101</span>
    </div>
    <div class="flex items-center gap-2">
      <i class="ti ti-phone text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">+1 (617) 555-0192</span>
    </div>
    <div class="flex items-center gap-2">
      <i class="ti ti-building text-sm text-gray-400 flex-shrink-0"></i>
      <span class="text-sm text-gray-600">Harbor Realty Group</span>
    </div>
  </div>

  <!-- Action strip — location-first actions -->
  <div class="border-t border-gray-100 flex">
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5 border-r border-gray-100"
      aria-label="Call Sarah Okafor">
      <i class="ti ti-phone text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">Call</span>
    </button>
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5 border-r border-gray-100"
      aria-label="Navigate to 88 Harbor View Rd">
      <i class="ti ti-map text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">Navigate</span>
    </button>
    <button type="button"
      class="flex-1 h-11 flex flex-col items-center justify-center gap-0.5"
      aria-label="More actions for Sarah Okafor">
      <i class="ti ti-dots text-base text-primary"></i>
      <span class="text-xs text-primary font-medium">More</span>
    </button>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Always render the action strip unconditionally — do not wrap it in any hover, focus, or long-press conditional class. Technicians in the field need one-tap access to Call, Navigate, and other actions without a secondary gesture.
- Size every action strip button with at least `h-11` (44px) to meet the WCAG 2.5.5 and Apple HIG minimum touch target requirement.
- Use `flex-1` on every action strip button so all targets are equal width and easy to hit regardless of thumb position.
- Use `shadow-xs` (not `shadow-sm` or `drop-shadow`) on the card root to match the light elevation style defined in the mobile component system.
- Use `text-sm` (12px in this scale) for detail row values and `text-base` (14px in this scale) for the card title to maintain the visual hierarchy established across mobile list screens.
- Truncate long detail row values with `truncate` and wrap the text container in `min-w-0` to prevent overflow breaking the card's full-width layout.

### Don't

- Do not use `opacity-0 group-hover:opacity-100` or any `group-hover` variant on action buttons — hover does not exist on touch devices and the actions will be permanently invisible.
- Do not constrain the card with a fixed width (e.g., `w-64` or `max-w-xs`) — Mobile Cards must stretch to the full available width of the list container.
- Do not place more than four detail rows inside the card body — beyond that, the card becomes a substitute for the full detail screen and the user should be directed there via the card title link or the More action.
- Do not omit the `overflow-hidden` class from the card root — without it, the action strip's bottom corners will not be clipped to the card's `rounded-xl` border radius.
- Do not use the desktop address card's side-by-side map thumbnail panel on mobile — the map preview requires a minimum width that is not available at mobile viewport sizes; use the Navigate action in the strip instead.

## Patterns & Rules

1. **Always-visible action strip** — The action strip (`border-t border-gray-100 flex`) must always be rendered in the DOM. Never toggle its visibility or opacity based on interaction state. This is the primary structural difference from the desktop card.
2. **Equal-width tap targets** — Each button in the strip uses `flex-1` so all targets share identical width. Never use fixed widths or `auto` sizing on strip buttons, as uneven targets increase mis-tap rates on mobile.
3. **Three-button strip limit** — The strip holds a maximum of three actions. If more actions are required, the third slot must be a "More" button (`ti-dots`) that opens an [Action Sheet](./mobile-action-sheet.md) — do not add a fourth button.
4. **Status badge placement** — The status badge sits in the top-right of the header row using `whitespace-nowrap` so it never wraps or competes with the title text on narrow screens.
5. **No inline map panel** — The desktop address card's `w-2/5` map thumbnail is not used in the mobile variant. Navigation intent is served entirely by the Navigate action button in the strip, which deep-links to the device's native maps application.

## Accessibility

- Each action strip button must carry an `aria-label` that names both the action and its target entity (e.g., `aria-label="Call John Smith"`, `aria-label="Navigate to 42 Birch Ave"`), because the visible label ("Call", "Navigate") alone does not identify which entity is being acted on when multiple cards appear in a list.
- The card container itself should be a semantic `<div>` — do not make the entire card a `<button>` or `<a>`, as the action strip already provides the interactive controls. If tapping the card body should navigate to a detail screen, wrap only the header area in an `<a>` or `<button>`.
- Swipe gestures (if implemented for quick actions) must never be the only way to reach an action — the always-visible strip ensures keyboard and switch-access users can reach all actions without swiping.
- The status badge must not rely on color alone to convey state; ensure the badge text (e.g., "In Progress", "On Hold") is always present alongside the color.

## Related Components

- [Cards](./cards.md) — Desktop counterpart; uses hover-revealed action buttons and constrained widths. Use this for web app development instead of Mobile Card.
- [Mobile Button](./mobile-button.md) — Full-width `h-11` button used in card footers and action sheets; shares the same touch target sizing rules as the action strip buttons.
