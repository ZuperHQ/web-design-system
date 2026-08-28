---
component: Action Sheet
category: Mobile
variants: [single-group, destructive]
related: [bottom-sheet, mobile-nav-bar, dropdown-menu]
replaces: Dropdown Menu
---

# Action Sheet

> Full-width grouped action list at the bottom of the screen; replaces contextual dropdown menus on mobile.

## Overview

The Action Sheet is a full-width overlay panel that slides up from the bottom of the screen, presenting a grouped list of actions the user can take on a record or context. Unlike the desktop Dropdown Menu — which floats anchored to a trigger element and relies on hover states — the Action Sheet occupies the entire screen width, uses large touch-friendly tap targets (`h-11` minimum), and is dismissed by tapping a backdrop or dragging down. It always accounts for the device's safe area at the bottom via `pb-[max(1rem,env(safe-area-inset-bottom))]` to avoid overlap with the home indicator on notchless devices and the home bar on newer iPhones. The Action Sheet is the primary pattern for surfacing contextual record-level commands in the Zuper mobile experience.

## When to Use

- Presenting record-level actions (e.g., Edit, Reassign, Mark Complete, Delete) triggered by a long-press or a tapping a "more" (`ti ti-dots`) overflow button on a mobile list row or detail header.
- Offering creation shortcuts for related entity types (e.g., new Job, Quote, or Invoice) from a mobile FAB or toolbar button when more than two options exist.
- Replacing an inline row of icon buttons when three or more actions would crowd the available width on a 375 px viewport.
- Grouping a destructive action (Delete, Archive) visually apart from safe actions when the consequence of a mistap would be significant.
- Confirming a state change that does not require a full modal form — for example, choosing a new status from a list before committing.

## When NOT to Use

- When building for desktop or tablet-width viewports — use [Dropdown Menu](./dropdown-menu.md) instead, which anchors to the trigger element and does not consume the full screen width.
- When the user must choose a value to populate a form field — use the mobile-adapted [Select Dropdown](./select-dropdown.md) instead, which provides proper form binding and scrollable option lists.
- When the interaction requires explanatory copy, a confirmation message with a body paragraph, or any form input — use [Modal / Dialog](./modal-dialog.md) instead, which provides a title, body, and cancel/confirm button pair.

## Variants

| Variant | Description |
|---------|-------------|
| single-group | All actions belong to one logical group with equal weight; use when no action is destructive and there is no need to visually separate items by risk level. |
| destructive | Actions are split into two groups — safe actions above, a destructive action (Delete, Remove, Archive) below — separated by a gap and rendered inside a visually distinct second container with red text; use whenever at least one action is irreversible. |

## HTML Structure

