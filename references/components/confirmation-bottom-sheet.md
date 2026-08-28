---
component: Confirmation Bottom Sheet
category: Mobile
variants: [warning, danger, info]
related: [bottom-sheet, action-sheet, modal-dialog]
replaces: Modal / Dialog (confirmation variant)
---

# Confirmation Bottom Sheet

> Bottom-anchored confirmation overlay using the same amber/red/blue severity system as the desktop confirmation dialog.

## Overview

The Confirmation Bottom Sheet renders as a full-width white card anchored to the bottom of the viewport, sliding up from below with `rounded-t-2xl` corners and a `shadow-2xl` elevation. Unlike the desktop Modal / Dialog — which floats centered at a fixed width over a backdrop — this component expands edge-to-edge to fill the phone screen horizontally and is dismissed by swiping down or tapping the scrim above it. It carries the identical severity signaling system (amber for warning, red for danger, blue for info) but adapts the layout for one-handed thumb reach: the action buttons are full-width stacked rows in the footer, always visible above the device home indicator, and the dismiss handle bar sits at the top so users have a natural swipe target before reading the content.

## When to Use

- Asking a field technician to confirm a consequential action — such as closing a work order or releasing a part from inventory — while they are working on a mobile device.
- Presenting an irreversible destructive action warning, such as permanently deleting an attachment or removing a line item, when the user is mid-flow in the mobile app.
- Surfacing a mandatory system alert, such as a session-expiry or connectivity-loss warning, that requires an explicit tap to proceed or dismiss before the user can continue.
- Blocking a navigation transition — for example, leaving a form with unsaved changes — until the user taps a clear binary choice (discard vs. keep editing).
- Replacing any instance of the desktop confirmation dialog in mobile-breakpoint views where a centered fixed-width overlay would be too narrow to read comfortably.

## When NOT to Use

- When building for the web app desktop experience — use [Modal / Dialog (confirmation variant)](./modal-dialog.md) instead, which centers at a controlled width and allows backdrop interaction patterns that do not translate to touch.
- When the user needs to select from a list of discrete options rather than confirm a single action — use [Action Sheet](./action-sheet.md) instead, which presents a stacked list of labeled choices without a body description.
- When the content to confirm requires more than two sentences of explanation — that volume of copy belongs on a dedicated confirmation screen, not in a bottom sheet overlay.

## Variants

| Variant | Description |
|---------|-------------|
| warning | Use for consequential but recoverable actions, such as reassigning a work order or resetting a form. Renders an amber icon badge (`text-amber-500 bg-amber-100`) and an amber confirm button (`bg-amber-500`) to signal caution without implying permanent loss. |
| danger | Use for irreversible destructive actions such as deleting a record, removing a part, or permanently closing a job. Renders a red icon badge (`text-red-600 bg-red-100`) and a red confirm button (`bg-red-600`) to communicate maximum severity. |
| info | Use for system-initiated prompts that are not user errors, such as session expiry or a required app update. Renders a blue icon badge (`text-blue-600 bg-blue-100`), omits the handle bar swipe-to-dismiss affordance when the choice is mandatory, and omits the scrim tap-to-dismiss behaviour. |

## HTML Structure

```html
<!-- Confirmation Bottom Sheet — Warning variant -->
<!-- Note: env(safe-area-inset-bottom) requires viewport-fit=cover in the <meta name="viewport"> tag -->

<!-- Scrim backdrop (tap to dismiss; remove pointer events for mandatory info variant) -->
<div class="fixed inset-0 z-40 bg-black/40" aria-hidden="true"></div>

<!-- Sheet container -->
<div
  role="dialog"
  aria-modal="true"
  aria-labelledby="cbs-title"
  class="fixed bottom-0 left-0 right-0 z-50 bg-white rounded-t-2xl shadow-2xl flex flex-col"
>

  <!-- Handle bar (omit for mandatory info variant) -->
  <div class="flex justify-center pt-3 pb-1 flex-shrink-0">
    <div class="w-10 h-1 rounded-full bg-gray-300"></div>
  </div>

  <!-- Body: icon badge + title + supporting text -->
  <div class="flex flex-row items-start px-5 pt-5 pb-6 flex-shrink-0">
    <!-- Icon badge: swap color classes per variant -->
    <div class="flex items-center justify-center w-11 h-11 rounded-full text-amber-500 bg-amber-100 flex-shrink-0 mr-4">
      <i class="ti ti-alert-triangle text-current text-xl"></i>
    </div>
    <div class="flex flex-col space-y-1.5 flex-1 min-w-0">
      <div id="cbs-title" class="text-lg leading-6 font-semibold text-gray-900">Close Work Order?</div>
      <div id="cbs-desc" class="text-gray-500 text-base leading-snug">This action cannot be undone and will notify the assigned technician.</div>
    </div>
  </div>

  <!-- Footer action bar: stacked full-width buttons above safe area -->
  <div class="flex flex-col gap-3 px-5 pt-2 pb-[max(1.25rem,env(safe-area-inset-bottom))] flex-shrink-0">
    <!-- Confirm button: swap bg color per variant (bg-amber-500 / bg-red-600 / bg-blue-500) -->
    <button
      class="w-full h-11 rounded-xl text-base font-medium text-white bg-amber-500 flex items-center justify-center"
      aria-describedby="cbs-desc"
    >
      Close Work Order
    </button>
    <button
      class="w-full h-11 rounded-xl text-base font-medium text-gray-700 bg-gray-100 flex items-center justify-center"
    >
      Cancel
    </button>
  </div>

</div>

<!-- Danger variant: swap icon + button classes -->
<!--
  Icon badge:   class="... text-red-600 bg-red-100"
  Icon:         class="ti ti-trash text-current text-xl"
  Confirm btn:  class="... bg-red-600"
-->

<!-- Info variant (mandatory — no handle bar, no scrim dismiss): -->
<!--
  Scrim:        remove the click handler; pointer-events-none on the backdrop div
  Handle bar:   omit entirely
  Icon badge:   class="... text-blue-600 bg-blue-100"
  Icon:         class="ti ti-info-circle text-current text-xl"
  Confirm btn:  class="... bg-blue-500"
-->
```

