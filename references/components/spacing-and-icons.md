---
component: Spacing & Icons
category: Design System Foundations
variants: [spacing-scale, utility-reference, tabler-icons]
related: [colors, typography]
---

# Spacing & Icons

> The spacing scale and Tabler icon library are the shared foundation that ensures consistent visual rhythm and iconography across every surface in the Zuper UI.

## Overview

Spacing is defined as a fixed numeric scale (0.5 through 12) where each unit equals 0.25rem, applied via Tailwind utility classes for padding, margin, and gap. Tabler Icons are rendered as `<i>` tags using `ti ti-*` CSS classes and are grouped into semantic categories — Actions, Navigation, Search & View, Status & Alerts, Communication, Calendar & Time, People & Business, Finance, and Files & Media. Together these two systems enforce predictable density and visual consistency without component-level overrides.

## When to Use

- When spacing elements within a component — pick from the defined scale (0.5–12) instead of arbitrary pixel values.
- When adding an icon to a button, label, status indicator, or navigation item — choose from the curated `ti ti-*` set.
- When laying out sibling elements horizontally — use `space-x-*` or `gap-*` from the scale rather than margins on individual children.
- When laying out stacked vertical content — use `space-y-*` or `gap-*` from the scale to maintain consistent vertical rhythm.
- When building an equal-column data display (stats cards, form grids) — use `grid grid-cols-*` with `gap-*` from the scale.

## When NOT to Use

- When the need is decorative illustration or a brand logo rather than a UI affordance — use an inline SVG asset instead of a `ti ti-*` icon.
- When conveying semantic status with colour and shape together — use [Colors](./colors.md) tokens alongside icons rather than relying on icon shape alone.

## Variants

| Variant | Description |
|---------|-------------|
| spacing-scale | Use when you need to apply a padding, margin, or gap value; select the closest step from 0.5–12 rather than writing an arbitrary rem value. |
| utility-reference | Use when deciding which Tailwind spacing utility class to reach for — `p-*`, `px-*`/`py-*`, `mx-*`/`my-*`, `space-x-*`/`space-y-*`, or `gap-*` — based on the layout relationship (sibling gap vs. container padding vs. axis margin). |
| tabler-icons | Use when an action, navigation cue, status signal, or domain concept needs a visual glyph; always pick from the approved `ti ti-*` subset documented here. |

## HTML Structure

```html
<!-- Spacing: visualising a scale step -->
<div class="flex flex-col items-center gap-1">
  <div class="w-6 h-4 bg-primary rounded"></div>
  <div class="text-base text-gray-600 font-mono">4</div>
  <div class="text-base text-gray-600">1rem</div>
</div>

<!-- Utility reference card -->
<div class="border border-border rounded-lg px-3 py-2.5">
  <div class="text-base font-mono text-gray-800 font-semibold mb-1">gap-*</div>
  <div class="text-base text-gray-600 mb-1.5">Flex / grid gap</div>
  <div class="text-base text-gray-600">Used: 0.5, 1, 1.5, 2, 2.5, 3, 4</div>
</div>

<!-- Layout convention: primary (flex) -->
<div class="flex-1 border border-border rounded-lg px-3 py-2.5 bg-product-light">
  <div class="text-base font-mono text-gray-800 font-semibold mb-1">flex · flex-col · items-* · justify-*</div>
  <div class="text-base text-gray-600 mb-1">Primary layout — use for almost everything</div>
  <div class="text-base text-gray-600">Combine with space-x-* / space-y-* or gap-* for element spacing</div>
</div>

<!-- Tabler icon — single glyph with border container -->
<div class="flex flex-col items-center gap-1">
  <i class="ti ti-pencil text-lg text-gray-600 p-2 rounded-lg border border-border"></i>
  <div class="text-base text-gray-500">ti-pencil</div>
</div>

<!-- Icon group row (Actions category example) -->
<div class="flex flex-wrap gap-10">
  <div class="flex flex-col items-center gap-1">
    <i class="ti ti-plus text-lg text-gray-600 p-2 rounded-lg border border-border"></i>
    <div class="text-base text-gray-500">ti-plus</div>
  </div>
  <div class="flex flex-col items-center gap-1">
    <i class="ti ti-trash text-lg text-gray-600 p-2 rounded-lg border border-border"></i>
    <div class="text-base text-gray-500">ti-trash</div>
  </div>
</div>
```

