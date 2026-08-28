---
component: Bottom Sheet
category: Mobile
variants: [standard, no-header, tall]
related: [confirmation-bottom-sheet, action-sheet, drawer-panel, modal-dialog]
replaces: Modal / Dialog
---

# Bottom Sheet

> Full-width overlay anchored to the bottom of the screen; replaces centered modal on mobile.

## Overview

The Bottom Sheet is a white card with rounded top corners (`border-radius: 1rem 1rem 0 0`) that slides up from the bottom edge of the viewport and spans the full screen width, sitting above a semi-transparent backdrop. On mobile, centered modals are awkward to reach and prone to being clipped by the on-screen keyboard; the bottom sheet addresses both problems by anchoring content where the thumb naturally rests and leaving room above for the keyboard to push it. Its role in the design system is to carry the same three use-cases as the desktop Modal / Dialog — confirmations, short-form data entry, and time-sensitive alerts — in a touch-first, viewport-safe wrapper that respects device safe areas.

## When to Use

- Asking the user to confirm a destructive or reversible action on a mobile record, such as deleting a customer or closing a job, where a centered dialog would be difficult to reach with one hand.
- Presenting a short inline form (2–4 fields) that must be filled before the user proceeds — for example, adding a note, entering a signature, or selecting an assignee.
- Surfacing a contextual action menu with 3–6 labeled options where an action sheet layout is preferable to a dropdown that fights the soft keyboard.
- Displaying a time-sensitive prompt such as an offline-sync warning or a session-expiry notice that requires an explicit tap to dismiss.
- Picking a value from a compact list (status, priority, category) when a native `<select>` element would break the visual design or offer insufficient styling control.

## When NOT to Use

- When building for desktop or a responsive breakpoint wider than `md` — use [Modal / Dialog](./modal-dialog.md) instead, which centers over a backdrop and uses constrained fixed widths appropriate for larger screens.
- When the content involves more than four or five form fields or requires the user to reference background content while filling in data — use [Drawer Panel](./drawer-panel.md) instead, which slides in without fully obscuring the page.
- When the user needs to perform a multi-step wizard flow that tracks progress across screens — a dedicated full-screen mobile page is more appropriate; a bottom sheet does not communicate step context well.

## Variants

| Variant | Description |
|---------|-------------|
| standard | The default variant: includes a drag handle bar, a titled header with a dismiss button, a scrollable body, and a footer action bar. Use for confirmations and short forms where the user needs orientation (a title) before acting. |
| no-header | Omit the header row entirely when the sheet content is self-explanatory — for example, a list of labeled action buttons or a single confirmation message. The drag handle remains; the body begins immediately below it. |
| tall | A taller sheet capped at `max-h-[85vh]` instead of the default `max-h-[60vh]`, used when the body content is a scrollable list (statuses, assignees, addresses) that benefits from more vertical real estate. The footer remains fixed at the bottom inside the sheet. |

## HTML Structure

