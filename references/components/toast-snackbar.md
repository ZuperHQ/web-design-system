---
component: Toast / Snackbar
category: Feedback & Content
variants: [toast, snackbar, success, error, warning, info]
related: [modal-dialog]
---

# Toast / Snackbar

> A transient feedback component that surfaces brief, non-blocking notifications or bulk-selection action bars without interrupting the user's current workflow.

## Overview

The Toast is a white card positioned fixed at the top-right of the viewport, rendered with a `shadow-lg` and a subtle `ring-1 ring-black ring-opacity-5` outline; it contains a leading icon or avatar, a title, an optional body message, and a dismiss button. The Snackbar is a dark pill (`bg-[#192d43]`) anchored at the bottom of the screen that appears when one or more list rows are selected, surfacing bulk actions such as Assign, Export, Delete, and a dismiss control. Together they form the design system's primary surface for ephemeral, asynchronous feedback and multi-record operations.

## When to Use

- A background operation completes (record saved, job assigned, message sent) and the user needs brief confirmation without being pulled off their current page.
- An async error occurs (SMS delivery failure, API rejection) and the user needs to be informed immediately without a blocking modal.
- One or more table or list rows are selected and the user must act on the selection (assign, export, delete) via the Snackbar bulk-action bar.
- A real-time event arrives (chat message, push notification) that the user may want to act on inline before navigating.
- A simple status result (success or error) needs to be communicated with a single icon and one line of text.

## When NOT to Use

- The user must read and respond to important information before continuing — use [Modal / Dialog](./modal-dialog.md) instead.
- The feedback is tied to a specific form field and needs to appear inline — use [Text Input](./text-input.md) with its built-in error/helper state instead.

## Variants

| Variant | Description |
|---------|-------------|
| toast — module notification | Use when a Zuper module event (work order, job, asset) has occurred and the notification requires an icon circle coloured to the module's brand colour. |
| toast — chat notification | Use when an incoming chat message requires an avatar, a badge icon, and an inline Reply action button separated by a left border. |
| toast — error / failed | Use when an async operation has failed (e.g. SMS delivery); leads with a `bg-red-50` icon circle and `text-red-500` heading to signal severity. |
| toast — simple success | Use for single-line confirmations where only a `ti-circle-check text-green-500` icon and one sentence of text are needed. |
| toast — simple error | Use for single-line failure notices where only a `ti-circle-x text-red-500` icon and one sentence of text are needed. |
| snackbar — select all + actions | Use when a list selection is started; shows a count, a Select All shortcut, and individual action buttons (Assign, Export, Delete). |
| snackbar — clear all + overflow | Use when the action set is too wide for the bar; collapses secondary actions into a "More actions" overflow button and offers a Clear All shortcut. |

## HTML Structure

