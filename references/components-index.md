---
title: Zuper Component Library — Developer Reference
version: "1.0"
components: 43
---

# Zuper Component Library — Developer Reference

A framework-agnostic developer reference for 43 Zuper design system components. Each file covers when to use, HTML structure, dos & don'ts, patterns, and accessibility. Intended for internal Angular developers and external React developers building on the Zuper platform.

This file is the index of what exists and where each doc lives. For which component to reach for and why, plus app-wide UI patterns, see [usage-guide.md](./usage-guide.md). For exact markup to copy, see `src/assets/design-system/zuper-components.html`.

---

## Design System Foundations

| Component | File | Description |
|-----------|------|-------------|
| Colors | [colors.md](./colors.md) | Defines the full Zuper color palette, semantic tokens, and dark-mode surface variables. |
| Typography | [typography.md](./typography.md) | Covers type scale, font families, weight rules, and line-height guidance for all text styles. |
| Spacing & Icons | [spacing-and-icons.md](./spacing-and-icons.md) | Documents the 4 px spacing scale and the icon library sizing and usage conventions. |

## Interactive

| Component | File | Description |
|-----------|------|-------------|
| Button | [button.md](./button.md) | Primary, secondary, and destructive button variants with size and state specifications. |
| Icon Button | [icon-button.md](./icon-button.md) | Compact icon-only action trigger with tooltip requirement and accessible label rules. |
| Toggle & Segment | [toggle-and-segment.md](./toggle-and-segment.md) | Binary toggle switch and multi-option segmented control for mutually exclusive choices. |
| Text Input | [text-input.md](./text-input.md) | Single-line and multiline text fields with label, helper text, and validation state patterns. |
| Select / Dropdown | [select-dropdown.md](./select-dropdown.md) | Styled select control supporting single and multi-select with search and grouped options. |
| Checkbox & Toggle | [checkbox-and-toggle.md](./checkbox-and-toggle.md) | Checkbox for multi-select lists and inline toggle for boolean settings with indeterminate support. |

## Form & Layout

| Component | File | Description |
|-----------|------|-------------|
| Form Layout | [form-layout.md](./form-layout.md) | Grid and stacked layout containers that consistently space labels, inputs, and error messages. |
| Expansion Panel | [expansion-panel.md](./expansion-panel.md) | Collapsible accordion section for progressively disclosing grouped form fields or content. |

## Data Display

| Component | File | Description |
|-----------|------|-------------|
| Badges & Tags | [badges-and-tags.md](./badges-and-tags.md) | Small status indicators and categorical labels with semantic color and optional dismiss actions. |
| Cards | [cards.md](./cards.md) | Surface container for summarising a single entity with header, body, and action slot. |
| Tables | [tables.md](./tables.md) | Responsive data table with sortable columns, row selection, pagination, and inline actions. |
| Stats Cards | [stats-cards.md](./stats-cards.md) | KPI summary tiles showing a metric value, label, trend indicator, and optional sparkline. |
| Tab Bar | [tab-bar.md](./tab-bar.md) | Horizontal tab navigation for switching between related content panels within a page. |
| Sidebar Nav | [sidebar-nav.md](./sidebar-nav.md) | Collapsible left-side primary navigation with icon, label, and nested sub-menu support. |

## Navigation & Filtering

| Component | File | Description |
|-----------|------|-------------|
| Breadcrumb | [breadcrumb.md](./breadcrumb.md) | Hierarchical path trail showing the user's location and enabling ancestor-page navigation. |
| Toolbar Row | [toolbar-row.md](./toolbar-row.md) | Top-of-view action bar combining search, filters, bulk actions, and view-mode controls. |
| Filter Chips | [filter-chips.md](./filter-chips.md) | Dismissible inline chips that display active filter criteria with a clear-all affordance. |
| Search Input | [search-input.md](./search-input.md) | Instant-search text field with debounce, clear button, and optional scoped-search selector. |

## Overlay

