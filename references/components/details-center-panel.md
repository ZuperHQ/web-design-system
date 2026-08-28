---
component: Details Center Panel
category: Application Layouts
variants: [loaded, loading]
related: [details-left-panel, details-right-sidebar-nav, details-page-layout, tab-bar]
---

# Details Center Panel

> The main content column of a record detail view, combining a sticky tab bar with a scrollable structured content area containing Highlights, related record tables, Description, and Activity sections.

## Overview

The Details Center Panel is a `flex-col` container that anchors the centre of a record detail view. A sticky tab bar at the top (`flex-shrink-0`) allows navigation between Overview, Tasks, Notes, Activity, Gallery, Financials, and other tabs. Below it, a scrollable content area (`bg-theme-light flex-1 overflow-y-auto p-4`) holds structured section cards — Highlights summary cards, Jobs table, Description, Activity feed, and more. In the standalone design-system demo the panel sits in a fixed-size container (`44rem × 580px`); in the full details page layout it stretches to `flex-1 min-w-0` to fill the space between the left panel and right sidebar.

## When to Use

- On record detail pages (work orders, customers, properties, invoices) where the primary content requires tabbed navigation plus a structured overview with summary cards, related record tables, and activity feeds.
- When the record has multiple distinct content domains (financials, tasks, notes, activity) that benefit from top-level tab switching rather than stacking everything in a single scroll column.
- As the centre column in the Full Details Page Layout between the Details Left Panel and the Details Right Sidebar Nav.

## When NOT to Use

- For simple key-value field panels — use the [Details Left Panel](./details-left-panel.md) instead.
- For primary application navigation between pages or app sections — use [Sidebar Nav](./sidebar-nav.md) instead.
- Inside a modal or drawer where a flat [Tab Bar](./tab-bar.md) is sufficient without the full panel structure.

## Variants

| Variant | Description |
|---------|-------------|
| loaded | Tab bar with active/inactive tabs plus content area containing Highlights cards, Jobs table, Description card, and Activity feed. Use as the default state once data has resolved. |
| loading | Same structural shape as the loaded variant with `animate-pulse` gray placeholder blocks replacing all content. Show while data is fetching to prevent layout shift. |

## HTML Structure

