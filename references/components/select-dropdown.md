---
component: Select / Dropdown
category: Interactive
variants: [single-select, multi-select, searchable]
related: [text-input, dropdown-menu, form-layout]
---

# Select / Dropdown

> A form control that lets users pick one or more values from a predefined list via an overlay panel, replacing the browser's native `<select>` with a consistent, styleable trigger and option list.

## Overview

The Select / Dropdown renders as a rounded trigger button (`h-9 rounded-lg border border-border`) that reveals a floating panel (`bg-white border border-gray-200 rounded-lg shadow-lg`) anchored directly below. It fills a form field role across the Zuper design system, sharing height and border radius with Text Input so mixed-field forms align on a single grid baseline. The chevron icon (`ti ti-chevron-down` / `ti ti-chevron-up`) communicates closed/open state, and a `ti ti-check` mark inside the list confirms the active selection.

## When to Use

- Choosing from a fixed, enumerated set of values (e.g., Priority: Low / Medium / High / Urgent) where all options are known at design time.
- Selecting a single entity from a moderate list (5–30 items) that would be impractical as radio buttons.
- Picking one or more assignees, categories, or tags inside a filter chip row where horizontal space is constrained.
- Replacing a native `<select>` element to meet the design system's visual style or to add icons and grouped options.
- Collecting a required field in a form where a missing value must trigger an inline error (`border-red-500` + `text-sm text-red-500` helper text).

## When NOT to Use

- Choosing between 2–3 mutually exclusive options — use [Checkbox & Toggle](./checkbox-toggle.md) instead (radio-style toggles take less interaction cost).
- Triggering an action (edit, delete, export) — use [Dropdown Menu](./dropdown-menu.md) instead, which is scoped to commands rather than value selection.

## Variants

| Variant | Description |
|---------|-------------|
| single-select | Default variant; exactly one value is active at a time, confirmed by a `ti ti-check` icon beside the selected option. Use when only one value is semantically valid. |
| multi-select | Multiple options can be checked simultaneously, each confirmed by a `ti ti-check`. The panel adds a **Selected:** list (each row removable with `ti ti-x`) and an **Update** button that commits the set; the trigger summarises the count (e.g., "3 selected") when options overflow the trigger width. Use for assignees, skills, tags, or any field that is logically a set. |
| searchable | An inline `<input type="text" placeholder="Search">` is rendered at the top of the open panel, filtering the visible options in real time. Use when the list exceeds roughly 15 items and users benefit from type-ahead filtering. |

## HTML Structure