## Dos & Don'ts

### Do

- Match the icon badge color and confirm button color to the action's severity: amber for warning, red for danger, blue for info. These pairs must stay coordinated — never mix a red badge with an amber button or vice versa.
- Size all tappable elements to a minimum of `h-11` (44px) so thumbs can activate them reliably; this applies to both the confirm button and the cancel button.
- Include `pb-[max(1.25rem,env(safe-area-inset-bottom))]` on the footer container so the action buttons clear the home indicator on notched devices without relying on a fixed pixel value.
- Render action buttons as full-width stacked rows (`w-full`), with the confirm action on top and the cancel below, so the most common escape path (cancel) sits closest to the thumb's natural resting position.
- Limit body copy to one or two sentences that state what will happen and what consequence the user should know about; supporting text longer than two lines will push buttons below the comfortable tap zone.

### Don't

- Do not render the Confirmation Bottom Sheet as a narrow centered card on mobile — it must be full-width `left-0 right-0` so it fills the screen edge to edge and avoids awkward side margins on small viewports.
- Do not place action buttons inside the body section rather than the footer — mixing content and actions in the same zone breaks the predictable layout that users rely on to find the cancel path quickly.
- Do not omit the handle bar (`w-10 h-1 rounded-full bg-gray-300`) from the warning and danger variants — it is the visual affordance for swipe-to-dismiss, and removing it leaves users without a gesture cue.
- Do not use `:hover`-only states to indicate the active or pressed state of buttons — mobile devices have no hover event; use active/focus states or a pressed background shift instead.
- Do not open a Confirmation Bottom Sheet on top of another open sheet — stacked blocking overlays disorient mobile users and make the back navigation path unpredictable.

## Patterns & Rules

1. **Full-width, bottom-anchored positioning** — The sheet always uses `fixed bottom-0 left-0 right-0` with `rounded-t-2xl` corners and no side margins. Never apply a max-width constraint or center it horizontally; the full-width presentation is load-bearing for legibility on small viewports.
2. **Severity signaling is inherited from desktop** — The icon badge + confirm button color pair follows the same rules as the desktop confirmation dialog: `text-amber-500 bg-amber-100` / `bg-amber-500` for warning, `text-red-600 bg-red-100` / `bg-red-600` for danger, `text-blue-600 bg-blue-100` / `bg-blue-500` for info. Colors from different severity levels must never be mixed.
3. **Mandatory vs. dismissible** — For the info variant when the choice is truly mandatory (e.g. session expiry), remove the handle bar and disable tap-to-dismiss on the scrim backdrop. For warning and danger variants, always include the handle bar and enable scrim tap-to-dismiss so users have multiple escape paths.
4. **Safe area footer padding** — The footer container must use `pb-[max(1.25rem,env(safe-area-inset-bottom))]` — not a fixed pixel value — so the action buttons sit comfortably above the home indicator on iPhone models with a sensor notch and flush to the bottom on devices without one.
5. **Stacked button order** — The confirm action renders first (closer to screen center) and the cancel action renders second (closer to the bottom edge near the thumb). This order ensures cancel is within easy reach without requiring a deliberate upward stretch, which reduces accidental confirmations.

## Accessibility

- The sheet root must carry `role="dialog"` and `aria-modal="true"` so screen readers restrict virtual cursor movement to the overlay and announce it as a blocking region.
- `aria-labelledby` must reference the title element's `id` (e.g. `id="cbs-title"`) so VoiceOver and TalkBack announce the sheet's purpose immediately when it receives focus.
- The confirm button for danger and warning variants must carry `aria-describedby` pointing to the supporting-text element's `id` (e.g. `id="cbs-desc"`) so screen reader users hear the consequence before activating the action.
- Focus must move to the confirm button (or the first interactive element) when the sheet opens, and return to the trigger element when the sheet closes. For mandatory info variants, focus must not be allowed outside the sheet until one of the two actions is tapped.
- Swipe-to-dismiss via the handle bar must have a keyboard and assistive-technology equivalent: pressing Escape or activating a visually hidden "Dismiss" button must trigger the same cancel action that a downward swipe performs.
- The cancel button must be a native `<button>` element, not a styled `<div>`, so it is reachable by keyboard and fires on both tap and Enter/Space without additional event handling.

## Related Components

- [Modal / Dialog (confirmation variant)](./modal-dialog.md) — Desktop counterpart; use for web app views where a centered, fixed-width overlay is appropriate and hover-state interactions are available.
- [Action Sheet](./action-sheet.md) — A bottom-anchored sheet for presenting a list of labeled discrete choices; use it when the user is selecting one of several options rather than confirming or cancelling a single action.
- [Bottom Sheet](./bottom-sheet.md) — The generic bottom-anchored container pattern that the Confirmation Bottom Sheet is built on; use the base Bottom Sheet when the content inside is not a confirmation flow.
