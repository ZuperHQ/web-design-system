---
component: Dropdown Menu
category: Overlay
variants: [single-group, multiple-groups]
related: [select-dropdown, modal-dialog]
---

# Dropdown Menu

> A contextual overlay panel that surfaces a list of actions or navigation items anchored to a trigger element, allowing users to act on a record without navigating away.

## Overview

The Dropdown Menu is a floating panel with a white background, subtle border (`border-gray-200`), rounded corners (`rounded-lg`), and a drop shadow (`shadow-lg`). It renders action buttons stacked vertically inside one or more logical groups separated by a `divide-y divide-gray-100` divider, making it the primary component for contextual, trigger-anchored command lists in the Zuper design system.

## When to Use

- Presenting a set of actions for a specific record (e.g., Edit, View, Export, Delete) from a row-level overflow button.
- Offering navigation shortcuts to related entity types (e.g., create a new Project, Job, Quote, or Invoice) from a single "New" trigger.
- Grouping destructive actions (e.g., Delete) away from safe actions using a divider so the visual separation communicates risk.
- Replacing a set of inline icon buttons when there are four or more actions and screen space is constrained.

## When NOT to Use

- When the user must pick a value to populate a form field — use [Select Dropdown](./select-dropdown.md) instead, which provides proper form binding and selection state.
- When the interaction requires a title, rich body content, or a confirmation prompt — use [Modal / Dialog](./modal-dialog.md) instead, which keeps the user focused on a single decision.

## Variants

| Variant | Description |
|---------|-------------|
| single-group | All actions belong to one logical category; use this when every item carries equal weight and no action is destructive. |
| multiple-groups | Actions are split into two or more groups separated by a `divide-y divide-gray-100` divider; use this when at least one group contains a destructive or irreversible action that must be visually isolated. |

## HTML Structure

```html
<!-- Trigger button is not part of the menu itself; position the menu with CSS relative to the trigger. -->

<!-- Single group -->
<div class="select-none min-w-44 bg-white border border-gray-200 rounded-lg shadow-lg p-1 divide-y divide-gray-100">
  <div class="py-1 first:pt-0 last:pb-0 space-y-1">
    <button type="button" class="flex gap-2 items-center hover:bg-gray-100 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-gray-600 text-xl ti ti-clipboard-check"></i>
      <span class="truncate text-base leading-tight">Project</span>
    </button>
    <button type="button" class="flex gap-2 items-center hover:bg-gray-100 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-gray-600 text-xl ti ti-briefcase"></i>
      <span class="truncate text-base leading-tight">Job</span>
    </button>
  </div>
</div>

<!-- Multiple groups (with divider) — active/selected item uses bg-gray-100 and a check icon -->
<div class="select-none min-w-44 bg-white border border-gray-200 rounded-lg shadow-lg p-1 divide-y divide-gray-100">
  <div class="py-1 first:pt-0 last:pb-0 space-y-1">
    <button type="button" class="flex gap-2 items-center hover:bg-gray-100 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-gray-600 text-xl ti ti-edit"></i>
      <span class="truncate text-base leading-tight">Edit</span>
    </button>
    <!-- Selected state: bg-gray-100 + trailing ti-check icon -->
    <button type="button" class="flex gap-2 items-center bg-gray-100 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-gray-600 text-xl ti ti-eye"></i>
      <span class="truncate text-base leading-tight">View</span>
      <i class="ti ti-check text-gray-800 ml-auto text-base"></i>
    </button>
    <button type="button" class="flex gap-2 items-center hover:bg-gray-100 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-gray-600 text-xl ti ti-download"></i>
      <span class="truncate text-base leading-tight">Export</span>
    </button>
  </div>
  <!-- Destructive group — separate with divide-y; use red palette -->
  <div class="py-1 first:pt-0 last:pb-0 space-y-1">
    <button type="button" class="flex gap-2 items-center hover:bg-red-50 text-red-500 rounded-md w-full px-2 py-1.5 text-left cursor-pointer">
      <i class="text-xl ti ti-trash"></i>
      <span class="truncate text-base leading-tight">Delete</span>
    </button>
  </div>
</div>
```

## Dos & Don'ts

### ✅ Do

- Use `select-none` on the root container to prevent text selection when the menu opens quickly after a click-hold.
- Apply `truncate` to every label `<span>` so long action names do not overflow the `min-w-44` container.
- Place destructive actions (Delete, Archive, Remove) in their own group at the bottom, separated by the `divide-y divide-gray-100` divider.
- Mark the currently active item with `bg-gray-100` background and a trailing `ti ti-check` icon so users see the current state at a glance.
- Use Tabler icons (`ti ti-*`) sized at `text-xl text-gray-600` for all leading icons to stay consistent with the rest of the design system.

### ❌ Don't

- Do not nest a Dropdown Menu inside another Dropdown Menu — cascading menus add cognitive load and break keyboard navigation patterns.
- Do not mix form controls (checkboxes, text inputs) inside the menu panel — use a [Modal / Dialog](./modal-dialog.md) for multi-step or form-based interactions.
- Do not omit the `type="button"` attribute on menu items — without it, buttons inside a `<form>` will submit the form unexpectedly.
- Do not remove `min-w-44` or hard-code a narrow width — labels need room to breathe, and clipped text is unreadable on smaller viewports.
- Do not use the red destructive palette (`hover:bg-red-50 text-red-500`) for non-destructive actions — reserving it for irreversible operations trains users to treat red as a danger signal.

## Patterns & Rules

1. **Group isolation** — Each logical group lives in its own `<div class="py-1 first:pt-0 last:pb-0 space-y-1">` child. The `divide-y divide-gray-100` on the root container automatically renders a hairline separator between groups without extra markup.
2. **Minimum width** — The root panel carries `min-w-44` (11 rem) as the floor; it may grow wider to fit content but must never be narrower, ensuring touch targets remain comfortable.
3. **Selected state** — An active or currently-applied item replaces `hover:bg-gray-100` with a static `bg-gray-100` and appends `<i class="ti ti-check text-gray-800 ml-auto text-base">` as a trailing indicator. Only one item per group should carry this state at a time.
4. **Icon requirement** — Every menu item must include a leading Tabler icon. Icon-free items break the visual rhythm and make scanning harder when the list grows beyond five items.
5. **Positioning** — The menu panel is always rendered outside normal document flow (absolute or fixed) and anchored to its trigger. The component itself carries no positioning classes; the surrounding layout context controls placement.

## Accessibility

- The menu container should carry `role="menu"` and each action button `role="menuitem"` so screen readers announce the context correctly.
- Keyboard interaction: `Tab` or `Enter` opens the menu; `ArrowDown` / `ArrowUp` move focus between items; `Enter` or `Space` activates the focused item; `Escape` closes the menu and returns focus to the trigger.
- The trigger element must have `aria-haspopup="menu"` and `aria-expanded` toggled to `true`/`false` as the menu opens and closes, so screen readers announce the menu state.

## Related Components

- [Select Dropdown](./select-dropdown.md) — Use when the user is choosing a value to populate a form field rather than executing an action.
- [Modal / Dialog](./modal-dialog.md) — Use when an action requires a confirmation step, rich body content, or a form before it can be committed.
