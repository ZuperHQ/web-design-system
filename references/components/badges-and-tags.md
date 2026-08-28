---
component: Badges & Tags
category: Data Display
variants: [status-badge, priority-badge, count-badge, tag, chip]
related: [cards, tables]
---

# Badges & Tags

> Small, non-interactive inline labels that communicate status, priority, counts, or categorical metadata at a glance without requiring user action.

## Overview

Badges and tags are compact inline components rendered as pill or rounded-rectangle shapes with color-coded backgrounds, borders, and text to convey meaning. They occupy three distinct roles in the design system: status/priority badges signal workflow state or urgency using semantic color palettes, count badges surface numeric quantities in a neutral style, and tags/chips label entities with removable categorical identifiers. All variants are non-interactive by default, though tags support an optional dismiss action.

## When to Use

- Display the current workflow status of a record (e.g., Active, Pending, Overdue, Draft) inline within a table row, card, or detail panel.
- Indicate priority level (Critical, High, Medium, Low) on a job or task so users can triage at a glance.
- Show a count of associated items (tasks completed, unread messages, related records) next to a label or heading.
- Render a flat list of categorical labels — such as job types or skill tags — on a record where users may need to add or remove individual labels.
- Summarize overflow quantities using the "99+" capped count badge when an exact number would be too long.

## When NOT to Use

- Do not use a badge to trigger navigation or perform an action — use [Button](./button.md) instead.
- Do not use a tag to select from a list of options in a form — use [Select Dropdown](./select-dropdown.md) instead.
- Do not use a status badge as the sole affordance for changing a status — pair it with a dropdown or use a dedicated status selector component.

## Variants

| Variant | Description |
|---------|-------------|
| status-badge | Use when communicating workflow state (Active, Pending, Overdue, Draft); color encodes meaning — green for success, yellow for warning, red for danger, gray for neutral. |
| priority-badge | Use when communicating urgency level (Critical, High, Medium, Low); shares the same visual structure as status-badge but maps to a priority scale — red/orange/yellow/gray. |
| count-badge | Use when displaying a numeric quantity beside a label; intentionally neutral (gray border, gray-50 background) so it does not compete with status color. |
| tag | Use when displaying static categorical labels on a record where removal is not needed; rendered as a fixed-height chip with truncation. |
| chip | Use when a categorical label must be removable by the user; identical to tag but includes a dismiss icon (ti-x) and a hover state to signal interactivity. |

## HTML Structure

```html
<!-- Status / Priority Badge -->
<span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-green-100 text-green-700 border-green-200">
  Active
</span>

<!-- Warning state -->
<span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-yellow-100 text-yellow-700 border-yellow-200">
  Pending
</span>

<!-- Danger state -->
<span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-red-100 text-red-700 border-red-200">
  Overdue
</span>

<!-- Neutral state -->
<span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-gray-100 text-gray-600 border-gray-200">
  Draft
</span>

<!-- High priority (orange) -->
<span class="px-1.5 py-1 leading-tight rounded-md font-medium text-md border cursor-default bg-orange-100 text-orange-700 border-orange-200">
  High
</span>

<!-- Count Badge -->
<span class="px-1.5 py-0.5 text-md border border-border rounded-lg bg-gray-50 text-gray-700 leading-tight">
  12
</span>

<!-- Count Badge at limit -->
<span class="px-1.5 py-0.5 text-md border border-border rounded-lg bg-gray-50 text-gray-700 leading-tight">
  99+
</span>

<!-- Tag (static, no dismiss) -->
<span class="inline-flex items-center justify-center border border-gray-200 font-medium rounded-md px-2 h-6 min-w-6 gap-1.5 text-sm shrink-0 bg-gray-100 text-gray-700" title="Installation">
  <span class="truncate leading-tight max-w-24">Installation</span>
</span>

<!-- Chip (removable tag) -->
<span class="inline-flex items-center justify-center border border-gray-200 font-medium rounded-md px-2 h-6 min-w-6 gap-1.5 text-sm shrink-0 bg-gray-100 text-gray-700 cursor-pointer hover:bg-gray-200" title="Plumbing">
  <span class="truncate leading-tight max-w-24">Plumbing</span>
  <i class="ti ti-x text-sm flex-shrink-0"></i>
</span>
```

## Dos & Don'ts

### ✅ Do

- Match the color palette to semantic meaning: green for success/active, yellow for warning/medium, red for danger/critical/overdue, orange for high priority, gray for neutral/draft/low.
- Use `cursor-default` on status and priority badges to signal they are non-interactive.
- Apply `truncate` and `max-w-24` on tag/chip inner text spans to prevent overflow in constrained layouts.
- Cap count badges at "99+" when the number exceeds two digits to avoid layout disruption.
- Always provide a `title` attribute on tag and chip components so the full label is accessible on hover when the text is truncated.

### ❌ Don't

- Do not reuse status color classes (e.g., `bg-green-100`) for decorative purposes unrelated to status — it trains users to misread color signals and undermines the semantic system.
- Do not use a badge where an action is needed — badges are informational only, and adding click handlers to them breaks the design contract with users.
- Do not mix status-badge and count-badge styles on the same element — the padding, radius, and background scales are intentionally different.
- Do not omit the matching border color (e.g., `border-green-200` alongside `bg-green-100`) — without it the badge loses definition on light page backgrounds.
- Do not place more than five or six tags in a single inline row without wrapping via `flex-wrap` — unwrapped tag lists cause horizontal overflow on narrow viewports.

## Patterns & Rules

1. **Semantic color pairing** — Always use the 100-level background, 700-level text, and 200-level border from the same Tailwind color family (e.g., `bg-red-100 text-red-700 border-red-200`). Mixing levels from different families breaks the tonal consistency of the badge system.
2. **Count badge neutrality** — Count badges intentionally use a neutral palette (`bg-gray-50`, `border-border`, `text-gray-700`) regardless of the value they display. If the count itself carries urgency, pair it with a separate status badge rather than recoloring the count badge.
3. **Tag truncation ceiling** — The inner text span of a tag or chip must carry `max-w-24` to cap display at approximately 96px. Longer labels should either be abbreviated or use a tooltip; never allow the chip to grow unbounded in flex containers.
4. **Dismiss affordance only on chips** — The `ti-x` dismiss icon and `hover:bg-gray-200` hover state are exclusive to removable chips. Static tags must not include these styles, as hover states imply interactivity to users.
5. **Vertical rhythm** — Status and priority badges use `py-1` while count badges use `py-0.5`. Do not equalize the padding — the difference is intentional and keeps count badges visually lighter than status badges in the same row.

## Accessibility

- Status and priority badges should include `role="status"` when they update dynamically (e.g., after a save action) so screen readers announce the change.
- Badges and static tags are non-interactive and must not receive keyboard focus; do not add `tabindex` to them.
- Removable chips (with `ti-x`) must be wrapped in or replaced by a `<button>` element with an `aria-label` such as `"Remove Plumbing tag"` so keyboard users can activate the dismiss action.
- Color alone does not distinguish badge states for colorblind users — always include a visible text label inside every badge rather than relying on color as the sole indicator.

## Related Components

- [Cards](./cards.md) — Cards frequently embed status and priority badges in their header row to surface record state without opening the detail view.
- [Select Dropdown](./select-dropdown.md) — When the user needs to choose or change a status or priority value, a select dropdown should be used rather than a clickable badge.
