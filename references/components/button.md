---
component: Button
category: Interactive
variants: [ghost, text, small, standard, button-group]
related: [icon-button, toggle-and-segment]
---

# Button

> A labelled, clickable control that triggers a discrete action, giving users a clear and consistent affordance for submitting forms, opening flows, or executing commands.

## Overview

Buttons in the Zuper design system are built on native `<button>` elements and styled entirely through Tailwind utility classes — no custom base class is required. They appear in four visual weights — ghost/text, small, standard, and grouped — each mapped to a distinct level of visual prominence in the interface. The component always pairs an optional icon with a text label to make the action self-describing; when it does, add `pr-2` alongside the variant's own horizontal padding so the label sits with balanced right-side breathing room next to the icon.

## When to Use

- Triggering a primary action on a page or panel, such as creating a new job, saving a form, or submitting a filter.
- Providing a secondary or cancel action alongside a primary action so the user has a clear escape path.
- Offering a low-emphasis inline action inside a table row, card, or list item where a full-weight button would be visually noisy.
- Switching between mutually exclusive views (e.g. List, Map, Kanban) when the set of options is fixed and small.

## When NOT to Use

- When the action navigates to another page and should be perceived as a link — use an `<a>` element styled as inline text instead.
- When the action is purely icon-based with no label — use [Icon Button](./icon-button.md) instead.
- When the user needs to toggle between two persistent states (on/off) — use [Toggle & Segment](./toggle-and-segment.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| ghost | A text-only button with no background fill; use for low-priority inline actions where visual weight must be minimal. |
| text | Functionally identical to ghost but typically appears without an icon; use inside dense UI surfaces like table cells or sidebars. |
| small | A compact filled button (`bg-primary` or `border-border`) for tight layouts such as table toolbars, filter chips, or card headers where a standard button is too tall. |
| standard | The default action button for primary and secondary actions on forms, modals, and page-level toolbars; supports a loading spinner state. |
| button-group | Two or more standard-height buttons joined in a flush row to let the user switch between mutually exclusive views; only one item carries the active background at a time. |

## HTML Structure

```html
<!-- Ghost / Text Button -->
<button class="inline-flex items-center space-x-1 text-md font-medium text-blue-500 px-1 py-0.5 pr-2 rounded-md cursor-pointer">
  <i class="ti ti-plus"></i>
  <span>Label</span>
</button>

<!-- Small Button — Primary -->
<button class="inline-flex items-center space-x-1 text-md font-medium bg-primary text-white px-1.5 py-1 pr-2 rounded-lg cursor-pointer">
  <i class="ti ti-plus"></i>
  <span>Label</span>
</button>

<!-- Small Button — Secondary -->
<button class="inline-flex items-center space-x-1 text-md font-medium border border-border text-gray-600 px-1.5 py-1 pr-2 rounded-lg cursor-pointer">
  <i class="ti ti-plus"></i>
  <span>Label</span>
</button>

<!-- Standard Button — Primary -->
<button class="inline-flex items-center justify-center gap-1 whitespace-nowrap rounded-lg border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit disabled:opacity-50 disabled:pointer-events-none hover:bg-primary px-2 py-1.5 pr-2 bg-primary text-white border-transparent font-medium">
  <em class="ti ti-plus text-lg"></em>
  <span class="leading-tight text-base font-normal">Label</span>
</button>

<!-- Standard Button — Primary Loading -->
<button class="inline-flex items-center justify-center gap-1 whitespace-nowrap rounded-lg border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit disabled:opacity-50 disabled:pointer-events-none hover:bg-primary px-2 py-1.5 pr-2 bg-primary text-white border-transparent font-medium">
  <em class="ti ti-loader-2 animate-spin text-lg"></em>
  <span class="leading-tight text-base font-normal">Label</span>
</button>

<!-- Standard Button — Primary Disabled -->
<button class="inline-flex items-center justify-center gap-1 whitespace-nowrap rounded-lg border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit disabled:opacity-50 disabled:pointer-events-none hover:bg-primary px-2 py-1.5 pr-2 bg-primary text-white border-transparent font-medium disabled" disabled>
  <em class="ti ti-plus text-lg"></em>
  <span class="leading-tight text-base font-normal">Label</span>
</button>

<!-- Standard Button — Secondary -->
<button class="inline-flex items-center justify-center gap-1 whitespace-nowrap rounded-lg border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit hover:bg-gray-50 disabled:opacity-50 disabled:pointer-events-none px-2 py-1.5 pr-2">
  <em class="ti ti-plus text-lg"></em>
  <span class="leading-tight text-base font-normal">Label</span>
</button>

<!-- Button Group -->
<div class="inline-flex">
  <button class="py-2 px-4 border border-border bg-gray-50 text-base text-gray-600 rounded-l-lg rounded-r-none">List</button>
  <button class="py-2 px-4 border border-border bg-white text-base text-gray-600 rounded-none -ml-px">Map</button>
  <button class="py-2 px-4 border border-border bg-white text-base text-gray-600 rounded-r-lg rounded-l-none -ml-px">Kanban</button>
</div>
```

## Dos & Don'ts

### Do

- Apply the full standard-button Tailwind class set (`inline-flex items-center justify-center gap-1 whitespace-nowrap rounded-lg border border-border text-sm text-gray-600 shadow-sm outline-none cursor-pointer transition-colors w-fit`) to every standard-weight button so border, radius, and flex behaviour stay consistent — there is no shared base class to inherit it from.
- Apply `disabled` both as a CSS class and as the native HTML `disabled` attribute so the button is excluded from both visual interaction and keyboard focus.
- Show a `ti-loader-2 animate-spin` icon in place of the action icon during async operations to communicate progress without removing the button.
- Keep button labels short (one to three words) so the action is scannable at a glance.
- Collapse borders between adjacent buttons in a group with `-ml-px` so they read as a single cohesive control.

### Don't

- Do not use `pointer-events-none` alone to disable a button — the native `disabled` attribute must also be set, otherwise the element remains in the tab order and is announced as interactive by screen readers.
- Do not mix ghost and standard variants in the same toolbar for actions of equal importance — inconsistent weight sends a false hierarchy signal to the user.
- Do not place more than one primary (`bg-primary`) button in a single view region, as competing primaries eliminate the visual hierarchy that guides user attention.
- Do not omit the icon's containing `<em>` or `<i>` element class; without `text-lg` the icon will not align with the label baseline.
- Do not create a button group with more than five items — use a dropdown or segmented control instead to avoid horizontal overflow on small viewports.

## Patterns & Rules

1. **Primary vs. secondary pairing** — When a form or modal offers two actions, place the primary (`bg-primary`) button on the right and the secondary standard button (without a fill) on the left, so the destructive or dismissive action is never the first tap target.
2. **Loading state ownership** — The loading state belongs to the button that triggered the request; keep it mounted and disable pointer events for the duration so users cannot double-submit.
3. **Ghost buttons in dense surfaces** — Reserve the ghost/text variant for surfaces where adding a border or fill would compete with surrounding data; never use it as the sole call-to-action on an empty state or landing surface.
4. **Button group active state** — Mark the active item in a button group with `bg-gray-50` on its own background; do not rely on text colour alone, as colour is not sufficient for users with colour vision deficiencies.
5. **Icon placement** — Always put the icon before the label (`<em>` then `<span>`) to match the left-to-right reading direction and the established pattern across all button variants in this system.

## Accessibility

- Use a native `<button>` element so the browser provides `role="button"`, keyboard activation, and focus management automatically.
- Keyboard interaction: `Tab` moves focus to the button; `Enter` or `Space` activates it; `Escape` does not dismiss the button itself but should close any overlay the button opened.
- When using `disabled`, the HTML `disabled` attribute removes the element from the tab order; if the button must remain focusable (to show a tooltip explaining why it is disabled), use `aria-disabled="true"` with `pointer-events-none` instead.
- For icon-only content inside a button group (e.g. icon labels without visible text), add `aria-label` on each `<button>` so screen readers announce the purpose.

## Related Components

- [Icon Button](./icon-button.md) — A square button containing only an icon; use when there is no room for a text label and the icon meaning is unambiguous from context.
- [Toggle & Segment](./toggle-and-segment.md) — A pill-style segmented control for persistent state switching; use instead of a button group when the options represent modes rather than one-off actions.