```html
<!-- Framework-agnostic. Requires viewport-fit=cover in the meta tag for env() to work:
     <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> -->

<!-- Backdrop — tap to dismiss -->
<div class="fixed inset-0 z-40 bg-black/40" aria-hidden="true"></div>

<!-- Action Sheet root — single-group variant -->
<div
  role="dialog"
  aria-modal="true"
  aria-label="Record actions"
  class="fixed bottom-0 left-0 right-0 z-50 px-4 pb-[max(1rem,env(safe-area-inset-bottom))]"
>
  <!-- Optional: drag handle for swipe-to-dismiss affordance -->
  <!-- Handle lives inside the action group container, not above it -->

  <!-- Action group -->
  <div class="bg-white rounded-2xl overflow-hidden shadow-2xl divide-y divide-gray-100">
    <!-- Optional group label -->
    <div class="px-4 py-3 text-center">
      <span class="text-sm text-gray-400 font-medium">Job #ZJ-00421</span>
    </div>
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-gray-800 text-left active:bg-gray-100">
      <i class="text-gray-500 text-xl ti ti-edit"></i>
      <span class="truncate">Edit</span>
    </button>
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-gray-800 text-left active:bg-gray-100">
      <i class="text-gray-500 text-xl ti ti-user-check"></i>
      <span class="truncate">Reassign</span>
    </button>
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-gray-800 text-left active:bg-gray-100">
      <i class="text-gray-500 text-xl ti ti-circle-check"></i>
      <span class="truncate">Mark Complete</span>
    </button>
  </div>

  <!-- Cancel button — always a separate container below the action group -->
  <div class="mt-3">
    <button type="button" class="w-full h-11 bg-white rounded-2xl text-base font-medium text-gray-800 shadow-2xl active:bg-gray-100">
      Cancel
    </button>
  </div>
</div>

<!-- ─────────────────────────────────────────── -->

<!-- Action Sheet root — destructive variant -->
<div
  role="dialog"
  aria-modal="true"
  aria-label="Record actions"
  class="fixed bottom-0 left-0 right-0 z-50 px-4 pb-[max(1rem,env(safe-area-inset-bottom))]"
>
  <!-- Safe actions group -->
  <div class="bg-white rounded-2xl overflow-hidden shadow-2xl divide-y divide-gray-100">
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-gray-800 text-left active:bg-gray-100">
      <i class="text-gray-500 text-xl ti ti-edit"></i>
      <span class="truncate">Edit</span>
    </button>
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-gray-800 text-left active:bg-gray-100">
      <i class="text-gray-500 text-xl ti ti-download"></i>
      <span class="truncate">Export</span>
    </button>
  </div>

  <!-- Destructive group — separate container with mt-3 gap, not a divider -->
  <div class="mt-3 bg-white rounded-2xl overflow-hidden shadow-2xl">
    <button type="button" class="flex gap-3 items-center w-full h-11 px-4 text-base text-red-500 text-left active:bg-red-50">
      <i class="text-xl ti ti-trash"></i>
      <span class="truncate">Delete</span>
    </button>
  </div>

  <!-- Cancel button -->
  <div class="mt-3">
    <button type="button" class="w-full h-11 bg-white rounded-2xl text-base font-medium text-gray-800 shadow-2xl active:bg-gray-100">
      Cancel
    </button>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Always render the Cancel button as its own standalone container beneath the action groups, not as a final item inside an action group — the visual gap signals to users that it is a dismissal control, not an action.
- Apply `pb-[max(1rem,env(safe-area-inset-bottom))]` to the root container so the Cancel button never sits behind the device home indicator; this requires `viewport-fit=cover` in the page's `<meta name="viewport">` tag.
- Set a minimum height of `h-11` (44 px) on every button, and ensure `px-4` horizontal padding applies — these are the minimum comfortable touch targets on mobile.
- Use `active:bg-gray-100` (and `active:bg-red-50` for destructive items) rather than `hover:` states — mobile browsers do not reliably fire hover events, and `:active` gives immediate tap feedback.
- Separate the destructive action group from the safe actions using a `mt-3` gap between two distinct `<div>` containers, not merely a `divide-y` divider within a single container — the spatial gap communicates higher risk than a hairline rule.

### Don't

- Do not use `hover:` alone to communicate interactivity on any action item — hover states are invisible on touchscreens and leave the UI feeling unresponsive.
- Do not place more than six action items across all groups in a single Action Sheet — if the list exceeds six items, consider whether a filter step or a dedicated sub-screen is more appropriate.
- Do not include form controls (text inputs, checkboxes, toggles) inside the Action Sheet panel — any interaction that requires input beyond a single tap belongs in a [Modal / Dialog](./modal-dialog.md).
- Do not omit the backdrop overlay — without it, users have no visual cue that the rest of the screen is blocked, and cannot tap outside to dismiss the sheet on implementations that support that gesture.
- Do not stack a second Action Sheet on top of an open one — if a selected action requires a follow-up choice, dismiss the first sheet and open a dedicated screen or modal instead.

## Patterns & Rules

1. **Container separation for destructive actions** — In the destructive variant, the red-tinted action lives in its own `<div class="mt-3 bg-white rounded-2xl overflow-hidden shadow-2xl">` container, not in the same container as safe actions. The physical gap (not just a rule) makes the risk legible at a glance and reduces accidental taps.
2. **Safe area compliance** — The root `fixed bottom-0` container must carry `pb-[max(1rem,env(safe-area-inset-bottom))]`. The `max()` ensures at least 1 rem of breathing room on devices where `env(safe-area-inset-bottom)` resolves to zero (older Android, desktop emulators).
3. **No selected-state indicator** — The Action Sheet does not carry a `ti ti-check` selected-state pattern. It presents actions to execute, not a current value to reflect. If the current state of a field must be visible before the user acts, add a short subtitle line below the group label, not a check icon on an item.
4. **Cancel is always last and always present** — The Cancel button must be the last element and rendered in its own container. It must never be omitted, even when the backdrop tap-to-dismiss gesture is implemented, because Android back-button behavior and accessibility tools rely on a visible, focusable dismiss control.
5. **Full-width, no anchoring** — The Action Sheet carries `left-0 right-0` and fills the full viewport width. It must never be sized or positioned relative to a trigger element. That pattern belongs to [Dropdown Menu](./dropdown-menu.md) on desktop.

## Accessibility

- The Action Sheet root container must carry `role="dialog"`, `aria-modal="true"`, and an `aria-label` that identifies the context (e.g., `"Job actions"`) so screen readers announce the overlay correctly when it appears.
- On open, focus must move to the first action button inside the sheet. On close (Cancel tap, backdrop tap, or swipe-down dismiss), focus must return to the trigger element that opened the sheet.
- The backdrop element must carry `aria-hidden="true"` so screen readers do not announce or navigate to it.
- Swipe-to-dismiss is a progressive enhancement; the Cancel button is the primary keyboard and assistive-technology dismissal path and must always be present and focusable.
- Each action button must have `type="button"` to prevent accidental form submission when the sheet is rendered inside a form context.

## Related Components

- [Dropdown Menu](./dropdown-menu.md) — Desktop counterpart; use for web app development when the viewport is wider than mobile breakpoints and the menu must anchor to a trigger element.
- [Modal / Dialog](./modal-dialog.md) — Use when the action requires a confirmation message, form input, or body copy before the user can commit.
- [Select Dropdown](./select-dropdown.md) — Use when the user is choosing a value to populate a form field rather than executing a record-level command.
