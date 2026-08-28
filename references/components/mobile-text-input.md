---
component: Mobile Text Input
category: Mobile
variants: [default, with-label, error, disabled, with-icon]
related: [mobile-search-bar, form-layout, text-input]
replaces: Text Input
---

# Mobile Text Input

> Full-width 48px-height input field; prevents iOS auto-zoom and ensures 44px+ touch targets.

## Overview

The Mobile Text Input is a full-width, `h-12` (48px) rounded field with a visible border and a white background, built specifically for touch interfaces. Unlike its desktop counterpart, it uses `text-[16px]` to prevent iOS Safari from triggering unwanted viewport zoom on focus, and its larger tap area satisfies the 44px minimum touch target requirement. It sits flush within a mobile form layout, stretching the full container width, and surfaces state changes — focus, error, disabled — through border-color shifts only, consistent with the Zuper design system's approach to state communication.

## When to Use

- Collecting short freeform text (name, email, phone, address) inside a mobile form or bottom sheet where the user is interacting with a touch device.
- Accepting a single-line search or filter value in a mobile list view when the full [Mobile Search Bar](./mobile-search-bar.md) component is too wide or contextually heavy.
- Providing an inline editable field for quick record updates inside a mobile card, where tapping to edit is the primary interaction pattern.
- Entering reference codes, labels, or titles on mobile screens where constrained column widths cannot accommodate the desktop grid layout.
- Capturing user input when a native keyboard will be invoked and the field must remain visible above the on-screen keyboard.

## When NOT to Use

- When building for desktop or wide-viewport web — use [Text Input](./text-input.md) instead, which uses `h-9` and a desktop-appropriate font size.
- When the user must choose from a predefined set of values — use [Select Dropdown](./select-dropdown.md) instead; do not use a free-text input and validate on submit.
- When the input spans multiple lines or accepts long-form content — use a `<textarea>` with `min-h-[96px]` and `resize-none` instead; the `h-12` fixed height will clip overflow.

## Variants

| Variant | Description |
|---------|-------------|
| default | Bare `h-12` input with placeholder text and `border-border`; use for any field without a value or active validation error. |
| with-label | Input preceded by a `<label>` element inside a `flex flex-col gap-2` wrapper; use for every named form field so the label is always visible above the keyboard. |
| error | Border shifts to `border-red-500`; a `text-sm text-red-500` message renders below the field; use immediately after failed submit or on-blur validation. |
| disabled | Background becomes `bg-[#F5F5F5]` and cursor becomes `cursor-not-allowed`; use when the field is contextually unavailable, such as a sub-field locked until a parent field is filled. |
| with-icon | A leading icon sits at `left-4` inside a `relative` wrapper; the input gains `pl-11` to clear it; use for fields with a strongly associated symbol (e.g., a phone icon for a phone number field). |

## HTML Structure