| Component | File | Description |
|-----------|------|-------------|
| Dropdown Menu | [dropdown-menu.md](./dropdown-menu.md) | Contextual floating menu triggered by a button, offering a list of actions or navigation links. |
| Modal / Dialog | [modal-dialog.md](./modal-dialog.md) | Blocking overlay dialog for confirmations, forms, and critical decisions requiring user input. |
| Drawer Panel | [drawer-panel.md](./drawer-panel.md) | Slide-in side panel for detail views or secondary forms without leaving the current context. |

## Feedback & Content

| Component | File | Description |
|-----------|------|-------------|
| Loading Shimmer | [loading-shimmer.md](./loading-shimmer.md) | Skeleton placeholder animation that mimics content layout while asynchronous data loads. |
| Empty States | [empty-states.md](./empty-states.md) | Illustrated zero-data screens with a headline, description, and primary call-to-action button. |
| Toast / Snackbar | [toast-snackbar.md](./toast-snackbar.md) | Transient notification banner for success, error, warning, and informational system feedback. |

## Application Layouts

| Component | File | Description |
|-----------|------|-------------|
| Kanban Column | [kanban-column.md](./kanban-column.md) | Vertical swimlane for drag-and-drop card management in board-style workflow views. |
| Details Left Panel | [details-left-panel.md](./details-left-panel.md) | Fixed left pane in a master-detail layout displaying entity summary and key attribute fields. |
| Details Right Sidebar Nav | [details-sidebar-nav.md](./details-sidebar-nav.md) | Collapsible right-side icon strip for switching contextual panels in a detail view; always collapsed within the Full Details Page Layout. |
| Details Center Panel | [details-center-panel.md](./details-center-panel.md) | Tabbed centre column for record detail views with Highlights, related record tables, Description, and Activity sections. |
| Full Details Page Layout | [details-page-layout.md](./details-page-layout.md) | Three-column shell composing the left panel, centre panel, and right sidebar into a complete record detail view. |
| Filter Panel | [filter-panel.md](./filter-panel.md) | Persistent side panel housing multi-facet filter controls for list and table views. |
| Reorderable List | [reorderable-list.md](./reorderable-list.md) | Drag-and-drop sortable list for user-defined ordering of items with keyboard accessibility support. |

## Mobile

Mobile-specific components. For shared foundations and desktop components, see the sections above. Mobile components either **replace** a desktop component with a mobile-native pattern (e.g. Bottom Sheet replaces Modal / Dialog) or **adapt** a desktop component for touch interfaces.

| Component | File | Description |
|-----------|------|-------------|
| Bottom Sheet | [bottom-sheet.md](./bottom-sheet.md) | Full-width overlay anchored to screen bottom; replaces centered modal on mobile. |
| Confirmation Bottom Sheet | [confirmation-bottom-sheet.md](./confirmation-bottom-sheet.md) | Bottom-anchored confirmation overlay using the amber/red/blue severity system. |
| Action Sheet | [action-sheet.md](./action-sheet.md) | Full-width grouped action list at screen bottom; replaces dropdown menus on mobile. |
| Bottom Navigation Bar | [mobile-nav-bar.md](./mobile-nav-bar.md) | Fixed bottom navigation with icon and label tabs; replaces sidebar and top tab nav. |
| Mobile Card | [mobile-card.md](./mobile-card.md) | Full-width card with always-visible action strip; touch-optimized version of Cards. |
| Mobile Button | [mobile-button.md](./mobile-button.md) | Full-width 44px button for mobile; adapts the desktop Button for touch contexts. |
| Mobile Text Input | [mobile-text-input.md](./mobile-text-input.md) | 48px input preventing iOS auto-zoom; adapts Text Input for mobile forms. |
| Mobile Search Bar | [mobile-search-bar.md](./mobile-search-bar.md) | Sticky top search bar with filter icon; simplified mobile version of Toolbar Row. |
| Mobile Filter Chips | [mobile-filter-chips.md](./mobile-filter-chips.md) | Horizontal scroll chip row; adapts Filter Chips for mobile with scroll-snap. |
