---
component: Mobile Button
category: Mobile
variants: [primary, secondary, destructive, disabled]
related: [mobile-card, mobile-text-input, button]
replaces: Button
---

# Mobile Button

> Full-width 44px-height button optimized for touch; adapts the desktop button for mobile contexts.

## Overview

The Mobile Button is a full-width, touch-optimized action control rendered at `h-11` (44px) with `rounded-xl` corners and `text-base` type weight. Unlike the desktop Standard Button — which sizes itself to its content and appears inline within toolbars or beside other controls — the Mobile Button spans the available container width and is typically anchored to the bottom of the screen in a safe-area-aware footer strip. It carries the same four semantic weights (primary, secondary, destructive, disabled) as the desktop Button but removes hover-state-only affordances entirely, relying instead on active-press feedback and sufficient contrast to communicate interactivity at touch scale.

## When to Use

- Confirming a primary action at the end of a mobile form or wizard step, such as "Create Job" or "Save Changes", where the button anchors to the bottom of the view inside a `pb-[max(1rem,env(safe-area-inset-bottom))]` footer.
- Presenting a destructive confirmation — "Delete", "Remove", "Discard" — in a mobile action sheet or bottom sheet where the action requires an unambiguous, easily reachable tap target.
- Offering a paired primary + secondary action row (e.g. "Confirm" and "Cancel") stacked vertically or placed side-by-side in a bottom strip, giving equal physical reach to both actions.
- Triggering navigation-advancing actions from a mobile card's footer strip, such as "View Details" or "Start", where inline text links would produce undersized tap targets.
- Acting as the sole call-to-action on a mobile empty state or onboarding screen where a ghost/text button would not have enough visual presence.

## When NOT to Use

- When building for the desktop web app — use [Button](./button.md) instead; the full-width layout and fixed bottom positioning disrupt desktop layouts designed for inline controls.
- When the action is purely icon-based with no visible label — the touch target is already constrained; use a dedicated icon button with an explicit `aria-label` and at minimum a `w-11 h-11` bounding box instead.
- When the set of actions is more than two and displayed simultaneously — use a mobile action sheet (an overlay list of options) rather than stacking three or more full-width buttons, which collapses vertical space and overwhelms the user.

## Variants

| Variant | Description |
|---------|-------------|
| primary | Filled `bg-primary text-white` button for the single most important action in a view; use at most once per bottom strip. |
| secondary | Bordered `border border-border text-gray-700 bg-white` button for cancel, back, or supporting actions placed alongside a primary. |
| destructive | Filled `bg-red-600 text-white` button reserved for irreversible actions such as delete or discard; always paired with an explicit confirmation label ("Delete Job", not "OK"). |
| disabled | Visual-only opacity reduction (`opacity-50 cursor-not-allowed`) combined with the native `disabled` attribute; preserves layout so the strip does not reflow when the state changes. |

## HTML Structure

```html
<!-- Note: env(safe-area-inset-bottom) requires viewport-fit=cover in the meta viewport tag -->
<!-- <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> -->

<!-- Primary Button -->
<button class="w-full h-11 rounded-xl bg-primary text-white text-base font-medium flex items-center justify-center gap-2 active:opacity-80 transition-opacity">
  <i class="ti ti-plus text-lg"></i>
  <span>Create Job</span>
</button>

<!-- Secondary Button -->
<button class="w-full h-11 rounded-xl border border-border bg-white text-gray-700 text-base font-medium flex items-center justify-center gap-2 active:bg-gray-50 transition-colors">
  <i class="ti ti-x text-lg"></i>
  <span>Cancel</span>
</button>

<!-- Destructive Button -->
<button class="w-full h-11 rounded-xl bg-red-600 text-white text-base font-medium flex items-center justify-center gap-2 active:opacity-80 transition-opacity">
  <i class="ti ti-trash text-lg"></i>
  <span>Delete Job</span>
</button>

<!-- Disabled Button (Primary) -->
<button class="w-full h-11 rounded-xl bg-primary text-white text-base font-medium flex items-center justify-center gap-2 opacity-50 cursor-not-allowed" disabled>
  <i class="ti ti-plus text-lg"></i>
  <span>Create Job</span>
</button>

<!-- Loading State (Primary) -->
<button class="w-full h-11 rounded-xl bg-primary text-white text-base font-medium flex items-center justify-center gap-2 opacity-80 cursor-not-allowed" disabled>
  <i class="ti ti-loader-2 animate-spin text-lg"></i>
  <span>Saving…</span>
</button>

<!-- Bottom-anchored footer strip — single primary action -->
<div class="fixed bottom-0 left-0 right-0 z-50 bg-white border-t border-border px-4 pt-3 pb-[max(1rem,env(safe-area-inset-bottom))]">
  <button class="w-full h-11 rounded-xl bg-primary text-white text-base font-medium flex items-center justify-center gap-2 active:opacity-80 transition-opacity">
    <i class="ti ti-check text-lg"></i>
    <span>Confirm</span>
  </button>
</div>

<!-- Bottom-anchored footer strip — primary + secondary side-by-side -->
<div class="fixed bottom-0 left-0 right-0 z-50 bg-white border-t border-border px-4 pt-3 pb-[max(1rem,env(safe-area-inset-bottom))] flex gap-3">
  <button class="flex-1 h-11 rounded-xl border border-border bg-white text-gray-700 text-base font-medium flex items-center justify-center gap-2 active:bg-gray-50 transition-colors">
    <span>Cancel</span>
  </button>
  <button class="flex-1 h-11 rounded-xl bg-primary text-white text-base font-medium flex items-center justify-center gap-2 active:opacity-80 transition-opacity">
    <span>Save</span>
  </button>
</div>

<!-- Action sheet button row (inside a bottom sheet overlay) -->
<div class="px-4 pb-[max(1rem,env(safe-area-inset-bottom))] flex flex-col gap-3">
  <button class="w-full h-11 rounded-xl bg-red-600 text-white text-base font-medium flex items-center justify-center gap-2 active:opacity-80 transition-opacity">
    <i class="ti ti-trash text-lg"></i>
    <span>Delete Job</span>
  </button>
  <button class="w-full h-11 rounded-xl border border-border bg-white text-gray-700 text-base font-medium flex items-center justify-center gap-2 active:bg-gray-50 transition-colors">
    <span>Cancel</span>
  </button>
</div>
```