```html
<!-- Bottom Sheet — standard variant -->
<!-- Requires <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> -->

<!-- Backdrop -->
<div class="fixed inset-0 z-40 bg-black/40" aria-hidden="true"></div>

<!-- Sheet container -->
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="sheet-title"
  class="fixed bottom-0 left-0 right-0 z-50 bg-white flex flex-col"
  style="border-radius:1rem 1rem 0 0;box-shadow:0 -4px 24px 0 rgba(0,0,0,0.12);max-height:60vh"
>

  <!-- Drag handle -->
  <div class="flex justify-center pt-3 pb-1 flex-shrink-0">
    <div class="w-10 h-1 rounded-full bg-gray-300"></div>
  </div>

  <!-- Header -->
  <div class="flex items-center justify-between px-5 py-3 border-b border-gray-200 flex-shrink-0">
    <h2 id="sheet-title" class="text-base font-semibold text-gray-900">Close Work Order?</h2>
    <button
      class="flex items-center justify-center h-11 w-11 rounded-full text-gray-500 hover:bg-gray-100 active:bg-gray-200"
      aria-label="Dismiss"
    >
      <i class="ti ti-x text-xl"></i>
    </button>
  </div>

  <!-- Scrollable body -->
  <div class="flex-1 overflow-y-auto px-5 py-4 text-sm text-gray-600 leading-relaxed">
    <p>This will close the work order and notify the assigned technician. You can reopen it from the work order detail page if needed.</p>
  </div>

  <!-- Footer action bar — safe area aware -->
  <div class="flex gap-3 px-5 pt-3 pb-[max(1rem,env(safe-area-inset-bottom))] border-t border-gray-200 flex-shrink-0">
    <button class="flex-1 h-11 rounded-xl border border-gray-300 text-sm font-medium text-gray-700 bg-white active:bg-gray-50">
      Cancel
    </button>
    <button class="flex-1 h-11 rounded-xl text-sm font-medium text-white bg-primary active:opacity-90">
      Close Work Order
    </button>
  </div>

</div>


<!-- Bottom Sheet — no-header variant -->
<div
  role="dialog"
  aria-modal="true"
  aria-label="Select Status"
  class="fixed bottom-0 left-0 right-0 z-50 bg-white flex flex-col"
  style="border-radius:1rem 1rem 0 0;box-shadow:0 -4px 24px 0 rgba(0,0,0,0.12);max-height:60vh"
>

  <!-- Drag handle only; no header row -->
  <div class="flex justify-center pt-3 pb-2 flex-shrink-0">
    <div class="w-10 h-1 rounded-full bg-gray-300"></div>
  </div>

  <!-- Body begins immediately (action list example) -->
  <div class="flex-1 overflow-y-auto pb-[max(1rem,env(safe-area-inset-bottom))]">
    <button class="w-full h-11 flex items-center gap-3 px-5 text-sm font-medium text-gray-800 active:bg-gray-50">
      <i class="ti ti-circle-check text-green-500 text-lg"></i>
      Mark as Complete
    </button>
    <button class="w-full h-11 flex items-center gap-3 px-5 text-sm font-medium text-gray-800 active:bg-gray-50">
      <i class="ti ti-clock-pause text-amber-500 text-lg"></i>
      Put On Hold
    </button>
    <button class="w-full h-11 flex items-center gap-3 px-5 text-sm font-medium text-red-600 active:bg-red-50">
      <i class="ti ti-trash text-lg"></i>
      Delete Work Order
    </button>
  </div>

</div>


<!-- Bottom Sheet — tall variant (scrollable list) -->
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="sheet-title-tall"
  class="fixed bottom-0 left-0 right-0 z-50 bg-white flex flex-col"
  style="border-radius:1rem 1rem 0 0;box-shadow:0 -4px 24px 0 rgba(0,0,0,0.12);max-height:85vh"
>

  <div class="flex justify-center pt-3 pb-1 flex-shrink-0">
    <div class="w-10 h-1 rounded-full bg-gray-300"></div>
  </div>

  <div class="flex items-center justify-between px-5 py-3 border-b border-gray-200 flex-shrink-0">
    <h2 id="sheet-title-tall" class="text-base font-semibold text-gray-900">Assign Technician</h2>
    <button
      class="flex items-center justify-center h-11 w-11 rounded-full text-gray-500 active:bg-gray-100"
      aria-label="Dismiss"
    >
      <i class="ti ti-x text-xl"></i>
    </button>
  </div>

  <!-- Optional search bar inside the tall sheet -->
  <div class="bg-white border-b border-gray-200 px-4 py-2 flex gap-2 flex-shrink-0">
    <div class="flex-1 flex items-center gap-2 bg-gray-100 rounded-xl px-3 h-10">
      <i class="ti ti-search text-gray-400 text-lg flex-shrink-0"></i>
      <input
        type="search"
        placeholder="Search technicians…"
        class="flex-1 bg-transparent text-sm text-gray-800 placeholder-gray-400 outline-none h-full"
      />
    </div>
  </div>

  <!-- Scrollable list body -->
  <div class="flex-1 overflow-y-auto">
    <button class="w-full h-14 flex items-center gap-3 px-5 active:bg-gray-50">
      <div class="w-9 h-9 rounded-full bg-primary/10 flex items-center justify-center text-primary text-sm font-semibold flex-shrink-0">JD</div>
      <div class="flex flex-col items-start">
        <span class="text-sm font-medium text-gray-900">James Dawson</span>
        <span class="text-xs text-gray-500">2 active jobs</span>
      </div>
      <i class="ti ti-check text-primary ml-auto text-lg" aria-hidden="true"></i>
    </button>
    <button class="w-full h-14 flex items-center gap-3 px-5 active:bg-gray-50">
      <div class="w-9 h-9 rounded-full bg-gray-100 flex items-center justify-center text-gray-600 text-sm font-semibold flex-shrink-0">MP</div>
      <div class="flex flex-col items-start">
        <span class="text-sm font-medium text-gray-900">Maria Patel</span>
        <span class="text-xs text-gray-500">Available</span>
      </div>
    </button>
  </div>

  <!-- Footer: confirm selection -->
  <div class="px-5 pt-3 pb-[max(1rem,env(safe-area-inset-bottom))] border-t border-gray-200 flex-shrink-0">
    <button class="w-full h-11 rounded-xl text-sm font-medium text-white bg-primary active:opacity-90">
      Confirm Assignment
    </button>
  </div>

</div>
```

## Dos & Don'ts

### Do

