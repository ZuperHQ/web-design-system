---
component: Typography
category: Design System Foundations
variants: [heading, body, caption, label, code]
related: [colors, spacing-and-icons]
---

# Typography

> Typography provides a consistent set of text size and weight utilities that establish visual hierarchy and readability across the Zuper UI.

## Overview

The Typography system is a scale of eight size classes (`text-xs` through `text-3xl`) paired with six font-weight utilities (`font-light` through `font-extrabold`), all rooted in a custom rem scale calibrated for Zuper's dense data interfaces. Each size class maps to a precise rem value — for example, `text-base` is 0.9rem and `text-lg` is 1rem — ensuring pixel-perfect consistency without ad-hoc font-size overrides. Typography is the backbone of visual hierarchy in the design system: every heading, body copy, caption, form label, and inline code snippet is expressed through these classes.

## When to Use

- Use `text-2xl font-semibold` or `text-3xl font-bold` for page-level section headings that need strong visual hierarchy.
- Use `text-base font-normal` for primary body copy and form field values where readability at small sizes is critical.
- Use `text-sm font-normal` for secondary descriptive text, helper text beneath form fields, and sidebar metadata.
- Use `text-xs font-medium` or `text-xs font-semibold` for captions, badges, and data-dense table cell annotations.
- Use `font-mono` alongside any text size class when rendering code snippets, class names, or monospaced token values.

## When NOT to Use

- Do not use raw `text-*` utilities to communicate status colors or semantic states — use [Colors](./colors.md) instead.
- Do not apply typography classes to decorative icon-only elements where no readable text is present — use [Spacing & Icons](./spacing-and-icons.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| heading | Use `text-xl` – `text-3xl` with `font-semibold` or `font-bold` for section and page headings that anchor content regions. |
| body | Use `text-base font-normal` for the primary reading flow of forms, detail panels, and list content. |
| caption | Use `text-xs` or `text-sm` with `font-normal` for supporting annotations, timestamps, and secondary metadata below primary content. |
| label | Use `text-sm font-medium` or `text-base font-medium` for form field labels, column headers, and interactive control labels. |
| code | Pair any text size class with `font-mono` when rendering class names, tokens, identifiers, or inline technical strings. |

## HTML Structure

```html
<!-- Heading variant -->
<h2 class="text-xl font-semibold text-gray-800 leading-tight">Section Title</h2>

<!-- Body variant -->
<p class="text-base font-normal text-gray-800">Primary body copy goes here.</p>

<!-- Caption variant -->
<span class="text-xs font-normal text-gray-600">Supporting annotation or timestamp</span>

<!-- Label variant -->
<label class="text-sm font-medium text-gray-800 leading-tight">Field Label</label>

<!-- Code / monospaced variant -->
<span class="text-base font-mono text-gray-800">text-base</span>

<!-- Weight showcase row (as used in the typography reference table) -->
<div class="text-base font-light text-gray-800">Light 300</div>
<div class="text-base font-normal text-gray-800">Regular 400</div>
<div class="text-base font-medium text-gray-800">Medium 500</div>
<div class="text-base font-semibold text-gray-800">Semibold 600</div>
<div class="text-base font-bold text-gray-800">Bold 700</div>
<div class="text-base font-extrabold text-gray-800">Extrabold 800</div>
```

## Dos & Don'ts

### Do

- Combine a `text-*` size class with an explicit `font-*` weight class on every text node so size and weight are independently controlled.
- Use `leading-tight` on headings (`text-xl` and above) to keep multi-line titles visually compact in dense layouts.
- Use `text-gray-600` for secondary or supporting text and `text-gray-800` for primary readable text to maintain consistent contrast hierarchy.
- Pair `font-mono` with an existing `text-*` size class (e.g., `text-base font-mono`) when displaying technical identifiers rather than switching to a custom font stack.
- Prefer the nearest step on the defined scale (`text-xs`, `text-sm`, `text-md`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`) over arbitrary inline `font-size` values.

### Don't

- Do not invent intermediate sizes (e.g., `text-[15px]`) outside the defined scale — it breaks the rem rhythm and makes cross-component sizing inconsistent.
- Do not use `font-extrabold` for body or caption text — high-weight classes at small sizes reduce legibility and are reserved for display-level emphasis.
- Do not mix heading semantics with body-scale classes (e.g., `<h1 class="text-xs">`) — semantic HTML element choice must align with the visual size scale.
- Do not rely on `font-weight` alone to communicate meaning (e.g., errors or warnings) — always pair weight changes with a color utility from the Colors system.
- Do not omit a `text-gray-*` color class from text nodes and rely on inherited color — always set the color explicitly so components remain portable.

## Patterns & Rules

1. **Size-weight pairing** — Every text node must declare both a `text-*` size class and a `font-*` weight class; relying on browser defaults produces inconsistent output across components.
2. **Scale fidelity** — The eight-step scale (`text-xs` 0.625rem → `text-3xl` 1.5rem) uses non-standard rem values; never substitute standard Tailwind defaults or raw pixel values, as the Zuper config overrides these.
3. **Heading hierarchy** — Reserve `text-2xl` and `text-3xl` for page- or section-level headings; use `text-xl` for subsection headings and `text-lg` for card or panel titles to maintain a clear three-level hierarchy.
4. **Mono for tokens** — Any string that represents a code token, class name, or system identifier (as seen in the typography reference table itself) must use `font-mono` regardless of surrounding prose weight.
5. **Semantic HTML** — Use the appropriate semantic element (`<h1>`–`<h6>`, `<p>`, `<label>`, `<span>`, `<code>`) in conjunction with typography classes; do not replace semantic meaning with visual styling alone.

## Accessibility

- Headings must use the appropriate `<h1>`–`<h6>` element hierarchy; applying `text-xl font-semibold` to a `<div>` without a role does not convey heading structure to assistive technology.
- Typography classes do not provide keyboard interaction on their own; interactive text (links, buttons) must still use the correct interactive element with visible focus styles.
- Ensure all `text-*` / `font-*` combinations against their background meet WCAG AA contrast ratio (4.5:1 for body text, 3:1 for large text at `text-lg` and above); use `text-gray-800` on `bg-theme-light` for compliant body text.
- Screen readers announce text content directly — do not use CSS `content` or `::before`/`::after` pseudo-elements as a substitute for real DOM text nodes.

## Related Components

- [Colors](./colors.md) — Defines the `text-gray-*`, `text-primary`, and semantic color tokens that are applied alongside typography classes to control text color.
- [Spacing & Icons](./spacing-and-icons.md) — Provides the spacing scale and icon sizing utilities that work alongside typography to control line height, padding, and inline icon alignment within text nodes.
