---
component: Modal / Dialog
category: Overlay
variants: [confirmation-dialog, form-modal, header-variants]
related: [drawer-panel, expansion-panel]
---

# Modal / Dialog

> A Modal / Dialog is a focused overlay that interrupts the current workflow to capture a required decision or user input before the user can continue.

## Overview

The Modal / Dialog renders as a white, rounded card (`border-radius: 10px`) elevated with a strong drop shadow (`shadow-2xl`) and centered over a backdrop. It is the design system's primary component for requiring explicit user action — confirmations, destructive-action warnings, and short-form data entry — before returning control to the underlying page. Content is divided into three distinct zones: a header (title and optional dismiss button), a scrollable body, and a footer action bar on a `bg-gray-50` ground.

## When to Use

- Asking the user to confirm a destructive or irreversible action, such as deleting a record or closing a work order.
- Presenting a short inline form (2–4 fields) that must be completed before the user proceeds, such as editing a description or renaming an entity.
- Surfacing a time-sensitive system alert — for example, a session-expiry warning — that requires an immediate decision.
- Blocking navigation or workflow continuation until the user makes an explicit binary choice (proceed vs. cancel).

## When NOT to Use

- When the content is a detail view with many fields or requires persistent side-by-side context — use [Drawer Panel](./drawer-panel.md) instead, which slides in without fully blocking the page.
- When the content is collapsible in-page information that does not require a blocking decision — use [Expansion Panel](./expansion-panel.md) instead.

## Variants

| Variant | Description |
|---------|-------------|
| confirmation-dialog (Warning) | Use for consequential but recoverable actions; renders an amber icon (`text-amber-500 bg-amber-100`) and an amber confirm button to signal caution without implying permanent loss. |
| confirmation-dialog (Error / Danger) | Use for irreversible destructive actions such as deletion; renders a red icon (`text-red-600 bg-red-100`) and a red confirm button (`bg-red-600`) to communicate maximum severity. |
| confirmation-dialog (Info) | Use for system-initiated prompts that are not user errors, such as session expiry; renders a blue icon (`text-blue-600 bg-blue-100`) and omits the top-right dismiss button when the choice is mandatory. |
| form-modal | Use when the user must edit or enter data in a short form before saving; provides a titled header with a border, a scrollable body capped at `max-h-[65vh]`, and a footer with cancel and submit actions. |

## HTML Structure

```html
<!-- Confirmation dialog (Warning variant) -->
<div class="bg-white shadow-2xl flex flex-col" style="width:30rem;border-radius:10px">
  <div class="relative flex flex-col w-full h-full">

    <!-- Dismiss button (omit for mandatory Info dialogs) -->
    <div class="absolute top-0 right-0 pt-4 pr-4">
      <button class="inline-flex items-center justify-center h-10 w-10 rounded-full hover:bg-gray-100 text-gray-500">
        <i class="ti ti-x text-xl"></i>
      </button>
    </div>

    <!-- Body: icon + title + supporting text -->
    <div class="flex flex-row flex-auto items-start p-8 pb-6">
      <!-- Icon badge: swap color classes per variant -->
      <div class="flex flex-0 items-center justify-center w-10 h-10 mr-4 rounded-full text-amber-500 bg-amber-100 flex-shrink-0">
        <i class="ti ti-alert-triangle text-current text-xl"></i>
      </div>
      <div class="flex flex-col items-start space-y-1 pr-8">
        <div class="text-xl leading-6 font-medium">Close Work Order?</div>
        <div class="text-gray-500 text-base">This action cannot be undone and will notify the assigned technician.</div>
      </div>
    </div>

    <!-- Footer action bar -->
    <div class="px-6 py-4 bg-gray-50 flex" style="border-radius:0 0 10px 10px">
      <div class="flex items-center space-x-3 justify-end flex-1">
        <button class="px-6 flex items-center py-2 border shadow-sm text-gray-600 bg-white text-base font-medium rounded-md h-10">Cancel</button>
        <!-- Confirm button: swap bg color per variant (bg-amber-500 / bg-red-600 / bg-blue-500) -->
        <button class="px-6 flex items-center py-2 border shadow-sm text-white text-base font-medium rounded-md h-10 bg-amber-500">Close</button>
      </div>
    </div>

  </div>
</div>

<!-- Form modal -->
<div class="bg-white shadow-2xl flex flex-col" style="width:40rem;border-radius:10px">

  <!-- Header: zuper-dialog-header pattern — py-3 px-5 flex items-center with bottom border -->
  <div class="flex justify-between border-b border-gray-300 py-3 px-5 items-center">
    <h6 class="font-semibold text-gray-800 text-base">Edit Description</h6>
    <span class="rounded-full cursor-pointer flex justify-center items-center hover:bg-gray-200 h-10 w-10 p-2 ml-2">
      <i class="ti ti-x text-xl font-bold"></i>
    </span>
  </div>

  <!-- Body: zuper-dialog-body pattern — p-5 with max-dialog-height (max-h-[65vh]) and overflow-y-auto -->
  <div class="flex flex-col p-5 overflow-y-auto" style="max-height:65vh">
    <div class="space-y-4">
      <!-- Form fields go here -->
    </div>
  </div>

  <!-- Footer: zuper-dialog-footer pattern — p-5 with top border -->
  <div class="flex justify-end border-t border-gray-300 p-5">
    <div class="flex justify-around space-x-4 bg-gray-50">
      <button class="px-6 h-10 flex items-center py-2 border border-gray-300 shadow-sm text-base font-medium rounded-md text-gray-600 bg-white hover:bg-gray-50">Cancel</button>
      <button class="min-w-24 px-6 h-10 flex items-center py-2 border shadow-sm text-base text-white font-medium rounded-md bg-primary">Update</button>
    </div>
  </div>

</div>
```

