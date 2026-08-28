---
component: Bottom Navigation Bar
category: Mobile
variants: [four-tabs, five-tabs-with-badge]
related: [tab-bar, details-sidebar-nav, sidebar-nav]
replaces: Sidebar Nav, Tab Bar
---

# Bottom Navigation Bar

> Fixed bottom navigation bar with icon and label tabs; replaces sidebar and top tab navigation on mobile.

## Overview

The Bottom Navigation Bar is a full-width, fixed strip anchored to the bottom edge of the viewport, containing between four and five icon-plus-label tabs that give mobile users persistent, one-tap access to every top-level section of the application. Unlike the desktop [Sidebar Nav](./sidebar-nav.md) — which occupies a fixed left column — the Bottom Navigation Bar runs horizontally and is sized for thumb reach, with each tap target occupying at least 44 px in height and an equal share of the screen width. It replaces both the Sidebar Nav and any top-mounted Tab Bar on viewports narrower than the product's mobile breakpoint, ensuring that primary wayfinding is always reachable in the natural resting position of the user's thumb.

## When to Use

- When the app is rendered in a mobile or small-viewport context (typically below 768 px) and users need persistent access to four or five top-level sections without scrolling or opening a drawer.
- When the primary user workflow involves frequent cross-section jumps — for example, a field technician moving between Work Orders, Schedule, and Customers within a single session.
- When the active section must be immediately legible at a glance, even when the user's hands are occupied or the screen is partially obscured.
- When the application must respect device safe-area insets (iPhone home indicator, Android gesture bar) and the navigation must not overlap system UI.
- When the icon set is universally recognizable to the user base, since labels below icons reinforce meaning but cannot carry ambiguous glyphs alone.

## When NOT to Use

- When the viewport is desktop-sized — use [Sidebar Nav](./sidebar-nav.md) (thin or compact variant) instead, which is optimized for a fixed left column and keyboard navigation patterns.
- When the application has fewer than four or more than five top-level destinations — fewer than four wastes the persistent real estate; more than five crowds the strip beyond safe thumb-reach sizing. Consider a drawer or sheet for overflow items.
- When the navigation is scoped to a single entity record (switching between attachments, activity, and history within a work order) — use [Details Sidebar Nav](./details-sidebar-nav.md), which is purpose-built for in-record panel switching and carries different ARIA semantics.

## Variants

| Variant | Description |
|---------|-------------|
| four-tabs | Four equal-width tabs, each with a Tabler icon above a short text label. Use this as the default; equal widths give each tab the largest possible touch target on narrow screens and prevent any single section from feeling deprioritized. |
| five-tabs-with-badge | Five tabs at slightly reduced width, with one tab supporting a numeric badge overlay for unread counts or pending items (for example, unacknowledged notifications or flagged work orders). Reserve this variant only when a fifth destination genuinely requires attention signaling — do not add a fifth tab merely to surface an additional section. |

## HTML Structure

```html
<!-- Framework-agnostic. Mobile-optimized class names. -->
<!-- Note: env(safe-area-inset-bottom) requires viewport-fit=cover in the meta tag -->

<!-- Four-tabs variant -->
<nav
  role="navigation"
  aria-label="Main navigation"
  class="fixed bottom-0 left-0 right-0 z-50
         bg-white border-t border-border
         pb-[env(safe-area-inset-bottom)]
         flex">

  <!-- Active tab -->
  <a
    href="/work-orders"
    aria-current="page"
    class="flex-1 flex flex-col items-center justify-center
           h-16 gap-1 text-[#804604] select-none">
    <span class="flex items-center justify-center
                  w-10 h-7 rounded-full bg-[#e9e0d2]">
      <i class="ti ti-briefcase text-xl" aria-hidden="true"></i>
    </span>
    <span class="text-[10px] font-semibold leading-none tracking-wide">
      Work Orders
    </span>
  </a>

  <!-- Default tab -->
  <a
    href="/customers"
    class="flex-1 flex flex-col items-center justify-center
           h-16 gap-1 text-slate-400 select-none">
    <span class="flex items-center justify-center w-10 h-7">
      <i class="ti ti-users text-xl" aria-hidden="true"></i>
    </span>
    <span class="text-[10px] font-semibold leading-none tracking-wide">
      Customers
    </span>
  </a>

  <!-- Default tab -->
  <a
    href="/schedule"
    class="flex-1 flex flex-col items-center justify-center
           h-16 gap-1 text-slate-400 select-none">
    <span class="flex items-center justify-center w-10 h-7">
      <i class="ti ti-calendar text-xl" aria-hidden="true"></i>
    </span>
    <span class="text-[10px] font-semibold leading-none tracking-wide">
      Schedule
    </span>
  </a>

  <!-- Default tab -->
  <a
    href="/assets"
    class="flex-1 flex flex-col items-center justify-center
           h-16 gap-1 text-slate-400 select-none">
    <span class="flex items-center justify-center w-10 h-7">
      <i class="ti ti-map-pin text-xl" aria-hidden="true"></i>
    </span>
    <span class="text-[10px] font-semibold leading-none tracking-wide">
      Assets
    </span>
  </a>

</nav>


<!-- Five-tabs-with-badge variant -->
<!-- Same nav shell; one tab carries a badge overlay -->
<nav
  role="navigation"
  aria-label="Main navigation"
  class="fixed bottom-0 left-0 right-0 z-50
         bg-white border-t border-border
         pb-[env(safe-area-inset-bottom)]
         flex">

  <!-- ... other tabs ... -->

  <!-- Tab with badge -->
  <a
    href="/notifications"
    aria-label="Notifications, 4 unread"
    class="flex-1 flex flex-col items-center justify-center
           h-16 gap-1 text-slate-400 select-none relative">
    <span class="relative flex items-center justify-center w-10 h-7">
      <i class="ti ti-bell text-xl" aria-hidden="true"></i>
      <!-- Badge: visible count up to 99, "99+" beyond -->
      <span
        aria-hidden="true"
        class="absolute -top-1 -right-0.5
               min-w-[16px] h-4 px-1
               bg-red-500 text-white
               text-[9px] font-bold leading-none
               rounded-full flex items-center justify-center
               font-variant-numeric tabular-nums">
        4
      </span>
    </span>
    <span class="text-[10px] font-semibold leading-none tracking-wide">
      Alerts
    </span>
  </a>

</nav>
```