## Dos & Don'ts

### Do

- Set `w-full` on every Mobile Button so it always spans its container; mobile layouts are column-based and a content-sized button creates an inconsistently sized tap target.
- Include `pb-[max(1rem,env(safe-area-inset-bottom))]` on every bottom-anchored strip so the button clears the home indicator on notched devices without leaving excessive padding on flat-screen devices.
- Use `active:opacity-80` or `active:bg-gray-50` (for secondary) as the press feedback mechanism — it fires reliably on touch devices, unlike `:hover` which fires only after a long-press or mouse event.
- Apply both the CSS `opacity-50 cursor-not-allowed` class and the native `disabled` attribute when disabling a button, so the element is removed from the tab order and announced correctly by screen readers.
- Keep button labels to two or three words maximum ("Save Changes", "Delete Job") so the text fits comfortably at `text-base` across the smallest supported viewport width (320px).

### Don't

- Do not use `:hover`-only styles to signal interactivity — hover events on touch screens fire inconsistently and can leave the button stuck in a highlighted state after a tap.
- Do not place more than two Mobile Buttons side-by-side in a strip; a three-button row on a 320px viewport produces tap targets below 44px wide, violating WCAG 2.5.5 Target Size.
- Do not stack more than three full-width buttons vertically in a single view — if the action set is larger, move options into a mobile action sheet or bottom sheet list instead.
- Do not omit the `fixed bottom-0 left-0 right-0` wrapper when anchoring a button to the bottom of the screen; using `absolute` positioning causes the button to scroll out of view on long-form pages.
- Do not rely on colour alone to distinguish the destructive variant from the primary variant — always include a label that names the irreversible consequence ("Delete", "Discard"), not a generic confirmation word like "Yes" or "OK".

## Patterns & Rules

1. **Safe area ownership** — The `pb-[max(1rem,env(safe-area-inset-bottom))]` padding belongs on the wrapper `div`, not on the `<button>` itself, so the button's visual height stays consistent at `h-11` and the safe area becomes whitespace below it.
2. **Primary action is always right or bottom** — In a side-by-side strip, the primary button sits on the right (`flex-row` with primary as the second child); in a stacked strip, the primary sits at the top so it is immediately reachable without scrolling past the secondary.
3. **Loading state keeps the button mounted** — Replace the action icon with `ti-loader-2 animate-spin` and add `disabled` for the duration of the async operation; do not remove or hide the button, as the layout shift disorients the user and can cause accidental taps on newly revealed content below.
4. **Destructive actions require explicit labels** — Never use a destructive variant button with a label like "OK", "Confirm", or "Yes". The label must name the action ("Delete Job", "Remove Member") so the consequence is unambiguous without reading surrounding copy.
5. **Content clearance** — The bottom strip occupies approximately `calc(44px + 1rem + env(safe-area-inset-bottom))` of fixed vertical space. The scrollable content area below it must have a matching `pb` value so the last item in the list is not occluded by the anchored strip.

## Accessibility

- Use a native `<button>` element so the browser assigns `role="button"` automatically and handles `Enter` and `Space` key activation without additional scripting.
- Minimum touch target size is `h-11` (44px height) with `w-full`; never reduce height below this threshold, even on layout-constrained screens.
- Apply both `disabled` (HTML attribute) and the visual disabled class together. If the button must remain focusable to surface a tooltip explaining why the action is unavailable, use `aria-disabled="true"` with `pointer-events-none` in place of the native `disabled` attribute.
- When displaying a loading state, update the button's accessible label with `aria-label="Saving, please wait"` or use a visually hidden `<span class="sr-only">` so screen readers announce the changed state rather than re-reading the now-hidden action label.
- Ensure the bottom strip's `z-50` stacking does not trap focus — after the strip renders, the focus order should still move naturally from the last interactive element in the scroll area down into the strip buttons, not skip past them.

## Related Components

- [Button](./button.md) — Desktop counterpart; use for all non-mobile web contexts where inline sizing, toolbar placement, and hover states are appropriate.
- [Mobile Card](./mobile-card.md) — Mobile card component whose footer strip commonly hosts Mobile Buttons as inline action controls.
- [Mobile Text Input](./mobile-text-input.md) — Mobile form field component that pairs with Mobile Button in form layouts anchored to the bottom of the screen.