```html
<!-- Note: viewport meta must include viewport-fit=cover for safe-area-inset values to work -->
<!-- <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"> -->

<!-- default (rest state) -->
<input
  type="text"
  placeholder="Placeholder"
  class="h-12 w-full rounded-xl border border-border bg-white px-4 text-[16px] text-gray-700 placeholder-gray-400 focus:border-gray-400 focus:outline-none"
>

<!-- focus state -->
<input
  type="text"
  value="Focused value"
  class="h-12 w-full rounded-xl border border-gray-400 bg-white px-4 text-[16px] text-gray-700 outline-none"
>

<!-- with-label (inside a form field wrapper) -->
<div class="flex flex-col gap-2">
  <label class="text-sm font-medium text-gray-700">
    Full Name <span class="text-red-500">*</span>
  </label>
  <input
    id="full-name"
    type="text"
    placeholder="John Doe"
    aria-required="true"
    class="h-12 w-full rounded-xl border border-border bg-white px-4 text-[16px] text-gray-700 placeholder-gray-400 focus:border-gray-400 focus:outline-none"
  >
</div>

<!-- error -->
<div class="flex flex-col gap-2">
  <label class="text-sm font-medium text-gray-700">
    Email <span class="text-red-500">*</span>
  </label>
  <input
    id="email"
    type="email"
    value="bad-email"
    aria-required="true"
    aria-describedby="email-error"
    aria-invalid="true"
    class="h-12 w-full rounded-xl border border-red-500 bg-white px-4 text-[16px] text-gray-700 outline-none"
  >
  <div id="email-error" class="text-sm text-red-500">Invalid email address</div>
</div>

<!-- disabled -->
<input
  type="text"
  value="Unavailable"
  disabled
  aria-disabled="true"
  class="h-12 w-full rounded-xl border border-border bg-[#F5F5F5] px-4 text-[16px] text-gray-400 cursor-not-allowed"
>

<!-- with-icon (e.g. phone field) -->
<div class="relative flex items-center">
  <span class="pointer-events-none absolute left-4 flex h-5 w-5 items-center justify-center text-gray-400">
    <!-- icon SVG or icon component here -->
  </span>
  <input
    type="tel"
    placeholder="+1 (555) 000-0000"
    class="h-12 w-full rounded-xl border border-border bg-white pl-11 pr-4 text-[16px] text-gray-700 placeholder-gray-400 focus:border-gray-400 focus:outline-none"
  >
</div>

<!-- inside a bottom sheet footer (demonstrates safe-area usage) -->
<div class="fixed bottom-0 left-0 right-0 z-50 bg-white rounded-t-2xl shadow-2xl">
  <!-- drag handle -->
  <div class="mx-auto mt-3 h-1 w-10 rounded-full bg-gray-200"></div>
  <!-- sheet body -->
  <div class="px-4 pt-4 pb-[max(1.5rem,env(safe-area-inset-bottom))]">
    <div class="flex flex-col gap-2">
      <label class="text-sm font-medium text-gray-700">Notes</label>
      <input
        type="text"
        placeholder="Add a note…"
        class="h-12 w-full rounded-xl border border-border bg-white px-4 text-[16px] text-gray-700 placeholder-gray-400 focus:border-gray-400 focus:outline-none"
      >
    </div>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Always set `text-[16px]` (or `text-base` if your Tailwind config maps `base` to 16px) — iOS Safari zooms the viewport on focus whenever the input font size is below 16px, which disrupts the layout.
- Use `h-12` (48px) for every mobile input so the touch target exceeds Apple's and Google's 44px minimum; never shrink to the desktop `h-9`.
- Wrap labeled fields in `flex flex-col gap-2` so the label, input, and any error message stack with consistent spacing without per-element margin overrides.
- When placing an input inside a bottom sheet or any fixed-position bottom container, apply `pb-[max(1rem,env(safe-area-inset-bottom))]` to the bottom container's footer so content is not clipped by the iPhone home indicator.
- Use `rounded-xl` on mobile inputs — the slightly larger radius matches mobile OS conventions and distinguishes mobile forms from the desktop `rounded-lg` fields at a glance.
- Show error messages immediately after the field that failed, using `aria-describedby` linking the input to its `<div id="...">` error text, so screen readers and VoiceOver announce the error on focus.

### Don't

- Do not use `text-sm` or any size below `text-[16px]` on mobile inputs — even if the design calls for compact forms, sub-16px font sizes cause iOS viewport zoom that breaks the user experience.
- Do not rely on `:hover` states to reveal the focused or active state of a mobile input — hover is unreliable on touch devices; use `:focus` and border-color changes only.
- Do not set a fixed pixel `width` on the input — always use `w-full` and let the parent container or padding govern horizontal size; mobile viewports vary too much for fixed widths.
- Do not place a mobile input inside a container that does not account for the soft keyboard height — always test that the focused input scrolls into view above the keyboard, particularly inside bottom sheets.
- Do not simulate a disabled state with `opacity-50` alone — use `bg-[#F5F5F5]`, `cursor-not-allowed`, and the `disabled` attribute together so both the visual appearance and the interaction are consistently non-functional.

## Patterns & Rules

1. **Font size locks the viewport** — Set `text-[16px]` explicitly rather than relying on a Tailwind preset. iOS Safari uses 16px as the threshold below which it auto-zooms on focus; this is the single most common mobile input bug in production.
2. **Touch target is always 48px** — The `h-12` class is mandatory on mobile. Padding alone cannot substitute — the element itself must be at least 44px tall so the tappable region is guaranteed regardless of surrounding layout.
3. **State is communicated through border color only** — `border-border` (rest), `border-gray-400` (focus), `border-red-500` (error), `border-border` with `bg-[#F5F5F5]` (disabled). Do not introduce box shadows, background-color shifts on focus, or ring utilities to signal state; they conflict with mobile OS focus rendering.
4. **Bottom-anchored forms require safe-area padding** — Any input rendered inside a `fixed bottom-0` container (bottom sheet, sticky footer) must have its bottom padding set with `pb-[max(1rem,env(safe-area-inset-bottom))]` so the field is not occluded by the iPhone home indicator on notched devices.
5. **Error messages belong to the input via ARIA** — Link every error `<div>` to its input with a matching `id`/`aria-describedby` pair, and set `aria-invalid="true"` on the input when the error is active. Do not rely solely on color or placement to communicate the error.

## Accessibility

- Associate every visible `<label>` with its `<input>` via a matching `for`/`id` pair; do not rely on proximity or wrapping alone, since some screen readers on mobile require the explicit association.
- Set `aria-required="true"` on inputs that must be filled, in addition to the visual `<span class="text-red-500">*</span>` asterisk in the label; VoiceOver and TalkBack announce required state from the ARIA attribute, not from the asterisk character.
- Set `aria-invalid="true"` and `aria-describedby="[error-id]"` on the `<input>` when an error is active, so VoiceOver reads the error message immediately after the field label when the user moves focus to the field.
- Use the correct `type` attribute for the expected input (`type="email"`, `type="tel"`, `type="number"`) — on mobile this controls which keyboard variant the OS surfaces, reducing user error before any validation runs.
- Users navigate between fields with the keyboard's **Next** and **Previous** controls on both iOS and Android; ensure no field is removed from the tab order unless it carries the `disabled` attribute.
- All interactive elements within or adjacent to the input (clear buttons, icon triggers) must also be at least `h-11` (44px) tall with sufficient padding so their own touch targets meet the minimum.

## Related Components

- [Text Input](./text-input.md) — Desktop counterpart with `h-9` and `text-base`; use when building for web app desktop viewports instead of this component.
- [Mobile Search Bar](./mobile-search-bar.md) — Combines a text input with a cancel action and optional filter chip row; use when the field's purpose is filtering or searching a list rather than collecting form data.
- [Form Layout](./form-layout.md) — Provides the column grid and section spacing that wraps Mobile Text Input fields inside longer mobile forms.
