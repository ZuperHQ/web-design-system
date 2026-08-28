---
component: Colors
category: Design System Foundations
variants: [primary, secondary, semantic, neutral, status]
related: [typography, spacing-and-icons]
---

# Colors

> The Colors foundation defines the canonical set of semantic color tokens used across the Zuper design system to ensure consistent visual communication, brand alignment, and accessible contrast throughout the UI.

## Overview

The Zuper color palette is organized into five functional groups: brand, surface, neutral, border, and status colors. Each token maps a semantic role (such as `surface`, `text-default`, or `destructive`) to a specific hex value via a Tailwind utility class, making intent explicit and preventing ad-hoc color choices. This palette forms the visual backbone of every component in the system — from backgrounds and borders to interactive feedback states.

## When to Use

- Apply `bg-product-light` as the primary tinted background behind highlighted or selected UI regions that need brand presence without full saturation.
- Apply `bg-theme` as the application-level page background to maintain the warm, low-contrast canvas the layout is designed around.
- Apply `bg-theme-light` for card and panel surfaces that sit atop the app background, creating the standard one-level elevation pattern.
- Apply status colors (`bg-red-500`, `bg-amber-500`, `bg-green-500`, `bg-blue-500`) for inline feedback — error, warning, success, and informational states respectively.
- Apply `text-gray-600` for primary body copy and `text-gray-500` for secondary or supporting labels to maintain the correct text hierarchy.

## When NOT to Use

- Do not reach for arbitrary Tailwind gray, color, or hex values for text — use [Typography](./typography.md) tokens (`text-gray-600`, `text-gray-500`, `text-gray-400`) which are already calibrated for contrast.
- Do not use status colors (destructive, warn, success, info) as decorative or branding accents — use [Spacing and Icons](./spacing-and-icons.md) alongside brand color (`gray-800` · `#1E293B`) for purely presentational highlights.

## Variants