## Dos & Don'ts

### Do

- Use Tabler Icons (`ti ti-*`) at `text-xl` uniformly across all tabs so icon weight stays consistent at every screen density.
- Apply the active state token (`bg-[#e9e0d2]` pill, `text-[#804604]`) to exactly one tab at a time, matching the current top-level route.
- Include `pb-[env(safe-area-inset-bottom)]` on the `<nav>` element so the bar clears the home indicator on iOS and the gesture bar on Android.
- Give each tab a minimum height of `h-16` (64 px) and use `flex-1` so touch targets scale equally across all screen widths.
- Use `aria-label` on tabs that carry a badge count to announce the unread number to screen readers (e.g., `"Notifications, 4 unread"`).

### Don't

- Do not render this component on desktop viewports — it conflicts with the Sidebar Nav's left-column layout and wastes screen real estate that the sidebar already covers.
- Do not rely on `:hover` states to reveal labels or actions; touch devices have no hover event and the label must always be visible.
- Do not place more than five tabs in the strip; at six or more, the tap targets fall below 44 px on typical phone widths and become unreliable for one-handed use.
- Do not use custom active-state colors other than the design token pair `#e9e0d2` / `#804604` — diverging breaks brand consistency across the app shell.
- Do not abbreviate labels to a single character; two-character labels are the minimum for legibility and safe localization into wider-script languages.

## Patterns & Rules

1. **Single active tab** — Only one tab may carry the active pill background (`bg-[#e9e0d2]`) and text color (`text-[#804604]`) at any time; this must be updated on every navigation event that changes the top-level route, including browser back/forward navigation.
2. **Safe-area inset on every bottom overlay** — The `<nav>` element uses `pb-[env(safe-area-inset-bottom)]` directly; do not wrap it in an additional container that also applies bottom padding, or the inset will double and the bar will sit too high on notched devices.
3. **Active pill is pill-shaped, not full-width** — The active background is applied to the icon container (`w-10 h-7 rounded-full`), not the entire tab column. This mirrors the Android Material 3 navigation rail convention and keeps the strip visually light.
4. **Badge numeric cap** — Badge counts display the raw number up to 99; values of 100 or more must display as `99+` to prevent the badge from widening beyond its pill bounds. The badge uses `font-variant-numeric: tabular-nums` so the layout does not shift as the count changes.
5. **Content scroll clearance** — Page content must include `pb-[calc(4rem+env(safe-area-inset-bottom))]` (or equivalent) on its scroll container so the last item in a list is never permanently hidden behind the fixed navigation bar.

## Accessibility

- The wrapping element must be a `<nav>` with `aria-label="Main navigation"` to distinguish it from other navigation landmarks on the page (e.g., Details Sidebar Nav on a record view).
- The currently active tab must carry `aria-current="page"` so screen readers announce the user's location without requiring visual inspection of the active state color.
- Tabs with a badge count must include an explicit `aria-label` on the `<a>` element that includes the count (e.g., `"Notifications, 4 unread"`); the badge `<span>` itself must have `aria-hidden="true"` to avoid double-announcing.
- All icon elements must carry `aria-hidden="true"` since the visible label and the `aria-label`/`aria-current` on the anchor provide the accessible name; the icon is purely decorative.
- Keyboard focus must be visible on each tab; do not suppress the default browser outline. Supplement it with the design system's focus ring (`ring-2 ring-offset-2 ring-[#2D5BE3]` or equivalent) if the default outline is too faint against the white background.
- The amber active token (`#804604` on `#e9e0d2`) meets a contrast ratio of approximately 4.6:1, satisfying WCAG AA for normal text; verify this ratio is maintained if the token values change.

## Related Components

- [Sidebar Nav](./sidebar-nav.md) — Desktop counterpart; vertical icon strip fixed to the left edge of the app shell. Use this instead of Bottom Navigation Bar when building for desktop or large-tablet viewports.
- [Tab Bar](./tab-bar.md) — Desktop counterpart; horizontal tab-style navigation for a flat set of destinations within a single view. The Bottom Navigation Bar replaces this component on mobile at the app-shell level.
- [Details Sidebar Nav](./details-sidebar-nav.md) — Icon strip scoped to a single entity record that switches between contextual sub-sections (attachments, activity, history). Not a replacement for bottom nav — both may coexist on a record detail screen.
