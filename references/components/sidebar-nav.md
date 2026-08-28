---
component: Sidebar Nav
category: Data Display
variants: [thin, compact]
related: [tab-bar, details-sidebar-nav]
---

# Sidebar Nav

> A vertical icon-based navigation strip fixed to the left edge of the application shell that gives users persistent, single-click access to top-level sections.

## Overview

The Sidebar Nav is a narrow, vertically stacked list of icon items rendered inside a white panel with a subtle border. It occupies the leftmost column of the layout and communicates the active section through a warm amber highlight (`bg-[#e9e0d2]` / `text-[#804604]`) with a rounded rectangle behind the icon. It serves as the primary wayfinding component for the application, always visible regardless of which page the user is on.

## When to Use

- When the application has five to eight top-level navigation destinations that must remain accessible at all times.
- When screen real estate is at a premium and a full-width top navigation bar would consume too much vertical space.
- When users switch frequently between sections (for example, moving between Work Orders, Customers, and Schedule during a single workflow).
- When a persistent visual indicator of the current section is required without any additional label hierarchy.
- When the product targets desktop or large-tablet viewports where a fixed side column is practical.

## When NOT to Use

- When a page has multiple sub-sections within a single entity record — use [Details Sidebar Nav](./details-sidebar-nav.md) instead, which is designed for in-record panel switching.
- When navigation items number fewer than three or more than eight — use [Tab Bar](./tab-bar.md) instead for a smaller, inline set of destinations.

## Variants

| Variant | Description |
|---------|-------------|
| thin | 80 px wide, icon only, no label. Choose this when horizontal space is severely constrained or when icons are universally recognizable without a text label. |
| compact | 112 px wide, icon stacked above a short text label. Choose this when users are less familiar with the icon set and the extra label reduces cognitive load. |

## HTML Structure

```html
<!-- Thin variant (80px wide, icon only) -->
<div class="bg-white border border-gray-200 rounded-lg overflow-hidden" style="width:80px;">

  <!-- Active item -->
  <div style="height:64px; padding:0 16px; display:flex; flex-direction:column; justify-content:center;">
    <div style="display:flex; align-items:center; justify-content:center;">
      <div style="padding:12px; border-radius:12px; background:#e9e0d2; color:#804604; display:flex; align-items:center; justify-content:center;">
        <i class="ti ti-briefcase text-2xl"></i>
      </div>
    </div>
  </div>

  <!-- Default item -->
  <div style="height:64px; padding:0 16px; display:flex; flex-direction:column; justify-content:center;">
    <div style="display:flex; align-items:center; justify-content:center;">
      <div style="padding:12px; border-radius:4px; display:flex; align-items:center; justify-content:center; color:rgba(30,41,59,0.6);">
        <i class="ti ti-users text-2xl"></i>
      </div>
    </div>
  </div>

  <!-- Hover item -->
  <div style="height:64px; padding:0 16px; display:flex; flex-direction:column; justify-content:center;">
    <div style="display:flex; align-items:center; justify-content:center;">
      <div style="padding:12px; border-radius:4px; background:rgba(30,41,59,0.05); display:flex; align-items:center; justify-content:center; color:rgba(30,41,59,0.8);">
        <i class="ti ti-map-pin text-2xl"></i>
      </div>
    </div>
  </div>

</div>

<!-- Compact variant (112px wide, icon + label) -->
<div class="bg-white border border-gray-200 rounded-lg overflow-hidden" style="width:112px;">

  <!-- Active item -->
  <div style="padding:4px 0 0 0;">
    <div style="margin:4px 8px 0 8px;">
      <div style="flex-direction:column; justify-content:center; padding:12px; border-radius:6px; background:#e9e0d2; color:#804604; display:flex; align-items:center; cursor:pointer;">
        <i class="ti ti-briefcase text-2xl"></i>
        <span style="font-size:12px; font-weight:500; text-align:center; line-height:16px; margin-top:8px;">Work Orders</span>
      </div>
    </div>
  </div>

  <!-- Default item -->
  <div style="padding:4px 0 0 0;">
    <div style="margin:4px 8px 0 8px;">
      <div style="flex-direction:column; justify-content:center; padding:12px; border-radius:6px; display:flex; align-items:center; cursor:pointer; color:rgba(30,41,59,0.6);">
        <i class="ti ti-users text-2xl"></i>
        <span style="font-size:12px; font-weight:500; text-align:center; line-height:16px; margin-top:8px; opacity:0.8;">Customers</span>
      </div>
    </div>
  </div>

  <!-- Hover item -->
  <div style="padding:4px 0 0 0;">
    <div style="margin:4px 8px 0 8px;">
      <div style="flex-direction:column; justify-content:center; padding:12px; border-radius:6px; background:rgba(30,41,59,0.05); display:flex; align-items:center; cursor:pointer; color:rgba(30,41,59,0.8);">
        <i class="ti ti-map-pin text-2xl"></i>
        <span style="font-size:12px; font-weight:500; text-align:center; line-height:16px; margin-top:8px;">Assets</span>
      </div>
    </div>
  </div>

</div>
```