```html
<!-- Standalone: fixed size container -->
<div class="flex flex-col overflow-hidden border border-gray-200 rounded-lg" style="width:44rem;height:580px">
  <!-- In full layout use: class="flex-1 min-w-0 flex flex-col overflow-hidden" (no fixed width/height) -->

  <!-- Tab bar: flex-shrink-0 keeps it outside the scroll container -->
  <div class="bg-white border-b border-gray-200 flex-shrink-0">
    <div class="relative pl-2 pr-4">
      <div class="flex items-center gap-x-1 group">
        <div class="pt-2 flex-1 overflow-hidden">
          <nav class="flex items-center gap-x-2 overflow-hidden">

            <!-- Active tab -->
            <button type="button"
              class="bg-gray-100 text-gray-800 after:scale-x-100 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]"
              aria-selected="true">Overview</button>

            <!-- Inactive tab -->
            <button type="button"
              class="text-gray-500 after:scale-x-0 cursor-pointer flex-shrink-0 px-3 py-1.5 mb-2 relative inline-flex justify-center items-center gap-x-2 hover:bg-gray-100 hover:text-gray-800 text-base font-medium rounded-lg after:absolute after:-bottom-2 after:inset-x-2 after:h-0.5 after:bg-gray-800 after:origin-center after:transform after:transition-transform after:duration-300 after:ease-[cubic-bezier(0.34,1.56,0.64,1)]"
              aria-selected="false">Tasks</button>

            <!-- … additional inactive tabs (Notes, Activity, Gallery, Financials) … -->

          </nav>
        </div>
      </div>
    </div>
  </div>

  <!-- Scrollable content area -->
  <div class="flex-1 overflow-y-auto p-4 bg-theme-light space-y-6">

    <!-- Highlights section -->
    <div class="space-y-2">
      <h6 class="p-1.5 flex items-center gap-1.5 text-lg font-medium leading-tight text-gray-700">
        <i class="ti ti-chart-bar"></i> Highlights
      </h6>
      <div class="flex flex-wrap gap-3">

        <!-- Summary card -->
        <div class="rounded-lg border border-border bg-white p-2.5 flex flex-col space-y-2 w-50 h-fit">
          <div class="flex items-center space-x-1 min-w-0">
            <i class="ti ti-receipt text-gray-500 text-lg flex-shrink-0"></i>
            <span class="text-md text-gray-500 leading-tight truncate">Accounts Receivables</span>
          </div>
          <span class="text-lg font-medium text-gray-800 leading-tight font-mono">$1,234.00</span>
        </div>

        <!-- … additional summary cards … -->

      </div>
    </div>

    <!-- Static section header (no navigation) -->
    <div class="space-y-2">
      <h6 class="p-1.5 flex items-center gap-1.5 text-lg font-medium leading-tight text-gray-700">
        <i class="ti ti-briefcase"></i>
        Jobs
        <!-- Count badge -->
        <span class="leading-tight px-1 py-0.5 flex items-center text-sm border font-medium bg-gray-100 text-gray-600 rounded-lg">3</span>
      </h6>
      <div data-slot="card" class="flex flex-col items-stretch text-card-foreground rounded-xl bg-white border border-border shadow-none">
        <div data-slot="card-content" class="grow">
          <!-- Table or list content -->
        </div>
      </div>
    </div>

    <!-- Navigate-on-click section header -->
    <div class="space-y-2">
      <button type="button" class="group/sec p-1.5 flex items-center gap-1.5 text-lg font-medium leading-tight transition-colors rounded-lg cursor-pointer hover:bg-gray-100 hover:text-gray-800 text-gray-700">
        <i class="ti ti-activity"></i>
        Activity
        <i class="ti ti-chevron-right text-lg transition-transform duration-200 ease-in-out group-hover/sec:translate-x-0.5"></i>
      </button>
      <div data-slot="card" class="flex flex-col items-stretch text-card-foreground rounded-xl bg-white border border-border shadow-none">
        <div data-slot="card-content" class="grow">
          <!-- Activity items (avatar + text rows) -->
        </div>
      </div>
    </div>

    <!-- Address section: Service/Pickup Address + Billing Address + map preview -->
    <div class="space-y-2 group/addr">
      <div class="p-1.5 flex items-center gap-1.5 text-lg font-medium leading-tight text-gray-700">
        <i class="ti ti-current-location"></i>
        Address
        <span class="inline-flex items-center space-x-3 invisible opacity-0 group-hover/addr:visible group-hover/addr:opacity-100 transition-opacity duration-150">
          <button type="button" class="p-1 flex items-center justify-center border border-border rounded-lg transition-colors duration-200 cursor-pointer text-gray-500 hover:text-gray-800 hover:bg-gray-100 bg-white" title="Edit">
            <i class="ti ti-pencil"></i>
          </button>
        </span>
      </div>
      <div data-slot="card" class="flex items-stretch text-card-foreground rounded-xl bg-white border border-border shadow-none overflow-hidden">
        <!-- Addresses -->
        <div class="flex-1 p-4 min-w-0">
          <div class="grid grid-cols-2 space-x-2">
            <!-- Service / Pickup Address -->
            <div class="flex flex-col space-y-1.5">
              <p class="text-base leading-tight text-gray-500">Service Address</p>
              <div class="flex flex-col space-y-1">
                <div class="flex items-center space-x-1.5">
                  <p class="text-base text-gray-600 truncate leading-tight">John Doe</p>
                  <div class="flex items-center space-x-1.5">
                    <a class="cursor-pointer rounded-full flex items-center hover:text-gray-600 text-gray-500" href="tel:9998887776"><i class="ti ti-phone text-base leading-none"></i></a>
                    <a class="rounded-full text-gray-500 flex items-center hover:text-gray-600" href="mailto:john@example.com"><i class="ti ti-mail text-base leading-none"></i></a>
                  </div>
                </div>
                <p class="text-base text-gray-600 leading-relaxed">5/347, Ambedkar Main Rd,<br>Chennai, Tamil Nadu — 600096<br>IN</p>
              </div>
            </div>
            <!-- Billing Address -->
            <div class="flex flex-col space-y-1.5">
              <p class="text-base leading-tight text-gray-500">Billing Address</p>
              <p class="text-base text-gray-600 leading-relaxed">4/605, VOC St, Rajiv Gandhi Salai,<br>Chennai, Tamil Nadu — 600096<br>IN</p>
            </div>
          </div>
          <!-- Maps link -->
          <div class="mt-1.5">
            <a class="inline-flex items-center gap-1.5 px-1.5 py-1 text-base border border-border rounded-lg text-gray-500 hover:text-gray-600 transition-colors cursor-pointer">
              <i class="ti ti-external-link text-base"></i>
              <span class="leading-tight">Maps</span>
            </a>
          </div>
        </div>
        <!-- Map preview (right, 2/5 width) -->
        <div class="w-2/5 flex-shrink-0 relative overflow-hidden rounded-r-xl group/map bg-gray-100">
          <div class="absolute inset-0 z-10 pointer-events-none flex items-center justify-center">
            <i class="ti ti-map-pin-share text-2xl text-gray-500 p-2 bg-white rounded-full opacity-0 scale-75 group-hover/map:opacity-100 group-hover/map:scale-100 transition-all duration-200 ease-out"></i>
          </div>
          <div class="absolute inset-0 transition-opacity duration-200 group-hover/map:opacity-30 bg-white opacity-0"></div>
          <!-- Real usage: <location-preview [options]="mapOptions"></location-preview> in place of the placeholder icon -->
          <div class="w-full h-full flex items-center justify-center text-gray-300"><i class="ti ti-map-2 text-4xl"></i></div>
          <div class="absolute top-0 left-0 bottom-0 w-12 pointer-events-none" style="background: linear-gradient(to right, #FFFFFF 15%, transparent 100%);"></div>
        </div>
      </div>
    </div>

  </div>

</div>

<!-- Loading variant: same shell with animate-pulse placeholder blocks -->
<!--
<div class="flex flex-col overflow-hidden border border-gray-200 rounded-lg" style="width:34rem;height:580px">
  <div class="bg-white border-b border-gray-200 flex-shrink-0 px-3 py-2">
    <div class="flex items-center gap-x-2">
      <div class="h-7 w-20 bg-gray-200 rounded-lg animate-pulse"></div>
      <div class="h-7 w-14 bg-gray-200 rounded-lg animate-pulse"></div>
      <div class="h-7 w-16 bg-gray-200 rounded-lg animate-pulse"></div>
    </div>
  </div>
  <div class="flex-1 overflow-y-auto p-4 bg-theme-light space-y-6">
    <div class="space-y-2">
      <div class="h-6 w-28 bg-gray-200 rounded animate-pulse"></div>
      <div class="flex flex-wrap gap-3">
        <div class="h-16 w-50 bg-gray-200 rounded-lg animate-pulse"></div>
        <div class="h-16 w-50 bg-gray-200 rounded-lg animate-pulse"></div>
        <div class="h-16 w-50 bg-gray-200 rounded-lg animate-pulse"></div>
      </div>
    </div>
    <div class="space-y-2">
      <div class="h-6 w-24 bg-gray-200 rounded animate-pulse"></div>
      <div class="rounded-xl border border-border bg-white p-3">
        <div class="grid grid-cols-12 gap-4">
          <div class="col-span-3 h-4 bg-gray-200 rounded animate-pulse"></div>
          <div class="col-span-4 h-4 bg-gray-200 rounded animate-pulse"></div>
          <div class="col-span-3 h-4 bg-gray-200 rounded animate-pulse"></div>
          <div class="col-span-2 h-4 bg-gray-200 rounded animate-pulse"></div>
        </div>
      </div>
    </div>
  </div>
</div>
-->
```