| Variant | Description |
|---------|-------------|
| primary | Use `bg-product-light` (#FCEDE8) when a surface needs a soft brand-tinted wash, such as a selected row or an active sidebar item. |
| secondary | Use `bg-theme` (#f8f2ec) as the outermost application background; do not nest it inside other surfaces. |
| neutral | Use `bg-theme-light` (#FDFDFC) for cards, panels, and modals that float above the app background at the first elevation level. |
| semantic | Use `border-border` (#E2E8F0) for standard dividers and input outlines, and `border-gray-400` (#94A3B8) when a stronger, more prominent border is required. |
| status | Use `bg-red-500` (destructive), `bg-amber-500` (warn), `bg-green-500` (success), or `bg-blue-500` (info) to communicate operational feedback states consistently. |

## HTML Structure

```html
<!-- Color swatch grid — mirrors the palette reference layout -->
<div class="grid grid-cols-7 gap-4">

  <!-- Brand -->
  <div>
    <div class="h-12 rounded-lg" style="background:#1E293B"></div>
    <div class="mt-1 text-base text-gray-600">brand</div>
    <div class="text-xs text-gray-400">gray-800 · #1E293B</div>
  </div>

  <!-- Primary surface -->
  <div>
    <div class="h-12 rounded-lg bg-product-light border border-gray-200"></div>
    <div class="mt-1 text-base text-gray-600">primary</div>
    <div class="text-xs text-gray-400">bg-product-light · #FCEDE8</div>
  </div>

  <!-- App background -->
  <div>
    <div class="h-12 rounded-lg bg-theme border border-gray-200"></div>
    <div class="mt-1 text-base text-gray-600">app-bg</div>
    <div class="text-xs text-gray-400">bg-theme · #f8f2ec</div>
  </div>

  <!-- Card / panel surface -->
  <div>
    <div class="h-12 rounded-lg bg-theme-light border border-gray-200"></div>
    <div class="mt-1 text-base text-gray-600">surface</div>
    <div class="text-xs text-gray-400">bg-theme-light · #FDFDFC</div>
  </div>

  <!-- Default border -->
  <div>
    <div class="h-12 rounded-lg border border-border" style="background:#E2E8F0"></div>
    <div class="mt-1 text-base text-gray-600">border</div>
    <div class="text-xs text-gray-400">border-border · #E2E8F0</div>
  </div>

  <!-- Strong border -->
  <div>
    <div class="h-12 rounded-lg bg-gray-400"></div>
    <div class="mt-1 text-base text-gray-600">border-strong</div>
    <div class="text-xs text-gray-400">border-gray-400 · #94A3B8</div>
  </div>

  <!-- Text default -->
  <div>
    <div class="h-12 rounded-lg bg-gray-600"></div>
    <div class="mt-1 text-base text-gray-600">text-default</div>
    <div class="text-xs text-gray-400">text-gray-600 · #475569</div>
  </div>

  <!-- Text secondary -->
  <div>
    <div class="h-12 rounded-lg bg-gray-500"></div>
    <div class="mt-1 text-base text-gray-600">text-secondary</div>
    <div class="text-xs text-gray-400">text-gray-500 · #64748B</div>
  </div>

  <!-- Text disabled -->
  <div>
    <div class="h-12 rounded-lg bg-gray-400"></div>
    <div class="mt-1 text-base text-gray-600">text-disabled</div>
    <div class="text-xs text-gray-400">text-gray-400 · #94A3B8</div>
  </div>

  <!-- Destructive / error -->
  <div>
    <div class="h-12 rounded-lg bg-red-500"></div>
    <div class="mt-1 text-base text-gray-600">destructive</div>
    <div class="text-xs text-gray-400">bg-red-500 · #EF4444</div>
  </div>

  <!-- Warning -->
  <div>
    <div class="h-12 rounded-lg bg-amber-500"></div>
    <div class="mt-1 text-base text-gray-600">warn</div>
    <div class="text-xs text-gray-400">bg-amber-500 · #F59E0B</div>
  </div>

  <!-- Success -->
  <div>
    <div class="h-12 rounded-lg bg-green-500"></div>
    <div class="mt-1 text-base text-gray-600">success</div>
    <div class="text-xs text-gray-400">bg-green-500 · #22C55E</div>
  </div>

  <!-- Info -->
  <div>
    <div class="h-12 rounded-lg bg-blue-500"></div>
    <div class="mt-1 text-base text-gray-600">info</div>
    <div class="text-xs text-gray-400">bg-blue-500 · #3B82F6</div>
  </div>

</div>
```

## Dos & Don'ts

### Do

- Use semantic token names (`bg-product-light`, `bg-theme`, `bg-theme-light`, `border-border`) instead of raw hex values so that theming and palette updates propagate automatically.
- Pair `text-gray-600` with `bg-theme-light` surfaces — this is the default pairing verified for contrast within the system.
- Apply status colors (`bg-red-500`, `bg-amber-500`, `bg-green-500`, `bg-blue-500`) only within feedback UI: alerts, badges, toast notifications, and validation messages.
- Use `border-border` for all standard container edges and form inputs; escalate to `border-gray-400` only when a visually stronger separator is semantically required.
- Keep the brand color (`gray-800` · `#1E293B`) reserved for the logo, primary call-to-action components, and the brand-tinted surface (`bg-product-light`).

### Don't

- Do not use status colors as backgrounds for large surface areas — they carry strong semantic meaning and will confuse users about the intent of the region.
- Do not hard-code hex values inline when a named token exists; raw hex values bypass the design system and break any future palette migration.
- Do not use `text-gray-400` (text-disabled) for active, interactive, or informational text — it signals a non-interactive disabled state and will fail contrast requirements.
- Do not nest `bg-theme` (app-bg) inside a card or panel; it is an outermost canvas color and will visually flatten the elevation hierarchy.
- Do not combine two status colors on the same surface or label — each status color has exclusive semantic meaning and mixing them creates ambiguous feedback.

## Patterns & Rules

1. **Semantic layering** — Always compose surfaces in the prescribed order: `bg-theme` (page) > `bg-theme-light` (card/panel) > `bg-product-light` (highlighted region). Inverting or skipping layers breaks the visual depth model.
2. **Status exclusivity** — Each status color maps to exactly one meaning: red = destructive/error, amber = warning, green = success, blue = informational. Never repurpose a status color for a different meaning, even in one-off cases.
3. **Text hierarchy via gray scale** — Use `text-gray-600` for primary readable content, `text-gray-500` for supporting or secondary labels, and `text-gray-400` only for disabled or placeholder text.
4. **Border strength as signal** — `border-border` (#E2E8F0) is the default low-emphasis divider; escalate to `border-gray-400` (#94A3B8) only when a boundary needs stronger visual weight, such as an active input focus ring supplement or a section separator.
5. **Brand restraint** — The brand color (`gray-800` · `#1E293B`) and its tint (`bg-product-light`) are reserved for intentional brand moments. Spreading them across incidental UI elements dilutes brand impact and creates visual noise.

## Accessibility

- All text colors in the system (`text-gray-600` on `bg-theme-light`) must maintain a minimum 4.5:1 contrast ratio per WCAG 2.1 AA for normal text.
- Status colors used as icon or badge fills must be accompanied by a text label or `aria-label` — color alone must never be the sole conveyor of meaning.
- Disabled text (`text-gray-400`) must only appear on non-interactive or disabled controls; screen readers must receive a corresponding `disabled` or `aria-disabled="true"` attribute on the host element.

## Related Components

- [Typography](./typography.md) — Typography specifies which color tokens to apply to each text size and weight class, completing the text rendering contract started by the Colors foundation.
- [Spacing and Icons](./spacing-and-icons.md) — Icons use the same gray-scale color tokens for fill and stroke, and spacing tokens define the gap between color swatches in layout compositions.