## Dos & Don'ts

### Do

- Keep the icon set consistent: use Tabler Icons (`ti ti-*`) at `text-2xl` across all items so visual weight is uniform.
- Apply the active state token (`background:#e9e0d2; color:#804604`) to exactly one item at a time to reflect the current route.
- Use the thin variant when the icon meaning is well established for your user base; icons alone must be self-explanatory without a tooltip.
- Add `title` attributes or ARIA labels to each nav item so the accessible name is available even in the thin variant.
- Maintain the fixed item height (64 px thin, padding-based compact) so the strip remains predictably sized regardless of label length.

### Don't

- Do not mix thin and compact items within the same sidebar instance — inconsistent heights break the rhythm of the vertical list.
- Do not add more than eight items to the strip; overloading the sidebar forces scrolling and hides destinations from immediate view.
- Do not place secondary or context-specific actions (such as record-level panels) in this component — use [Details Sidebar Nav](./details-sidebar-nav.md) for that purpose, as it is scoped to a single record.
- Do not apply custom background colors for the active state other than the design-token pair `#e9e0d2` / `#804604`; diverging breaks brand consistency across the app.
- Do not abbreviate labels in the compact variant to fewer than two characters; single-letter labels reduce scanability and cause localization issues.

## Patterns & Rules

1. **Single active item** — Only one navigation item may carry the active background (`background:#e9e0d2`) at any time; the active item reflects the current top-level route and must be updated on every navigation event.
2. **Icon padding determines touch target** — Each icon sits inside a `padding:12px` container rather than relying on the row height alone, so the tap/click target is at least 44 px square in both variants.
3. **Hover state is separate from active** — The hover background is `rgba(30,41,59,0.05)` with `color:rgba(30,41,59,0.8)`, which is visually distinct from the active amber token and must never be applied to the currently active item.
4. **Border radius differs by variant** — Active items use `border-radius:12px` in the thin variant and `border-radius:6px` in the compact variant; use these values exactly to match the design system specification.
5. **Compact label typography** — Labels in the compact variant are `font-size:12px; font-weight:500; line-height:16px` and centered below the icon; do not increase font size or switch to regular weight, as this disrupts vertical rhythm across items.

## Accessibility

- Each nav item must have a descriptive `title` attribute or `aria-label` so assistive technologies announce the destination, especially in the thin variant where no visible label is present.
- Keyboard users must be able to Tab through all nav items in document order; the active item should carry `aria-current="page"` to signal the current location to screen readers.
- The container element should be a `<nav>` with `aria-label="Main navigation"` to distinguish it from other navigation landmarks on the page (for example, the Details Sidebar Nav).
- Focus indicators must remain visible; do not suppress the default outline on item focus — augment it with the design system's focus ring token if needed.

## Related Components

- [Tab Bar](./tab-bar.md) — Provides horizontal tab-style navigation for a smaller, flat set of destinations within a single view rather than across the whole application.
- [Details Sidebar Nav](./details-sidebar-nav.md) — A narrow icon strip attached to a detail record panel that switches between contextual sub-sections (attachments, activity, history) rather than top-level routes.