## Dos & Don'ts

### ✅ Do

- Match the icon badge color (`text-amber-500 bg-amber-100`, `text-red-600 bg-red-100`, `text-blue-600 bg-blue-100`) and the confirm button color to the severity of the action being confirmed.
- Keep the body copy for confirmation dialogs to one or two short sentences — state what will happen and any consequence the user needs to know.
- Use the `max-h-[65vh]` + `overflow-y-auto` body constraint on form modals so the dialog never overflows the viewport on smaller screens.
- Always provide a clearly labeled cancel path alongside the primary action so the user can safely exit without making a change.
- Apply the `border-radius:0 0 10px 10px` inline style to the footer bar so it rounds only the bottom corners and aligns with the outer container.

### ❌ Don't

- Do not open a Modal / Dialog on top of another Modal / Dialog — stacked blocking overlays disorient users and make it impossible to track context.
- Do not place more than four or five form fields in a form modal — content that long belongs in a dedicated page or [Drawer Panel](./drawer-panel.md).
- Do not omit the footer action bar and put action buttons inside the body — this breaks the predictable three-zone layout the design system enforces.
- Do not use a single "OK" button as the only action for a destructive confirmation — always pair a cancel button with the confirm button so the user has an explicit escape.
- Do not remove the `shadow-2xl` drop shadow — it is what visually separates the modal from the backdrop and indicates its elevation in the layer stack.

## Patterns & Rules

1. **Three-zone layout** — Every modal must follow the header → body → footer structure. The header names the task, the body contains the content or form, and the footer holds the action buttons; mixing actions into the body breaks this contract.
2. **Severity signaling** — Confirmation dialogs communicate severity through a coordinated icon badge + confirm button color pair (amber for warning, red for danger, blue for info). Never mix badge and button colors from different severity levels.
3. **Mandatory vs. dismissible** — Omit the top-right `ti-x` dismiss button when the user must make an explicit choice (e.g., session expiry Info dialogs). Include it whenever the user can safely abandon the action.
4. **Fixed width, not fluid** — Modals use fixed pixel-equivalent widths (`30rem` for confirmation dialogs, `40rem` for form modals) set via inline style. Do not stretch them to full viewport width; the constrained width keeps focus on the task.
5. **Scrollable body cap** — The form modal body must always carry `max-h-[65vh]` and `overflow-y-auto` so that tall forms scroll internally rather than pushing the footer off-screen.

## Accessibility

- The dialog container must carry `role="dialog"` and `aria-modal="true"` so screen readers announce the overlay boundary and restrict virtual cursor movement to the modal.
- `aria-labelledby` must reference the heading element (the title `<div>` or `<h6>`) so screen readers announce the dialog's purpose when it opens.
- Focus must move to the first interactive element inside the modal on open, and return to the trigger element on close; the Escape key must trigger the cancel / dismiss action.
- Tab and Shift+Tab must cycle focus only within the open modal (focus trap); clicking the backdrop or pressing Escape should close dismissible modals.
- The confirm button for destructive variants should carry `aria-describedby` pointing to the supporting-text element so screen reader users hear the consequence before activating the action.

## Related Components

- [Drawer Panel](./drawer-panel.md) — A slide-in side panel that surfaces detail views and longer forms without fully blocking the underlying page; prefer it when the user needs to reference page context alongside the overlay content.
- [Expansion Panel](./expansion-panel.md) — An in-page collapsible section for supplementary content that does not require a blocking decision or an isolated focus context.