## Dos & Don'ts

### Do

- Use `flex-shrink-0` on the tab bar wrapper so it never scrolls away as the user scrolls the content area.
- Apply `bg-theme-light` as the content area background (`flex-1 overflow-y-auto p-4 bg-theme-light space-y-6`).
- Use `w-50 h-fit` for Highlights summary cards and `font-mono` for currency values inside them.
- Use the `data-slot="card"` + `data-slot="card-content"` card pattern for all section content containers.
- In the full layout, use `class="flex-1 min-w-0 flex flex-col overflow-hidden"` instead of a fixed width/height container so the panel fills the remaining space.
- Use navigate-on-click `<button>` section headers (with `ti-chevron-right` that translates on hover) for sections that link to a dedicated tab or sub-page.
- If a center panel tab must display record fields, wrap them in a `rounded-lg border border-border` card and render each field as a vertical stack — label (`text-sm text-gray-500`) on top, value (`text-base text-gray-800`) below — using `flex flex-col gap-0.5` per field row.
- Name the first/default tab "Overview" (not "Details" or "Primary Details") when it hosts an Address section, Highlights, or other summary content that supplements — rather than repeats — the left panel.
- Render addresses with the Address section pattern: `group/addr` wrapper, `data-slot="card"` body split into a `flex-1 p-4` text column (Service/Pickup Address + Billing Address in a `grid grid-cols-2`) and a `w-2/5` map preview using `<location-preview [options]="mapOptions">`, matching [job-details.component.html](../../src/app/modules/jobs/job-details/job-details.component.html)'s `ADDRESS` section.

### Don't

