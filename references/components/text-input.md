---
component: Text Input
category: Interactive
variants: [default, with-label, with-error, disabled]
related: [select-dropdown, form-layout]
---

# Text Input

> A single-line text field that lets users enter freeform text values in forms and search interfaces.

## Overview

The Text Input is a fixed-height (`h-9`) rounded field with a light border and a neutral background, designed to sit consistently inside the Zuper form grid. It covers the full range of interactive states — rest, focus, error, and disabled — through border-color changes rather than shadow or fill shifts. Its primary role is collecting short, freeform user input such as names, addresses, phone numbers, and search queries.

## When to Use

- Collecting short freeform text such as a name, email, phone number, or address in a form.
- Capturing a single-line search or filter query in a list or table header.
- Accepting user-defined labels, titles, or reference codes that cannot be constrained to a fixed option set.
- Providing an inline editable field for quick in-context record updates.

## When NOT to Use

- When the user must pick from a predefined set of values — use [Select Dropdown](./select-dropdown.md) instead.
- When the value is a boolean on/off preference — use the Toggle Switch within [Checkbox & Toggle](./checkbox-toggle.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| default | Bare input with placeholder text; use for any field that does not yet have a value and has no validation errors. |
| with-label | Input preceded by a `<label>` element inside a `flex flex-col gap-1` wrapper; use for every named form field in a Form Layout grid. |
| with-error | Border changes to `border-red-500` and a `text-sm text-red-500` message appears below the field; use immediately after failed validation to explain the problem. |
| disabled | Background becomes `bg-[#F5F5F5]` and the cursor becomes `cursor-not-allowed`; use when the field value cannot be edited in the current application state. |

## HTML Structure

```html
<!-- default (rest state) -->
<input
  type="text"
  placeholder="Placeholder"
  class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 placeholder-gray-400 focus:border-gray-400 focus:outline-none"
>

<!-- focus state -->
<input
  type="text"
  value="Focused value"
  class="h-9 w-full rounded-lg border border-gray-400 bg-white px-2 text-base text-gray-600 outline-none"
>

<!-- with-label (inside a form field wrapper) -->
<div class="flex flex-col gap-1">
  <label class="text-base text-gray-600">Full Name <span class="text-red-500">*</span></label>
  <input
    type="text"
    placeholder="John Doe"
    class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 placeholder-gray-400 focus:outline-none"
  >
</div>

<!-- with-error -->
<div class="flex flex-col gap-1">
  <label class="text-base text-gray-600">Email <span class="text-red-500">*</span></label>
  <input
    type="text"
    value="bad-email"
    class="h-9 w-full rounded-lg border border-red-500 bg-white px-2 text-base text-gray-600 outline-none"
  >
  <div class="text-sm text-red-500">Invalid email address</div>
</div>

<!-- disabled -->
<input
  type="text"
  value="Disabled"
  disabled
  class="h-9 w-full rounded-lg border border-border bg-[#F5F5F5] px-2 text-base text-gray-600 cursor-not-allowed"
>
```

## Dos & Don'ts

### Do

- Always wrap a labeled field in `flex flex-col gap-1` to maintain consistent spacing between the label, input, and any helper or error text.
- Use `text-red-500` and `border-red-500` together for the error variant so both the border and message are visually consistent.
- Place required-field asterisks inside a `<span class="text-red-500">*</span>` immediately after the label text.
- Use `placeholder-gray-400` for placeholder text so it is clearly distinguishable from actual user input.
- Use `w-full` on the input so it fills its grid column and responds to the parent layout.

### Don't

- Do not omit `focus:outline-none` — leaving the browser default outline creates a double-border appearance that breaks the design system's focus style.
- Do not apply the error border class (`border-red-500`) before the user has attempted to submit or leave the field — premature errors increase cognitive load.
- Do not use the Text Input for multi-line content — it has a fixed `h-9` height and will clip text; use a `<textarea>` or the appropriate rich-text component instead.
- Do not hard-code a pixel `width` on the input element — always size via the parent grid column (`w-full`) to preserve responsive layout.
- Do not place hint or helper text inside the `placeholder` attribute alone; add a visible `text-sm text-gray-500` element below the input so screen readers and filled states can still surface the guidance.

## Patterns & Rules

1. **Border communicates state** — The border color is the sole visual indicator that changes across states: `border-border` (rest), `border-gray-400` (focus), `border-red-500` (error), and `border-border` with `bg-[#F5F5F5]` (disabled). Do not use background fills or box shadows to signal state.
2. **Form Layout grid determines column span** — Text Inputs do not have intrinsic widths; they inherit width from the Form Layout grid (`grid-cols-4` for wide panels, `grid-cols-3` for narrow panels). Always use `w-full` and let the parent grid column govern horizontal size.
3. **Error message placement** — The `text-sm text-red-500` error message sits directly below the input with no extra margin wrapper; the `gap-1` on the `flex flex-col` parent provides all necessary spacing.
4. **Required field marking** — Mark required fields with `<span class="text-red-500">*</span>` in the label, not in the placeholder, so the requirement is visible even after the user types a value.
5. **Disabled vs read-only** — Use the `disabled` attribute (with `bg-[#F5F5F5]` and `cursor-not-allowed`) when the field must be non-interactive. Do not simulate a disabled appearance using opacity alone, as it reduces the contrast needed to communicate the state.

## Accessibility

- Associate every visible label with its input using a matching `for`/`id` pair or by nesting the input inside the `<label>` element, so screen readers announce the field name on focus.
- Users navigate between fields with **Tab** and move focus away with **Shift+Tab**; ensure the component is never removed from the tab order unless it is in the `disabled` state.
- The error message `<div class="text-sm text-red-500">` must be linked to the input via `aria-describedby` so assistive technology reads the error alongside the field label on focus.
- Mark required fields with `aria-required="true"` on the `<input>` in addition to the visual asterisk, so the requirement is announced to users who cannot see color.

## Related Components

- [Select Dropdown](./select-dropdown.md) — Use when the user must choose from a fixed list of options rather than type freeform text.
- [Form Layout](./form-layout.md) — Provides the grid wrapper (`grid-cols-4` / `grid-cols-3`) that determines column width and spacing for Text Input fields inside a form.