```html
<!-- Toast — Module notification -->
<div class="pointer-events-auto w-full overflow-hidden cursor-pointer rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
  <div class="p-4">
    <div class="flex items-start">
      <div class="flex-shrink-0 rounded-full px-3.5 py-3 bg-orange-50">
        <em class="ti ti-clipboard-list text-3xl font-medium text-primary"></em>
      </div>
      <div class="ml-3 w-0 flex-1 pt-0.5">
        <p class="text-base font-medium text-gray-900">Work Order Assigned</p>
        <p class="mt-1 text-base text-gray-500">WO-10432 has been assigned to John Doe.</p>
      </div>
      <div class="ml-4 flex flex-shrink-0">
        <button type="button" class="inline-flex rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none">
          <!-- 20×20 SVG close icon -->
        </button>
      </div>
    </div>
  </div>
</div>

<!-- Toast — Simple success -->
<div class="pointer-events-auto w-full overflow-hidden cursor-pointer rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
  <div class="p-4">
    <div class="flex items-center gap-3">
      <div class="flex">
        <i class="ti ti-circle-check text-green-500 text-2xl"></i>
      </div>
      <div class="w-0 flex-1">
        <p class="text-base font-medium text-gray-900">Job updated successfully</p>
      </div>
    </div>
  </div>
</div>

<!-- Toast — Simple error -->
<div class="pointer-events-auto w-full overflow-hidden cursor-pointer rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
  <div class="p-4">
    <div class="flex items-center gap-3">
      <div class="flex">
        <i class="ti ti-circle-x text-red-500 text-2xl"></i>
      </div>
      <div class="w-0 flex-1">
        <p class="text-base font-medium text-gray-900">Error in updating details</p>
      </div>
    </div>
  </div>
</div>

<!-- Toast — Chat notification (avatar + badge + Reply action) -->
<div class="pointer-events-auto flex w-full rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
  <div class="w-0 flex-1 p-4">
    <div class="flex items-start">
      <div class="flex-shrink-0 pt-0.5">
        <span class="relative inline-block">
          <div class="h-10 w-10 rounded-full bg-gray-200 flex items-center justify-center text-gray-500">
            <i class="ti ti-user text-xl"></i>
          </div>
          <span class="absolute bottom-0 right-0 block translate-y-1/3 translate-x-1/3 transform rounded-full border-2 border-white">
            <span class="h-5 w-5 rounded-full bg-indigo-500 flex justify-center items-center">
              <i class="ti ti-mail text-white" style="font-size:0.6rem"></i>
            </span>
          </span>
        </span>
      </div>
      <div class="ml-3 w-0 flex-1">
        <p class="text-base font-medium text-gray-900">Sarah Johnson</p>
        <p class="mt-1 text-base text-gray-500 mx-0.5 max-w-md truncate">Hi, the HVAC unit is making a strange noise again...</p>
      </div>
    </div>
  </div>
  <div class="flex border-l border-gray-200 cursor-pointer">
    <button type="button" class="flex w-full items-center justify-center rounded-none rounded-r-lg border border-transparent p-4 text-sm font-medium text-indigo-600 hover:text-indigo-500 focus:outline-none">Reply</button>
  </div>
</div>

<!-- Toast — Error / Failed -->
<div class="pointer-events-auto w-full overflow-hidden cursor-pointer rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
  <div class="p-4">
    <div class="flex items-start">
      <div class="flex-shrink-0 rounded-full px-3.5 py-2 bg-red-50">
        <em class="ti ti-alert-triangle text-3xl font-medium text-red-500"></em>
      </div>
      <div class="ml-3 w-0 flex-1 pt-0.5">
        <p class="text-base font-semibold text-red-500">Message Failed</p>
        <p class="text-md font-medium text-[#252A31]">Message could not be delivered</p>
        <p class="mt-1 text-sm text-gray-500 line-clamp-3">Hi, your technician is on the way to fix the unit.</p>
      </div>
      <div class="ml-4 flex flex-shrink-0">
        <button type="button" class="inline-flex rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none">
          <!-- 20×20 SVG close icon -->
        </button>
      </div>
    </div>
  </div>
</div>

<!-- Snackbar — With Select All + actions -->
<div class="rounded-lg shadow-lg px-4 py-3 select-none text-base text-white inline-flex" style="background-color:#192d43">
  <div class="flex items-center justify-between gap-6">
    <div class="flex items-center gap-2">
      <div class="flex items-center h-8 opacity-80 gap-2 whitespace-nowrap leading-tight">3 Job(s)</div>
      <button type="button" class="flex items-center cursor-pointer py-1 px-2.5 h-8 whitespace-nowrap hover:bg-gray-700 rounded-lg leading-tight">Select All</button>
    </div>
    <div class="flex items-center gap-2">
      <button type="button" class="px-2.5 py-1 h-8 rounded-lg inline-flex items-center gap-1.5 leading-tight bg-gray-600 hover:bg-gray-700 text-white whitespace-nowrap">Assign</button>
      <button type="button" class="px-2.5 py-1 h-8 rounded-lg inline-flex items-center gap-1.5 leading-tight bg-gray-600 hover:bg-gray-700 text-white whitespace-nowrap">Export</button>
      <button type="button" class="px-2.5 py-1 h-8 rounded-lg inline-flex items-center gap-1.5 leading-tight bg-red-600 hover:bg-red-700 text-white whitespace-nowrap">Delete</button>
      <button type="button" class="px-1.5 h-8 rounded-lg hover:bg-gray-700 flex items-center text-white">
        <i class="ti ti-x text-xl mt-0.5 opacity-80"></i>
      </button>
    </div>
  </div>
</div>

<!-- Snackbar — With Clear All + overflow "More actions" -->
<div class="rounded-lg shadow-lg px-4 py-3 select-none text-base text-white inline-flex" style="background-color:#192d43">
  <div class="flex items-center justify-between gap-6">
    <div class="flex items-center gap-2">
      <div class="flex items-center h-8 opacity-80 gap-2 whitespace-nowrap leading-tight">10 Job(s)</div>
      <button type="button" class="flex items-center cursor-pointer py-1 px-2.5 h-8 whitespace-nowrap hover:bg-gray-700 rounded-lg leading-tight">Clear All</button>
    </div>
    <div class="flex items-center gap-2">
      <button type="button" class="px-2.5 py-1 h-8 rounded-lg inline-flex items-center gap-1.5 leading-tight bg-gray-600 hover:bg-gray-700 text-white whitespace-nowrap">Assign</button>
      <button type="button" class="px-2.5 py-1 h-8 rounded-lg inline-flex items-center gap-1.5 leading-tight bg-gray-600 hover:bg-gray-700 text-white whitespace-nowrap">Export</button>
      <button type="button" class="px-2.5 h-8 rounded-lg flex items-center gap-1.5 bg-gray-600 hover:bg-gray-700 text-white whitespace-nowrap leading-tight">
        <span>More actions</span>
        <i class="ti ti-dots text-xl"></i>
      </button>
      <button type="button" class="px-1.5 h-8 rounded-lg hover:bg-gray-700 flex items-center text-white">
        <i class="ti ti-x text-xl mt-0.5 opacity-80"></i>
      </button>
    </div>
  </div>
</div>
```