- Never hard-code the panel width in the full layout — `flex-1 min-w-0` lets it fill the remaining space between the left panel and right sidebar.
- Never put the tab bar inside the scrollable content area — it must be a `flex-shrink-0` sibling outside the scroll container.
- Do not use `animate-shimmer` for the loading variant; use `animate-pulse` with `bg-gray-200` placeholder blocks that mirror the loaded section hierarchy.
- Do not use raw `div` with manual border and padding in place of the `data-slot="card"` / `data-slot="card-content"` pattern for section content.
- Never display key-value record fields in the center panel without enclosing them in a `rounded-lg border border-border` card. Do not use the left panel's `grid-cols-5` side-by-side label/value grid here.
- Do not render naked field rows (label beside value) directly in the content area — they must always be inside a card container with a `rounded-lg` border.
- **Never add a "Primary Details" tab that re-lists fields already surfaced in the Details Left Panel's `primaryInfo` accordion.** The left panel is the single source of truth for record fields; a duplicate center-panel tab creates two places to keep in sync and confuses editors about which one is authoritative. If the center panel needs a landing tab, call it "Overview" and populate it only with content the left panel doesn't show (Address, Highlights, related-record tables, Description, Activity).
- Do not hand-roll address markup (custom map overlays, `absolute inset-0` background maps, ad-hoc `<h2>`/`<p>` address blocks). Always use the Address section pattern above with `<location-preview>` for the map.

## Patterns & Rules

1. **Fields belong in the left panel** — Record key-value fields are the exclusive domain of the [Details Left Panel](./details-left-panel.md). Never create a "Primary Details"/"Details" tab whose sole purpose is to re-list those same fields in the center panel. Only surface fields in the center panel when a tab is explicitly dedicated to field data the left panel doesn't already show (e.g., "Specifications"). In that case, follow the card + vertical-stack rule below. The default/first tab should be named "Overview" and hold non-duplicative content (Address, Highlights, related-record tables, Description, Activity).
2. **Field display in the center panel** — When a center panel tab must show record fields, enclose the entire field group in a `data-slot="card"` container (`rounded-lg border border-border bg-white`). Each field renders as a `flex flex-col gap-0.5`: label `<span class="text-sm text-gray-500">` above, value `<span class="text-base text-gray-800">` below. Never use the left panel's `grid-cols-5` side-by-side layout here.
3. **Tab underline indicator** — The active tab uses `after:scale-x-100` and the inactive tab uses `after:scale-x-0` on the `after:` pseudo-element (`after:h-0.5 after:bg-gray-800 after:inset-x-2 after:-bottom-2`). Toggle only these two scale classes and `aria-selected`; never swap the full class string.
2. **Section header types** — Static section headers (Highlights, Jobs, Description) use `<h6>` with `p-1.5 flex items-center gap-1.5 text-lg font-medium leading-tight text-gray-700`. Navigate-on-click section headers (Activity, Tasks) use `<button>` with the same base classes plus `hover:bg-gray-100 rounded-lg` and a `ti-chevron-right` that translates `0.5` on `group-hover`.
3. **Count badge** — When a section has a known record count, append a badge immediately after the section title: `<span class="leading-tight px-1 py-0.5 flex items-center text-sm border font-medium bg-gray-100 text-gray-600 rounded-lg">3</span>`.
4. **Shimmer structure mirrors loaded structure** — The loading variant must mirror the same section hierarchy (tab bar, Highlights row, section cards) so the layout does not shift when data arrives. Use `grid grid-cols-12 gap-4` col-span blocks for table-row shimmer.
5. **Card pattern** — All section content uses `data-slot="card"` on the outer div and `data-slot="card-content"` on the inner div. Never use a raw `div` with manual border and padding in place of this pattern.
6. **Address section** — Wrap in `group/addr`; body is `data-slot="card"` split into a `flex-1 p-4` column (`grid grid-cols-2` for Service/Pickup + Billing Address, each a `flex flex-col space-y-1.5`) and a `w-2/5 flex-shrink-0` map column using `<location-preview [options]="mapOptions">` inside a `group/map` hover overlay. Add the edit button only inside the `group-hover/addr:visible` span, same as the section header pattern. Never hand-build the map with custom `absolute inset-0` background images or inline SVG pins in place of `<location-preview>`.

## Accessibility

- Tab buttons must have visible focus styles and carry `aria-selected="true"` on the active tab and `aria-selected="false"` on inactive tabs.
- Section headers that are `<button>` elements need a descriptive `aria-label` when the icon and visible text alone are ambiguous.
- Avatar initials in the Activity feed need `aria-label` on the avatar container so screen readers announce the author rather than a single letter.
- The loading variant's container should carry `aria-busy="true"` and individual shimmer blocks should carry `aria-hidden="true"` to prevent screen readers from enumerating empty placeholders.

## Related Components

- [Details Left Panel](./details-left-panel.md) — The fixed-width left column that provides record identity, status, and field data alongside this component.
- [Details Right Sidebar Nav](./details-sidebar-nav.md) — The collapsible right icon strip that sits to the right of this panel in the full details layout.
- [Full Details Page Layout](./details-page-layout.md) — The three-column shell that composes this panel with the left panel and right sidebar into a complete record detail view.
- [Tab Bar](./tab-bar.md) — The standalone tab navigation primitive; the tab bar inside this component follows the same active/inactive class conventions.
