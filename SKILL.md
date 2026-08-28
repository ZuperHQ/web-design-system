---
name: zuper-design-system
description: Use whenever designing, mocking up, or building a UI feature that should match Zuper's product design system. Triggers on "design a feature", "mock up a screen", "build this using Zuper components", or any UI request that should look like part of the Zuper product. Produces a rendered visual mockup built from real, documented Zuper component markup.
version: "1.0.0"
---

# Zuper Design System

A portable reference to Zuper's UI component library, framework-agnostic, for designing and mocking up features that look and feel like the Zuper product — without needing the Zuper webapp repo.

## When to use this skill

Use this whenever someone asks to design, mock up, sketch, or build a UI feature, screen, or flow that should match Zuper's product. This applies equally to an engineer wanting implementation-ready markup and a PM or designer wanting a visual mockup to review.

## How to design a feature

1. Read `references/components-index.md` to see the full list of available components and find the ones relevant to the requested feature.
2. For each relevant component, read `references/components/<name>.md` — it documents when to use it, its exact HTML structure and Tailwind classes, dos and don'ts, and accessibility requirements.
3. Read `references/usage-guide.md` for cross-component and app-wide patterns (for example: every page needs a breadcrumb, tables are the only list pattern, etc.).
4. Assemble a single, complete HTML page using **only** the markup and classes documented in the component references. Never invent classes, colors, shapes, or structure that aren't shown in the docs.
5. Render the assembled HTML as a visual artifact so the result is immediately visible. If artifact rendering isn't available in the current context, output the raw HTML instead.

## Forbidden patterns

- Raw hex color values inline (`style="color: #..."`) — use the documented color tokens instead.
- Arbitrary Tailwind color shades not named in the component docs (e.g. `bg-blue-400` for a state that has a documented token).
- Custom `border-radius` values outside the documented tokens (`rounded-lg`, `rounded-md`, etc.).
- Custom shimmer/loading animations — use the documented `animate-shimmer` pattern from `references/components/loading-shimmer.md`.

## Full-page reference

`references/zuper-components.html` renders every component together on one page, including composite/assembled examples (e.g. a full record detail layout). Use it when a single component doc doesn't show how components combine, or to sanity-check that an assembled mockup's visual rhythm (spacing, alignment) matches the rest of the system.