## Dos & Don'ts

### Do

- Keep toast body text to one or two short sentences so the notification is scannable at a glance before it auto-dismisses.
- Use the simple success (`ti-circle-check text-green-500`) and simple error (`ti-circle-x text-red-500`) variants for generic CRUD feedback, reserving the module-icon variant for entity-specific events.
- Always include a dismiss button (`ti-x`) so the user can clear the toast immediately if it obscures content.
- Display the Snackbar as soon as the first row is selected and dismiss it as soon as the selection count reaches zero.
- Place destructive Snackbar actions (Delete) in `bg-red-600 hover:bg-red-700` to distinguish them visually from neutral actions.

### Don't

- Do not stack more than four toasts simultaneously — overflow the queue by removing the oldest notification first, otherwise the screen fills.
- Do not put a Snackbar in place of a toast for single-record feedback; the Snackbar is strictly for bulk selection contexts.
- Do not omit the `pointer-events-auto` class from toast wrappers — without it, hover and click events will not fire when the toast lives inside a `pointer-events-none` overlay container.
- Do not use the toast for destructive confirmation dialogs (e.g. "Are you sure you want to delete?") — those require a blocking [Modal / Dialog](./modal-dialog.md).
- Do not truncate toast titles; `font-medium text-gray-900` titles must remain fully visible so the user understands the notification without opening a detail view.

## Patterns & Rules

1. **Auto-dismiss timing** — Toasts should auto-dismiss after a short, fixed duration (typically 4–6 seconds); error toasts may persist until manually dismissed to ensure the user does not miss failure information.
2. **Snackbar count label** — Always show the count as `N Job(s)` (or the relevant entity name) at the leading edge of the Snackbar so the user knows how many records the bulk action will affect.
3. **Overflow to "More actions"** — When more than three Snackbar action buttons are needed, collapse secondary actions into a `ti-dots` overflow button to prevent the bar from exceeding its container width.
4. **Module icon background** — Module-specific toast icons must use a tinted background circle (`bg-orange-50`, `bg-red-50`, etc.) that matches the severity or module colour, keeping the icon visually distinct from the white card.
5. **Chat notification Reply placement** — The Reply action in the chat variant must be separated from the message body by a `border-l border-gray-200` divider and styled as `text-indigo-600`, not as a filled button, to preserve the light notification aesthetic.

## Accessibility

- Toast: apply `role="status"` for success/info notifications and `role="alert"` for error notifications so screen readers announce the content without requiring user focus.
- Snackbar: apply `role="toolbar"` to the action button group and ensure each button has a descriptive `aria-label` when its text label alone may be ambiguous.
- The dismiss button in both component forms must be reachable via Tab and activated with Enter or Space; use `focus:outline-none` only alongside a custom visible focus ring to maintain keyboard accessibility.
- Toasts must not auto-dismiss while the user has keyboard focus inside the notification; pause the dismiss timer on `focusin` and resume on `focusout`.

## Related Components

- [Modal / Dialog](./modal-dialog.md) — Use instead of a toast when the user must acknowledge or respond to information before continuing their workflow.