```html
<!-- Rest state (closed) -->
<div class="h-9 w-full rounded-lg border border-border bg-white px-2 text-base text-gray-600 flex items-center justify-between cursor-pointer">
  <span class="truncate text-base text-gray-400">Select option…</span>
  <i class="ti ti-chevron-down text-gray-600 flex-shrink-0"></i>
</div>

<!-- Open state — trigger changes border to border-gray-400, chevron flips to ti-chevron-up -->
<div class="h-9 w-full rounded-lg border border-gray-400 bg-white px-2 text-base text-gray-600 flex items-center justify-between cursor-pointer">
  <span class="truncate text-base">Low</span>
  <i class="ti ti-chevron-up text-gray-600 flex-shrink-0"></i>
</div>

<!-- Floating panel (positioned absolute, z-50, appears directly below trigger) -->
<div class="absolute z-50 w-full mt-0.5 bg-white border border-gray-200 rounded-lg shadow-lg max-w-50 overflow-auto zuper-scrollbar">
  <div class="p-1 space-y-1">
    <!-- Selected option -->
    <button class="flex gap-2 items-center justify-between hover:bg-gray-100 rounded-lg cursor-pointer w-full px-2 py-1 text-left text-gray-800">
      <span class="truncate text-base">Low</span>
      <i class="ti ti-check flex-shrink-0"></i>
    </button>
    <!-- Unselected option (default) -->
    <button class="flex gap-2 items-center justify-between hover:bg-gray-100 rounded-lg cursor-pointer w-full px-2 py-1 text-left text-gray-500">
      <span class="truncate text-base">Medium</span>
    </button>
    <!-- Hovered option -->
    <button class="flex gap-2 items-center justify-between bg-gray-100 rounded-lg cursor-pointer w-full px-2 py-1 text-left text-gray-500">
      <span class="truncate text-base">High</span>
    </button>
  </div>
</div>

<!-- Multi-select panel (searchable) — e.g. Skills in the details center overview -->
<div class="bg-white border border-gray-200 rounded-lg shadow-lg overflow-hidden flex flex-col" style="min-width: 240px; max-width: 320px;">
  <!-- Search header -->
  <div class="relative border-b border-gray-200 flex-shrink-0">
    <i class="ti ti-search absolute left-3 top-1/2 -translate-y-1/2 text-gray-400 text-base pointer-events-none"></i>
    <input type="text" placeholder="Search" class="w-full pl-8 pr-8 py-1.5 text-base text-gray-700 placeholder-gray-400 focus:outline-none">
  </div>
  <!-- Options: selected = text-gray-800 + ti-check, unselected = text-gray-500, hover = bg-gray-100 -->
  <div class="overflow-y-auto zuper-scrollbar p-1" style="max-height: 15rem;">
    <button type="button" class="cursor-pointer gap-2 flex items-center justify-between hover:bg-gray-100 rounded-lg w-full px-2 py-1.5 text-left text-gray-800">
      <span class="truncate text-base leading-tight">Installation</span>
      <i class="ti ti-check text-lg flex-shrink-0"></i>
    </button>
    <button type="button" class="cursor-pointer gap-2 flex items-center justify-between hover:bg-gray-100 rounded-lg w-full px-2 py-1.5 text-left text-gray-500">
      <span class="truncate text-base leading-tight">Kitchen floor cleaning</span>
    </button>
    <button type="button" class="cursor-pointer gap-2 flex items-center justify-between hover:bg-gray-100 rounded-lg w-full px-2 py-1.5 text-left text-gray-800">
      <span class="truncate text-base leading-tight">Lawn Cleaning</span>
      <i class="ti ti-check text-lg flex-shrink-0"></i>
    </button>
    <!-- Hovered unselected option: bg-gray-100, text colour unchanged -->
    <button type="button" class="cursor-pointer gap-2 flex items-center justify-between bg-gray-100 rounded-lg w-full px-2 py-1.5 text-left text-gray-500">
      <span class="truncate text-base leading-tight">Kitchen Installation</span>
    </button>
    <button type="button" class="cursor-pointer gap-2 flex items-center justify-between hover:bg-gray-100 rounded-lg w-full px-2 py-1.5 text-left text-gray-500">
      <span class="truncate text-base leading-tight">Parking systems installation</span>
    </button>
  </div>
  <!-- Selected list (shown when at least one item is selected and search is empty) -->
  <div class="px-3 py-2 flex items-center justify-start border-t border-gray-200">
    <span class="text-base font-medium truncate leading-tight">Selected:</span>
  </div>
  <div class="overflow-y-auto zuper-scrollbar px-1 pb-2 mb-0.5" style="max-height: 9rem;">
    <div class="flex gap-2 items-center leading-tight justify-between hover:bg-gray-100 w-full px-3 py-1.5 text-left rounded-md text-gray-700">
      <span class="truncate text-base">Installation</span>
      <button type="button" title="Remove" class="flex items-center h-5 w-5 justify-center flex-shrink-0 text-gray-400 hover:text-gray-600 rounded-md p-1 hover:bg-gray-200">
        <i class="ti ti-x"></i>
      </button>
    </div>
    <div class="flex gap-2 items-center leading-tight justify-between hover:bg-gray-100 w-full px-3 py-1.5 text-left rounded-md text-gray-700">
      <span class="truncate text-base">Lawn Cleaning</span>
      <button type="button" title="Remove" class="flex items-center h-5 w-5 justify-center flex-shrink-0 text-gray-400 hover:text-gray-600 rounded-md p-1 hover:bg-gray-200">
        <i class="ti ti-x"></i>
      </button>
    </div>
  </div>
  <!-- Commit footer -->
  <div class="p-2 border-t border-gray-200">
    <button type="button" class="w-full px-3 py-1.5 rounded-md text-base text-white bg-primary hover:opacity-90">Update</button>
  </div>
</div>

<!-- Error state -->
<div class="h-9 w-full rounded-lg border border-red-500 bg-white px-2 text-base text-gray-600 flex items-center justify-between cursor-pointer">
  <span class="truncate text-base text-gray-400">Select option…</span>
  <i class="ti ti-chevron-down text-gray-600 flex-shrink-0"></i>
</div>
<div class="text-sm text-red-500 mt-1">Selection is required</div>
```

