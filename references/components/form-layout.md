---
component: Form Layout
category: Form & Layout
variants: [single-column, two-column, inline]
related: [text-input, select-dropdown, checkbox-and-toggle]
---

# Form Layout

> A grid-based container that arranges labeled input fields into responsive columns, eliminating the need for ad-hoc spacing decisions on every form.

## Overview

Form Layout uses a CSS grid with `gap-4` gutters and either `grid-cols-4` or `grid-cols-3` columns depending on the available panel width. Each field cell stacks a `<label>` above an `<input>` using `flex flex-col gap-1`, with an optional helper or error line rendered in `text-sm` below the control. The component is the primary structural layer for all data-entry surfaces in the Zuper design system, ensuring consistent rhythm across create, edit, and filter forms.

## When to Use

- Collecting multiple structured fields on a create or edit form (e.g., customer profile, job details, asset registration).
- Laying out address blocks where City, State, and ZIP belong on the same visual row.
- Embedding a form inside a side panel or drawer where the available width dictates the appropriate column count.
- Displaying inline validation errors alongside their originating field without disrupting the surrounding layout.
- Grouping related fields (e.g., contact info vs. address) by placing each group in its own `grid` container within the same section.

## When NOT to Use

- Displaying a single isolated field inline with other UI controls — use [Text Input](./text-input.md) standalone instead.
- Building a settings toggle row where the label sits beside a switch — use [Checkbox and Toggle](./checkbox-and-toggle.md) instead.
- Presenting a filterable list of options inside a pop-over — use [Select Dropdown](./select-dropdown.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| single-column | One field per row; use for very narrow panels or when each field requires substantial vertical space such as a textarea. |
| two-column | `grid-cols-2`; use for moderate-width panels where a four-column grid would produce inputs that are too narrow to read comfortably. |
| inline | `grid-cols-3` (narrow panel, `<50%` viewport width); use when the host panel occupies less than half the screen width to prevent field truncation. |

## HTML Structure

```html
<!-- Wide panel (>50% width) — 4 columns -->
<div class="grid grid-cols-4 gap-4">

  <!-- Required field -->
  <div class="flex flex-col gap-1">
    <label class="text-base text-gray-600">
      Full Name <span class="text-red-500">*</span>
    </label>
    <input
      type="text"
      placeholder="John Doe"
      class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 placeholder-gray-400 focus:outline-none"
    >
  </div>

  <!-- Field with validation error -->
  <div class="flex flex-col gap-1">
    <label class="text-base text-gray-600">
      Email <span class="text-red-500">*</span>
    </label>
    <input
      type="text"
      value="bad-email"
      class="h-9 w-full rounded-lg border border-red-500 bg-white px-2 text-base text-gray-600 focus:outline-none"
    >
    <div class="text-sm text-red-500">Invalid email address</div>
  </div>

  <!-- Optional field with helper text -->
  <div class="flex flex-col gap-1">
    <label class="text-base text-gray-600">Address</label>
    <input
      type="text"
      placeholder="Street address"
      class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 placeholder-gray-400 focus:outline-none"
    >
    <div class="text-sm text-gray-500">Enter your full street address</div>
  </div>

</div>

<!-- Narrow panel (<50% width) — 3 columns -->
<div class="grid grid-cols-3 gap-4">

  <div class="flex flex-col gap-1">
    <label class="text-base text-gray-600">
      Full Name <span class="text-red-500">*</span>
    </label>
    <input
      type="text"
      placeholder="John Doe"
      class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 placeholder-gray-400 focus:outline-none"
    >
  </div>

  <!-- Repeat field cells as needed -->

</div>
```

## Dos & Don'ts

### ✅ Do

- Choose `grid-cols-4` when the form panel occupies more than 50% of the viewport width so inputs have enough room to display values without truncation.
- Choose `grid-cols-3` when the panel is narrow (side panel, drawer) to maintain a minimum comfortable input width.
- Apply `border-red-500` to the input and render a `text-sm text-red-500` error line immediately below the control when validation fails.
- Use `text-red-500 *` span inside the label for required fields so the asterisk inherits the correct color token without custom CSS.
- Keep helper text (`text-sm text-gray-500`) to one line to avoid increasing row height inconsistently across the grid.

### ❌ Don't

- Do not mix `grid-cols-4` and `grid-cols-3` sections inside the same visual group — it produces misaligned column gutters that feel broken.
- Do not place a `<textarea>` or tall control inside a multi-column grid without spanning it across all columns — mismatched row heights break the grid rhythm.
- Do not omit the `gap-4` class — removing it collapses inputs together and makes labels and controls visually merge.
- Do not use inline `style="width:…"` to size individual inputs — all inputs should span the full cell width via `w-full` so the grid controls layout.
- Do not show a tooltip instead of an inline error line for validation messages — users on mobile cannot hover, and inline errors meet WCAG 1.3.1.

## Patterns & Rules

1. **Column count by panel width** — Use `grid-cols-4` for panels wider than 50% of the viewport and `grid-cols-3` for narrower panels; never use fewer than three columns inside a dedicated form section unless the panel is a modal narrower than 400 px.
2. **Field cell structure** — Every field cell must follow the `flex flex-col gap-1` pattern (label → input → optional sub-line); deviating from this order breaks the vertical rhythm established by the grid rows.
3. **Required field marking** — Mark required fields with a `<span class="text-red-500">*</span>` appended inside the `<label>`, never as placeholder text, so the requirement is visible before the user interacts with the field.
4. **Validation state on the input** — When a field is invalid, swap `border-border` for `border-red-500` on the input element and append a `text-sm text-red-500` error message as a sibling div; do not use a separate overlay or tooltip.
5. **Helper text placement** — Helper text uses `text-sm text-gray-500` and sits below the input as a sibling div, sharing the same `flex flex-col gap-1` cell; it should be hidden when an error message is active to avoid two sub-lines competing for the same space.

## Accessibility

- Each `<input>` must be programmatically associated with its `<label>` via a matching `for`/`id` pair or by nesting the input inside the label element.
- When an error message is visible, the input must carry `aria-invalid="true"` and `aria-describedby` pointing to the error div's `id` so screen readers announce the message on focus.
- Tab order follows DOM order, which the grid preserves naturally; do not use `tabindex` values other than `0` or `-1` to avoid creating an unexpected focus sequence.
- Required fields must also set `aria-required="true"` on the input in addition to the visual asterisk, as screen readers do not read CSS-generated content.

## Related Components

- [Text Input](./text-input.md) — The individual input control placed inside each Form Layout cell; it defines the border, height (`h-9`), and focus styles used throughout the grid.
- [Select Dropdown](./select-dropdown.md) — A drop-down control that can occupy any Form Layout cell in place of a text input when the field value must come from a predefined list.
- [Checkbox and Toggle](./checkbox-and-toggle.md) — Boolean controls that can be embedded inside a Form Layout cell but require adjusted cell height to align their touch targets with adjacent text inputs.
