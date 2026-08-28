---
title: Zuper Component Library — Usage Guide (Ported Components)
version: "1.0"
---

# Zuper Component Library — Usage Guide (Ported Components)

## Naming convention — read this first

If your port used different names or paths, the references below won't resolve as written — either re-run the port following this convention, or update this file to match your actual output.

---

## Design System Foundations

*(Tokens/utilities, not components — expect these in your ported Tailwind theme config and global CSS, not a component import.)*

- **Colors** — Use when picking a background or text token — choose by the purpose denoted by the color's label (e.g. surface tokens for page/card backgrounds, status tokens for feedback), never by a shade that just looks right.
- **Typography** — Use when setting any text size — the default body size is the base scale step; never use arbitrary bracket values, always pick the nearest token on the type scale.
- **Spacing & Icons** — Use when applying padding, margin, gap, or an icon — pick from the defined spacing scale (0.5–12) and the ported icon set instead of arbitrary pixel/rem values or a different icon library.

## Interactive

- **Button**  — Use when triggering an action, choosing the variant by context: Ghost for a field list; Small button (secondary/bordered style) for buttons inside tab-like elements; Small button (primary/filled style) for dialog or form submit actions; Standard button for the main button in a breadcrumb; Standard button (secondary/bordered style) for breadcrumb actions like 'More Actions'; and Button Group when multiple buttons must be grouped together.
- **Icon Button**  — Use when an action needs to be icon-only and compact — table rows or list items (edit, delete, overflow), or a secondary action alongside a primary labeled button — not for a page's primary call-to-action, which should use Button instead.
- **Toggle & Segment** — Use a Segmented Toggle when a tab-like structure is needed inside an existing tab, or when switching between 2–3 closely related views (e.g. 'Quotes' vs 'Invoices').
- **Text Input**  — Use when collecting freeform short text (name, email, search) that isn't limited to a fixed set of options.
- **Select / Dropdown** — Use when choosing from a fixed, known set of options (5–30 items).
- **Checkbox & Toggle** — Use a checkbox when the user must make multiple independent selections before acting (e.g. bulk-select in a table). Use a toggle when a single setting applies immediately without a save action.

## Form & Layout

- **Form Layout** — Use when laying out multiple fields on a create/edit form needing consistent spacing, row grouping (e.g. City/State/ZIP), or inline validation placement. Use the narrow layout when the page is already a three-pane layout; use the wide layout otherwise.
- **Expansion Panel** — Use this for showing associated record data. Use when grouped metadata or settings should stay collapsed by default so the primary view isn't cluttered, but remain reachable in one click.

## Data Display

- **Badges & Tags** — Use a Status/Priority badge for showing status or priority. Use a Count badge for showing a numeric count. Use a Tag/Chip for showing tag-like categorical data.
- **Cards** — Use a plain Card for a single named field + value inside a detail panel (e.g. Scheduled Date, Job Value), a Record Card for a compact customer/company summary, or an Address Card for service/billing address with an inline map preview.
- **Tables** — Use when listing operational records (work orders, invoices, customers) that need side-by-side field comparison, sortable columns, or bulk row selection via checkboxes.
- **Stats Cards** — Use when showing KPI totals/aggregates above a list, especially when each tile should double as a clickable filter.
- **Tab Bar** — Use when switching between related sub-sections of a detail page (e.g. panels of a work order or customer record), where only one section is visible at a time — optionally with a count badge for pending/total items, an unread dot for new activity, or a '+N more' overflow control when tabs exceed the available width.
- **Sidebar Nav** — Use when the app has 5–8 persistent top-level destinations on desktop that must always stay reachable. Use the thin variant (icon-only) when icons are self-explanatory; use the compact variant (icon + label) when users are less familiar with the icon set.

## Navigation & Filtering

- **Breadcrumb** — Shows the current navigation path and gives a one-click way back to a parent entity.
- **Toolbar Row** — Use when a table/list/kanban view needs search, pinned filter chips, and a view-mode switcher combined above it.
- **Filter Chips** — Use when a fixed, known set of filters should stay visible and individually clearable without opening a filter panel.
- **Search Input** — Use when filtering a data table, list, or kanban board by keyword within a single module's toolbar (Jobs, Work Orders, Assets) — not for global, cross-module search, which needs a dedicated search overlay instead.

## Overlay