- Always include `pb-[max(1rem,env(safe-area-inset-bottom))]` on the footer container (and on no-header sheets that terminate with a button list) so content is never obscured by iPhone home indicator bars or Android gesture navigation zones.
- Size every tappable element to at least `h-11` (44 px) — buttons, list rows, icon buttons — to meet the minimum touch target threshold; small tappable regions cause tap misses on mobile without the precision of a cursor.
- Include the drag handle (`w-10 h-1 bg-gray-300 rounded-full`) as the topmost element of every sheet variant so users understand the component is swipe-dismissible and have a visual anchor for drag gestures.
- Use `active:bg-gray-50` or `active:opacity-90` instead of `:hover` states for all interactive elements inside the sheet; hover states produce no visible feedback on touch screens.
- Cap the standard sheet at `max-height:60vh` so the backdrop remains clearly visible above the sheet, giving the user spatial context and a clear tap-to-dismiss target.
- Apply `overflow-y-auto` only to the body div, never to the sheet container itself, so the header and footer stay pinned and do not scroll out of reach.

### Don't

- Do not use a fixed pixel height for the sheet — device heights vary widely across Android and iOS; always use `max-height` with viewport units so the sheet adapts rather than overflows or collapses.
- Do not rely solely on the backdrop tap to dismiss the sheet; always provide an explicit dismiss button (`ti-x`) in the header or a visible "Cancel" footer button so the action is discoverable without prior knowledge of the gesture.
- Do not open a bottom sheet on top of another bottom sheet — stacking overlays destroys spatial orientation on a small screen; if a secondary choice is needed, replace the current sheet's content or navigate to a new screen.
- Do not place more than four or five form fields in the standard variant without switching to the tall variant or a full-screen form page — content that overflows `60vh` leaves the footer action buttons invisible until the user scrolls, breaking discoverability.
- Do not use `:hover` pseudo-states as the only visual affordance for interactive rows; on mobile they never fire, making the entire action invisible until the user taps and hopes.
- Do not hard-code `padding-bottom` as a fixed value in place of `env(safe-area-inset-bottom)` — fixed values cut off content on devices with non-zero safe areas and add unnecessary whitespace on devices without them.

## Patterns & Rules

1. **Rounded top corners only** — The sheet uses `border-radius: 1rem 1rem 0 0` applied via inline style. Bottom corners are always square because the sheet is flush with the screen edge; applying `rounded-2xl` to the whole container produces a visible gap at the bottom on some devices.
2. **Safe area on every bottom surface** — Any element that sits at the very bottom of the sheet — footer button bar, the last button in a no-header action list — must use `pb-[max(1rem,env(safe-area-inset-bottom))]`. This requires `viewport-fit=cover` in the page `<meta name="viewport">` tag; without it `env()` resolves to zero on all devices.
3. **Body scrolls; header and footer do not** — The three-zone layout (handle + header, body, footer) must be implemented with the sheet as a `flex flex-col` container, the body as `flex-1 overflow-y-auto`, and both header and footer carrying `flex-shrink-0`. If `flex-shrink-0` is omitted, tall body content can compress the footer off-screen.
4. **Slide-up animation uses transform** — Sheets should animate in with `transform: translateY(100%)` → `translateY(0)` via a CSS transition (`transition: transform 0.3s ease`). Do not animate `bottom` or `top` as they trigger layout recalculations and produce jank on low-end Android devices.
5. **Touch target baseline is 44 px** — Every row, button, and icon button inside the sheet must meet `h-11` (44 px minimum). For icon-only dismiss buttons use `h-11 w-11` with `flex items-center justify-center` to pad the tap surface without inflating the visible icon size.

## Accessibility

- The sheet root must carry `role="dialog"` and `aria-modal="true"` so screen readers restrict virtual cursor movement to the sheet and announce the overlay boundary on open.
- `aria-labelledby` must reference the header `<h2>` element's `id`; for no-header sheets that have no visible title, use `aria-label` directly on the container with a concise description of the sheet's purpose.
- Focus must move to the first interactive element inside the sheet on open (typically the first action button or the close button) and return to the triggering element on close.
- The Escape key and a swipe-down gesture must both trigger the dismiss action; ensure the JavaScript handler listens for `keydown` with `key === "Escape"` in addition to touch event handlers.
- Swipe-to-dismiss gesture handlers must expose an equivalent button-based dismiss path (`aria-label="Dismiss"` on the close button) because swipe gestures are not accessible to users navigating by switch control or keyboard.
- The drag handle bar is decorative; give it `aria-hidden="true"` so screen readers do not announce it as a meaningless empty region.

## Related Components

- [Modal / Dialog](./modal-dialog.md) — Desktop counterpart; use on breakpoints wider than `md` where a centered card with a constrained fixed width is more appropriate than a full-width bottom-anchored sheet.
- [Drawer Panel](./drawer-panel.md) — A slide-in side panel for detail views and longer forms; on mobile, prefer a full-screen page over a side drawer, but reference this component when building responsive layouts that adapt between sheet (mobile) and drawer (desktop).
- [Action Sheet](./action-sheet.md) — A specialized no-header bottom sheet containing only a grouped list of labeled actions; use when the user tapped a context menu trigger and the result is a set of choices rather than a form or confirmation.
