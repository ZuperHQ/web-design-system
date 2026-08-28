---
component: Tab Bar
category: Data Display
variants: [default, with-count, with-unread, disabled]
related: [sidebar-nav, details-sidebar-nav]
---

# Tab Bar

> A horizontal row of tab buttons that lets users switch between related content sections within a single view, indicating the active section with a background highlight and an animated underline indicator.

## Overview

The Tab Bar is a horizontal navigation strip rendered inside a bordered container, where each tab is a pill-shaped button with `px-3 py-1.5` padding and a `rounded-lg` shape. The active tab is distinguished by a `bg-gray-100 text-gray-800` background and a `h-0.5` underline that animates in via a CSS scale transform, giving the bar a polished, fluid feel. It sits at the top of a content area and organises related data panels — such as Overview, Work Orders, Invoices, and Notes — under a single record or page.

## When to Use

- Switching between related sub-sections of a detail page, such as the panels of a work order or customer record.
- Displaying content panels where only one section is visible at a time and the user controls which is shown.
- Surfacing a count badge on a tab to communicate pending or total items without opening the panel.
- Showing an unread indicator dot on a tab when new activity has arrived in that section.
- Providing an overflow control ("+N more") when the number of tabs exceeds the available horizontal space.

## When NOT to Use

- Top-level application navigation between distinct pages — use [Sidebar Nav](./sidebar-nav.md) instead.
- Navigating between deeply nested record sub-sections in a detail sidebar — use [Details Sidebar Nav](./details-sidebar-nav.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| Default | Plain label button; use when the tab has no additional metadata to convey. |
| With count | Appends a small bordered badge showing a numeric count; use when the total number of items in that panel is useful at a glance. |
| With unread | Appends a solid blue dot (`bg-[#0172CB]`) after the label; use to indicate new or unread activity in that panel without showing a number. |
| Disabled | Applies `opacity-50` and removes pointer interaction; use when a tab's content is unavailable in the current context. |

## HTML Structure

```html
<!-- Tab Bar wrapper — sits inside a bordered container -->
<div class="border border-border rounded-lg overflow-hidden">
  <div class="relative pl-2 pr-4">
    <div class="flex items-center gap-x-1 group">

      <!-- Scrollable nav area -->
      <div class="pt-2 flex-1 overflow-hidden">
        <nav class="flex items-center gap-x-2 overflow-hidden">

          <!-- Active tab -->
          <button class="bg-gray-100 text-gray-800 after:scale-x-100 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]">
            Overview
          </button>

          <!-- Default (inactive) tab -->
          <button class="text-gray-500 after:scale-x-0 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]">
            Work Orders
          </button>

          <!-- Tab with count badge -->
          <button class="text-gray-500 after:scale-x-0 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]">
            Invoices
            <span class="leading-tight px-1 py-0.5 flex items-center gap-x-1.5 text-sm border font-medium bg-gray-100 text-gray-600 rounded-lg">8</span>
          </button>

          <!-- Tab with unread dot -->
          <button class="text-gray-500 after:scale-x-0 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]">
            Notes
            <div class="w-2 h-2 bg-[#0172CB] rounded-full inline-block"></div>
          </button>

          <!-- Disabled tab -->
          <button disabled class="text-gray-500 after:scale-x-0 opacity-50 flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300">
            History
          </button>

          <!-- Overflow control (shown when tabs are clipped) -->
          <button class="text-gray-500 after:scale-x-0 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-1.5 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300">
            <span>+2 more</span>
            <i class="ti ti-chevron-down text-sm leading-none"></i>
          </button>

        </nav>
      </div>

      <!-- Customize button (optional) -->
      <button class="flex-shrink-0 p-1 flex items-center justify-center border border-border rounded-lg text-gray-500 hover:text-gray-800 hover:bg-gray-100 cursor-pointer">
        <i class="ti ti-settings"></i>
      </button>

    </div>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Apply `after:scale-x-100` and `bg-gray-100 text-gray-800` together on the active tab so both the background highlight and underline indicator are always in sync.
- Use `flex-shrink-0` on every tab button to prevent labels from truncating when horizontal space is tight — rely on the overflow "+N more" control instead.
- Show the count badge only when the number is meaningful and current; keep the badge value up to date as the underlying data changes.
- Keep tab labels short (one or two words) so the bar fits within common viewport widths without overflow triggering too early.
- Place the customize (`ti-settings`) button flush to the right of the nav with `flex-shrink-0` so it is always visible regardless of how many tabs overflow.

### Don't

- Do not mix count badges and unread dots on the same tab — pick whichever communicates the relevant state, as combining them creates visual clutter.
- Do not remove the `after:*` pseudo-element classes from inactive tabs — the `after:scale-x-0` class is required so the underline is ready to animate in on activation.
- Do not use the Tab Bar for top-level page routing — navigating away from the current page breaks the contextual nature of the component and should use [Sidebar Nav](./sidebar-nav.md) instead.
- Do not add icons inside the label text of tabs — the design system reserves icon slots for the count badge and unread dot only; icons in label position are not a defined pattern.
- Do not set a fixed width on the nav container; the `flex-1 overflow-hidden` pattern is required so that the overflow button receives remaining space correctly.

## Patterns & Rules

1. **Underline animation** — The active underline uses a spring-like easing (`cubic-bezier(0.34,1.56,0.64,1)`) driven by toggling `after:scale-x-0` / `after:scale-x-100`; never replace this with a border-bottom or box-shadow, as the scale approach keeps the animation within the component's padding.
2. **Active state is dual-class** — An active tab always carries both `bg-gray-100 text-gray-800` (background) and `after:scale-x-100` (underline); setting only one of the two leaves the tab in a visually inconsistent intermediate state.
3. **Overflow pattern** — When rendered tabs exceed the container width, a "+N more" overflow button is appended as the last child of `<nav>`; the number N must reflect the actual count of hidden tabs and open a dropdown to reveal them.
4. **Disabled tabs** — Apply the HTML `disabled` attribute alongside the `opacity-50` class; never rely on only one of them, as the attribute blocks interaction while the class provides the visual affordance.
5. **Customize button placement** — The optional settings button lives outside the `<nav>` element, as a direct sibling of the scrollable nav wrapper, so it is never clipped by the overflow scroll container.

## Accessibility

- The `<nav>` element wrapping the tab buttons provides a landmark role; add `aria-label="Content sections"` (or a contextually specific label) so screen readers can distinguish this nav from others on the page.
- Each `<button>` receives `aria-selected="true"` when active and `aria-selected="false"` when inactive; the containing `<nav>` should carry `role="tablist"` and each button `role="tab"` to form a complete ARIA tabs pattern.
- Keyboard users navigate between tabs with the left and right arrow keys (not Tab); the Tab key should move focus out of the tab bar to the active panel below.
- Disabled tabs must include `aria-disabled="true"` in addition to the HTML `disabled` attribute so assistive technologies surface the unavailability correctly.

## Related Components

- [Sidebar Nav](./sidebar-nav.md) — Handles top-level application navigation in a vertical column; use it for routing between pages rather than between sub-sections of a single page.
- [Details Sidebar Nav](./details-sidebar-nav.md) — A vertical sibling nav pattern used inside detail sidebars; use it when sub-sections are displayed in a narrow side panel rather than across the full page width.