- **Dropdown Menu** — Use to present a set of record actions (Edit, View, Export, Delete) from a row-level overflow button, navigation shortcuts from a single 'New' trigger, or the 'More Actions' menu in a breadcrumb — group destructive actions apart with a divider, and use this instead of 4+ inline icon buttons when space is constrained.
- **Modal / Dialog** — Use to confirm a destructive/irreversible action (delete, close), collect a short 2–4 field inline form (rename, edit description), surface a time-sensitive alert (session expiry), or block navigation until the user makes an explicit binary choice.
- **Drawer Panel** — Use to preview a record selected from a list/table while keeping that list visible in the background, to navigate between related records with prev/next controls, or to show a child entity reached via a breadcrumb trail — without committing to a full-page navigation.

## Feedback & Content

- **Loading Shimmer** — Use when a table, card grid, or detail drawer/panel is fetching data with a known layout; the shimmer reserves the exact space real content will occupy to avoid layout shift.
- **Empty States** — Use the no-data variant when a table/panel has zero records yet (pair with a 'Create' action), or the no-results variant when a search/filter returns zero matches (pair with 'Clear filters' or 'Try different keywords') — never leave blank space where content is expected.
- **Toast / Snackbar** — Use Toast for a one-line success/error confirmation after a background operation, async error, or any API request — without blocking the page. Use Snackbar specifically for the bulk-action bar when one or more table/list rows are selected (assign, export, delete).

## Application Layouts

- **Kanban Column** — Use to group jobs/work orders/tasks by workflow status into drag-and-drop lanes (e.g. Scheduled, In Progress, Completed).
- **Details Left Panel** — Use as the left column of a record detail page to show identity, lifecycle status, quick actions (status change, schedule, email, call, note), and structured fields grouped into expandable accordion sections — also applicable for any field-list groupings more generally.
- **Details Right Sidebar Nav** — Use on a record detail page's right edge to switch between contextual sub-panels (attachments, activity, status history, assignments) without stacking them in one scroll column — always collapsed by default, with a Customize control for reordering/visibility. This is a quick-jump aid for scrollable panel content only, not a substitute for Tab Bar.
- **Details Center Panel** — Use as the tabbed centre column of a record detail page — Highlights (summary cards), related record tables, Description, and Activity — when the record has multiple distinct content domains that benefit from top-level tab switching rather than one long scroll.
- **Full Details Page Layout** — Assemble it from the three composable pieces: Details Left Panel for identity, Details Center Panel for tabbed content, and Details Right Sidebar Nav for contextual panels.
- **Filter Panel** — Use it when list filtering needs multiple simultaneous conditions, or when the field set is too large for inline Filter Chips or a plain Search Input to handle.
- **Reorderable List** — Use to let users drag-reorder or show/hide a small (3–12) set of named items — customizing tab order, toggling panel visibility, or setting sort-criteria priority — inside a 'Customize' panel where the preference must persist across sessions.

---

## General Patterns

1. **Breadcrumb on every page** — Every new page must render `<Breadcrumb />` component.
2. **Table is the only table** — Use the ported `Table` component app-wide; pair bulk row selection with `Snackbar` for bulk-action controls.
3. **DrawerPanel for record detail viewing** — Any record detail viewing from any page should use `<DrawerPanel />`.
4. **Shimmer only, never a spinner** — Any loading state must render `<Shimmer />`.
5. **DetailsPageLayout is definitive** — It is the definitive layout for any record detail page.
6. **FilterPanel is the standard filtering UI** — It is the standard look for any general filtering panel.
7. **`formatRecordTitle(record)`** — Returns `#<prefix (if available)><unique_id> <name_or_title>`.
   - Job → `#<prefix><work_order_number> <job_title>`
   - Quote → `#<prefix><quote_no> <quote_title>`
   - Invoice → `#<prefix><invoice_no> <invoice_title>`
   - Proposal → `#<prefix><proposal_no> <quote_title>` (there is no `proposal_title` field — reuse `quote_title`)
   - Any other record type: prefix key (if one exists) + unique ID key (e.g. work order number, invoice no) + name/title, in that order.
8. **`formatDate(date, userPreference?)`** — Use the user's preferred date format if set; otherwise default to `10 Jul 2026` (DD MMM YYYY).
9. **`formatTime(time, userPreference?)`** — Use the user's preferred 12- or 24-hour format if set; otherwise default to 12-hour format.
10. **`formatStatus(status, entityType)`** — Always render through `StatusBadge`, never custom styling. Replace underscores with spaces (e.g. `IN_PROGRESS` → `In Progress`). Exceptions: Quote `AWAIT_RESPONSE` → `SENT`; Invoice `AWAIT_PAYMENT` → `SENT`.
11. **`current_job_status`** — Use this field to show a job's status anywhere in the app; do not read status from any other field.