## Dos & Don'ts

### Do

- Always show a placeholder (`text-gray-400`) in the trigger when no value has been selected, so users can distinguish an empty field from a field with a value.
- Use `truncate` on both the trigger label and each option `<span>` so the component degrades gracefully at narrow widths without breaking layout.
- Apply `border-red-500` on the trigger and a `text-sm text-red-500 mt-1` message below for validation errors — match the exact pattern used by Text Input for visual consistency.
- Set the panel to `absolute z-50` so it overlays sibling form fields without causing layout reflow.
- Use `zuper-scrollbar` on the panel when the option list may overflow, keeping the custom scrollbar style consistent with other overflow containers in the app.

### Don't

- Do not use a native `<select>` element in place of this component — it breaks visual consistency with the design system's border radius, height, and icon conventions.
- Do not omit the `ti ti-check` mark on the selected option — removing it forces users to scan for background-colour differences alone, which fails at low contrast and harms accessibility.
- Do not allow the trigger label to wrap onto a second line — the trigger has a fixed `h-9` height; multi-line text will overflow and clip.
- Do not place the panel with `position: fixed` unless the trigger is inside a scroll container — fixed positioning causes misalignment when the page scrolls.
- Do not use this component for navigation or commands — opening a page or triggering a destructive action from a Select panel confuses users who expect it to behave as a value field.

## Patterns & Rules

1. **Trigger height is always h-9** — The trigger must remain `h-9` (36 px) to align with Text Input and other form controls on the same row; never adjust height per variant.
2. **Panel anchors with mt-0.5** — The floating panel uses `mt-0.5` offset so there is a 2 px visual gap between the trigger bottom border and the panel top border, preventing the borders from merging.
3. **Option rows use py-1 px-2** — All option buttons use `px-2 py-1` padding so touch targets remain at least 32 px tall and text aligns with the trigger label's left edge.
4. **Selected state uses text-gray-800 + ti-check; unselected uses text-gray-500; hover adds bg-gray-100 only** — This two-tone system creates a clear visual hierarchy in the list without relying solely on a background fill. Hover never changes the option's text colour, so selected and unselected items stay distinguishable while the pointer is over them. The same rules apply to single-select and multi-select.
6. **Multi-select anatomy** — Options use `px-2 py-1.5 rounded-lg` with a `ti ti-check text-lg` on selected rows. Below the list, when at least one item is selected and the search is empty, show a `border-t border-gray-200` **Selected:** header (`text-base font-medium`) followed by removable rows (`text-gray-700`, `hover:bg-gray-100`, remove button `text-gray-400 hover:text-gray-600 hover:bg-gray-200`). End with a `p-2 border-t border-gray-200` footer holding a full-width `bg-primary` **Update** button; changes apply only when it is clicked.
5. **Error validation targets the trigger border only** — Replace `border-border` with `border-red-500` on the trigger div; do not change the panel or option styles, as the error state belongs to the field, not the options.

## Accessibility

- The trigger element must have `role="combobox"` and `aria-haspopup="listbox"` to communicate its purpose to assistive technology.
- The option list must have `role="listbox"` and each option button must have `role="option"` with `aria-selected="true|false"`.
- Keyboard interactions: `Tab` moves focus to the trigger; `Enter` or `Space` opens/closes the panel; `ArrowDown` / `ArrowUp` moves focus through options; `Escape` closes the panel and returns focus to the trigger.
- Screen readers must announce the currently selected value when the trigger receives focus, using `aria-label` or a visible `<label>` element associated via `for` / `id`.

## Related Components

- [Dropdown Menu](./dropdown-menu.md) — A visually similar overlay panel (`select-none min-w-44 bg-white border border-gray-200 rounded-lg shadow-lg`) used for commands and actions rather than value selection; does not have a form-field trigger.
- [Text Input](./text-input.md) — Shares `h-9 rounded-lg border border-border` form field anatomy; use Text Input when the value is free-form rather than constrained to a list.
- [Form Layout](./form-layout.md) — Defines the grid (`grid-cols-4` for wide panels, `grid-cols-3` for narrow) and `gap-4` spacing that governs how Select fields are composed alongside other form controls.
