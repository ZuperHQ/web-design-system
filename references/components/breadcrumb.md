---
component: Breadcrumb
category: Navigation & Filtering
variants: [default]
related: [toolbar-row, details-left-panel]
---

# Breadcrumb

> A navigation component that shows the user's current location within a hierarchy, letting them jump back to any ancestor level with a single click.

## Overview

The Breadcrumb renders as a horizontal bar fixed to the top of a list or detail view, displaying a parent entity link, a chevron separator, the current page title, and an optional count badge showing the total number of records. It sits flush against the top of the content panel with rounded top corners, acting as the primary orientation and navigation anchor for nested entity views. Action buttons (such as Import and Create) are pinned to its right end, keeping page-level actions visually associated with the current context.

## When to Use

- Displaying a list of child entities that were navigated to from a parent record (for example, Work Orders under a Customer).
- Providing a one-click escape back to the parent entity without using the browser back button.
- Showing the total record count for the current list alongside the page title.
- Anchoring contextual action buttons (Import, Create) so they are always visible without scrolling.
- Communicating navigation depth in any view that is two or more levels deep within the entity hierarchy.

## When NOT to Use

- Inside a slide-over or details panel header — use [Details Left Panel](./details-left-panel.md) instead, which provides its own header with breadcrumb-style parent context.
- As a standalone page title with no parent link — use [Toolbar Row](./toolbar-row.md) instead, which is designed for flat list views that have no parent entity.

## Variants

| Variant | Description |
|---------|-------------|
| default | Use for all list views reached by navigating into a parent entity; displays the parent link, chevron, current title, count badge, and right-aligned action buttons. |

## HTML Structure

```html
<!-- Breadcrumb bar — top of a child entity list view -->
<div class="flex items-center bg-white border border-gray-200 border-b-0 h-14 select-none"
     style="border-radius: 1rem 1rem 0px 0px; width: calc(100% - 0.8rem);">

  <!-- Breadcrumb trail -->
  <nav class="flex-1 py-4" aria-label="Breadcrumb">
    <ol class="w-full px-4 flex space-x-4 sm:px-6 lg:px-6">
      <div class="flex space-x-2 items-center">

        <!-- Parent link -->
        <a class="flex items-center text-lg text-gray-600 leading-tight hover:text-gray-800 cursor-pointer">
          Customers
        </a>

        <!-- Separator + current page -->
        <div class="flex items-center space-x-2">
          <i class="ti ti-chevron-right text-gray-500 font-medium"></i>
          <a class="flex items-center text-lg text-gray-700 leading-tight hover:text-gray-800 cursor-pointer">
            <span class="breadcrumb-title truncate leading-tight text-lg text-gray-800 hover:text-gray-600 font-normal"
                  style="max-width:30rem; display:inline-block;">
              Work Orders
            </span>
          </a>
        </div>

        <!-- Record count badge -->
        <span class="px-1.5 py-0.5 text-sm border border-gray-200 rounded-lg bg-gray-50 text-gray-700 leading-tight">
          1,024
        </span>

      </div>
    </ol>
  </nav>

  <!-- Right-aligned action buttons -->
  <div class="flex ml-auto items-center">
    <div class="mx-2">
      <button class="inline-flex items-center justify-center gap-1 whitespace-nowrap border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit hover:bg-gray-50 px-2 py-1.5 rounded-lg">
        <em class="ti ti-upload text-lg"></em>
        <span class="leading-tight text-base font-normal ml-1">Import</span>
      </button>
    </div>
    <div class="mx-2 mr-4">
      <button class="inline-flex items-center justify-center gap-1 whitespace-nowrap border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit hover:bg-gray-50 px-2 py-1.5 rounded-lg">
        <em class="ti ti-plus text-lg"></em>
        <span class="leading-tight text-base font-normal ml-1">Create Work Order</span>
        <i class="ti ti-chevron-down text-base ml-1"></i>
      </button>
    </div>
  </div>

</div>

<!-- Bottom border fill — connects the bar visually to the content below -->
<div class="h-0.5 bg-gray-100" style="width: calc(100% - 0.8rem);"></div>
```

## Dos & Don'ts

### Do

- Always include the parent entity as a clickable link so the user can navigate back without using the browser history.
- Use the `breadcrumb-title` class with `truncate` and a `max-width` style to prevent long entity names from overflowing the bar.
- Display the record count badge whenever the current view is a filtered or paginated list, so users understand the scope of the data shown.
- Place page-level action buttons (Import, Create) in the right-aligned slot of the Breadcrumb bar, not in the Toolbar Row below it.
- Apply `border-b-0` on the bar and the `h-0.5 bg-gray-100` fill element to create a seamless visual join with the content panel beneath.

### Don't

- Do not include more than two levels (parent + current) in the breadcrumb trail — deeper hierarchies create visual clutter and should be handled by a dedicated breadcrumb navigation pattern instead.
- Do not place filter controls or column toggles inside the Breadcrumb bar — those belong in the [Toolbar Row](./toolbar-row.md) component directly below it.
- Do not omit the `aria-label="Breadcrumb"` attribute on the `<nav>` element, as screen readers need it to distinguish this landmark from other navigation regions on the page.
- Do not use the Breadcrumb bar on top-level list views where there is no parent entity; the bar will appear orphaned and the parent link will be meaningless.

## Patterns & Rules

1. **Parent link is always interactive** — The parent segment must be a tappable `<a>` that navigates the user back to the parent entity's list or detail view; never render it as plain text.
2. **Current page is never a link** — The final segment (current page title inside `breadcrumb-title`) represents where the user already is and should not be a navigable anchor, though it may have hover styling for visual consistency.
3. **Count badge uses formatted numbers** — Large counts must be formatted with locale-appropriate thousands separators (for example, "1,024" not "1024") to match the design system's number formatting conventions.
4. **Bar width uses `calc(100% - 0.8rem)`** — This deliberate offset creates the visual shadow gap on the right edge that aligns with the panel's `shadow-xs` rounding; do not change it to `100%`.
5. **Action buttons are contextual, not global** — Only include actions that operate on the current child entity list (Import, Create); global actions such as Settings or Help must not appear here.

## Accessibility

- The wrapping `<nav>` element must carry `aria-label="Breadcrumb"` to identify it as a landmark distinct from other navigation regions.
- The parent link must be focusable and activatable via the keyboard `Enter` key; no special arrow-key navigation is required for a two-level trail.
- Screen readers announce the `<nav>` landmark label first, then traverse the `<ol>` items in order, so DOM order must match visual left-to-right reading order.

## Related Components

- [Toolbar Row](./toolbar-row.md) — Rendered immediately below the Breadcrumb bar and provides filtering, search, column management, and view-switcher controls for the same list view.
- [Details Left Panel](./details-left-panel.md) — Used inside slide-over panels and provides its own header with parent-entity context, replacing the Breadcrumb in detail-view contexts.
