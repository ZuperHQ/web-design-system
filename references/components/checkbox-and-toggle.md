---
component: Checkbox & Toggle
category: Interactive
variants: [checkbox, toggle-switch]
related: [form-layout, toggle-and-segment]
---

# Checkbox & Toggle

> Binary selection controls that let users choose one or more options (checkbox) or instantly switch a setting on or off (toggle switch) without requiring a form submission.

## Overview

The Checkbox & Toggle component provides two distinct binary input controls housed in the same section of the design system. Checkboxes render as a native `<input type="checkbox">` with an inline label and support unchecked, checked, and disabled states. Toggle switches render as a styled `<button>` with a sliding pill indicator, using background color (`bg-gray-200` off, `bg-gray-700` on) and horizontal translation to communicate state visually.

## When to Use

- Use a **checkbox** when the user must explicitly commit multiple independent selections before an action is performed (e.g., picking items in a list or agreeing to terms).
- Use a **checkbox** for bulk-select patterns in data tables where rows must be individually or collectively marked.
- Use a **toggle switch** when a single setting takes effect immediately without a save action, such as enabling notifications or activating a feature flag.
- Use a **toggle switch** when the binary state maps naturally to on/off, active/inactive, or enabled/disabled language.
- Use the **disabled** state on either variant when the option exists but cannot be changed due to permissions or system state.

## When NOT to Use