## Dos & Don'ts

### ✅ Do

- Use `flex` and `flex-col` as the primary layout mechanism; reach for `grid grid-cols-*` only for equal-column displays like stat cards or form grids.
- Combine `space-x-*` / `space-y-*` with flex for sibling gaps, and `gap-*` with grid — keep the utility semantically correct for its layout context.
- Size icons with `text-lg` in standard inline contexts and keep them on the scale (e.g. `p-2` for the bordered icon container).
- Choose the most semantically specific icon available — prefer `ti-alert-triangle` for warnings over a generic `ti-info-circle`.
- Stick to the curated `ti ti-*` subset shown in the reference; the full Tabler library contains thousands of icons that are not approved for this system.

### ❌ Don't

- Do not use arbitrary spacing values (e.g. `mt-[7px]`) — the design scale only defines steps 0.5, 1, 1.5, 2, 2.5, 3, 4, 5, 6, 8, 9, 10, 12, and deviations break visual rhythm.
- Do not use `grid` for asymmetric or flowing layouts — it forces equal column widths where flex would be correct, leading to broken responsive behaviour.
- Do not combine `space-x-*` and `gap-*` on the same container — they both control sibling spacing and will conflict, producing inconsistent results.
- Do not apply icons without associated label text in contexts where the action is ambiguous — unlabelled icons fail WCAG 2.1 at small sizes without a tooltip or `aria-label`.
- Do not scale icons outside the spacing system (e.g. `w-7 h-7` arbitrary sizes) — use the text-size utilities (`text-lg`, `text-xl`) to keep icon sizing on the type scale.

## Patterns & Rules

1. **Scale-only spacing** — Every spacing decision must resolve to one of the 13 defined scale steps (0.5–12). Arbitrary rem or px values are not permitted, as they break the density contract between components.
2. **Flex first, grid second** — Use `flex` / `flex-col` with `items-*` / `justify-*` for virtually all layout work; only switch to `grid grid-cols-*` when the design explicitly requires equal, fixed-width columns.
3. **Icon sizing via text utilities** — Icons inherit size from Tailwind text-size classes (`text-lg` = 1.125rem is the standard inline size); do not use `w-*` / `h-*` to size icons because it breaks the relationship between icon weight and surrounding text.
4. **Semantic icon selection** — Always pick the icon whose name most accurately describes the action or concept (e.g. `ti-calendar-event` for a scheduled event, not `ti-calendar`); semantic accuracy reduces cognitive load for users scanning the interface.
5. **Padding over margin for containers** — Use `p-*`, `px-*`, `py-*` to create internal breathing room inside bordered or backgrounded containers; reserve `mx-*` / `my-*` for external offset from surrounding content.

## Accessibility

- Icons used as the sole label for an interactive control must carry `aria-label` on the parent element or a visually hidden text alternative so screen readers announce the action.
- Keyboard focus must never land on a bare `<i>` tag; the focusable element must be a `<button>` or `<a>` wrapping the icon, and the focus ring must remain visible at all zoom levels.
- Icon colour must not be the only means of conveying meaning — pair status icons (e.g. `ti-alert-triangle`) with a text label or `aria-label` describing the state, ensuring WCAG 1.4.1 compliance.

## Related Components

- [Colors](./colors.md) — Spacing and icons must always be combined with the colour token system; icon colour is drawn from the same semantic palette (text-gray-600, text-primary, etc.) to maintain consistent meaning across states.
- [Typography](./typography.md) — Icon sizing uses the same Tailwind text-size utilities as the typography scale, so icons and adjacent text stay optically balanced without manual adjustments.