- Do not use a checkbox to represent a single immediate action — use [Toggle & Segment](./toggle-and-segment.md) instead, which is purpose-built for instant activation controls with segmented context.
- Do not use a toggle switch inside a form that requires explicit submission — use [Form Layout](./form-layout.md) with checkboxes so users can review and confirm all selections together.
- Do not use either variant when the user must select exactly one option from a mutually exclusive set — use a radio group within [Form Layout](./form-layout.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| checkbox | Use when the selection is part of a multi-value form field or a list where zero, one, or many items may be chosen and the choice is not applied until a save or submit action occurs. |
| toggle-switch | Use when a binary setting must take effect the moment the user interacts with it, and the on/off metaphor clearly communicates the outcome without additional confirmation. |

## HTML Structure

```html
<!-- Checkbox — unchecked -->
<div class="flex items-center gap-1">
  <input type="checkbox" class="accent-gray-800 cursor-pointer">
  <span class="text-base text-gray-600">Label</span>
</div>

<!-- Checkbox — checked -->
<div class="flex items-center gap-1">
  <input type="checkbox" checked class="accent-gray-800 cursor-pointer">
  <span class="text-base text-gray-600">Label</span>
</div>

<!-- Checkbox — disabled -->
<div class="flex items-center gap-1">
  <input type="checkbox" disabled class="accent-gray-800 cursor-not-allowed opacity-50">
  <span class="text-base text-gray-600 opacity-50">Label</span>
</div>

<!-- Toggle Switch — off -->
<div class="flex items-center gap-2">
  <button type="button" class="relative inline-flex flex-shrink-0 items-center rounded-full transition-colors duration-200 cursor-pointer bg-gray-200" style="width:32px;height:18px">
    <span class="inline-block rounded-full bg-white shadow transform transition-transform duration-200 translate-x-[3px]" style="width:14px;height:14px"></span>
  </button>
  <span class="text-base text-gray-600">Off</span>
</div>

<!-- Toggle Switch — on -->
<div class="flex items-center gap-2">
  <button type="button" class="relative inline-flex flex-shrink-0 items-center rounded-full transition-colors duration-200 cursor-pointer bg-gray-700" style="width:32px;height:18px">
    <span class="inline-block rounded-full bg-white shadow transform transition-transform duration-200 translate-x-[15px]" style="width:14px;height:14px"></span>
  </button>
  <span class="text-base text-gray-600">On</span>
</div>

<!-- Toggle Switch — disabled -->
<div class="flex items-center gap-2">
  <button type="button" class="relative inline-flex flex-shrink-0 items-center rounded-full transition-colors duration-200 cursor-not-allowed bg-gray-200 opacity-50" style="width:32px;height:18px">
    <span class="inline-block rounded-full bg-white shadow transform transition-transform duration-200 translate-x-[3px]" style="width:14px;height:14px"></span>
  </button>
  <span class="text-base text-gray-600 opacity-50">Disabled</span>
</div>
```

## Dos & Don'ts

### Do

- Always pair a checkbox or toggle switch with a visible text label so the purpose of the control is unambiguous.
- Apply `opacity-50` and `cursor-not-allowed` to both the control and its label when rendering the disabled state, keeping them visually consistent.
- Use `translate-x-[3px]` for the off position and `translate-x-[15px]` for the on position of the toggle pill to match the design system's fixed 32x18px track dimensions.
- Group related checkboxes with consistent vertical or horizontal spacing (`gap-6` between items, `gap-1` between input and label) as shown in the reference section.
- Reflect toggle state changes immediately in the UI so users receive instant feedback without needing to save.

### Don't

- Do not omit the label on a toggle switch and rely solely on position or color to convey state — this fails users with color vision deficiency and breaks screen reader expectations.
- Do not use a toggle switch inside a multi-field form that has a submit button — the immediate-action metaphor conflicts with deferred submission and confuses users about when changes apply.
- Do not scale the toggle track or pill outside the `32x18px` / `14x14px` specification — custom sizes break the pixel-precise `translate-x` values that position the pill correctly.
- Do not render a checkbox without a `<label>` or adjacent `<span>` — unlabeled checkboxes are inaccessible and violate WCAG 2.1 Success Criterion 1.3.1.
- Do not use color alone to distinguish the checked state of a checkbox; always rely on the browser-native checked indicator supplemented by `accent-gray-800`.

## Patterns & Rules

1. **Immediate vs. deferred action** — Toggle switches always apply their change instantly; checkboxes accumulate selections for a later commit action such as a form submit or a bulk-operation button.
2. **Disabled state parity** — Both variants use `opacity-50` on the control and the label text simultaneously so the entire interactive unit appears equally unavailable.
3. **Label alignment** — The checkbox uses `gap-1` between the input and its label, while the toggle switch uses `gap-2` to account for the wider track width; do not swap these values.
4. **Toggle pill positioning** — The pill's off/on position is driven entirely by Tailwind translate utilities (`translate-x-[3px]` off, `translate-x-[15px]` on) applied to the inner `<span>`; toggling is implemented by swapping these classes along with the track background between `bg-gray-200` and `bg-gray-700`.
5. **State label documentation** — In the design system reference, each state is annotated with a `.state-label` element (Unchecked, Checked, Disabled, Off, On); these labels are documentation-only and must not be included in production UI.

## Accessibility

- Checkbox: the native `<input type="checkbox">` provides the `checkbox` ARIA role automatically; no additional `role` attribute is needed.
- Toggle switch: because it is implemented as a `<button>`, add `role="switch"` and `aria-checked="true|false"` to expose the binary state to assistive technologies.
- Keyboard — Checkbox: `Tab` moves focus to the control, `Space` toggles the checked state. Toggle switch: `Tab` moves focus, `Space` or `Enter` activates the switch and flips `aria-checked`.
- Disabled controls must carry the `disabled` attribute (checkbox) or `aria-disabled="true"` plus `tabindex="-1"` (toggle button) so screen readers announce the unavailable state without accepting input.
- Label text must be programmatically associated: for checkboxes wrap both in a `<label>` or use `aria-labelledby`; for toggle buttons set `aria-label` or `aria-labelledby` pointing to the adjacent `<span>`.

## Related Components

- [Form Layout](./form-layout.md) — Provides the grid-based field layout that hosts checkboxes in multi-field forms, supplying consistent spacing and label positioning.
- [Toggle & Segment](./toggle-and-segment.md) — Offers segmented binary or multi-option switching for contexts where two or more mutually exclusive modes must be presented together in a button-group style.
