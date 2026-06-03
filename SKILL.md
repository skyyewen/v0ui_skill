---
name: v0ui
description: Use when building, redesigning, or modifying frontend web apps, pages, dashboards, SaaS/admin tools, forms, tables, settings screens, landing pages, or interactive tools where the user wants v0-like modern UI quality, React, Next.js, Tailwind, shadcn/ui, responsive polish, or strict frontend generation constraints.
---

# V0 Frontend Constraints

Create modern, polished, v0-like frontend work by narrowing the design space: reuse the existing stack, use the required greenfield stack when no stack exists, build a real shadcn-compatible component layer, rely on design tokens, apply proven layout patterns, include Radix state-driven motion and real interaction states, and verify the rendered UI.

Always read `references/v0-frontend-rules.md` before implementing or reviewing frontend UI. That file is the source of truth for stack defaults, layout patterns, component discipline, visual guardrails, and verification.

## Expected Invocation

Use this skill for requests like:

- `@v0ui build a SaaS dashboard`
- `$v0ui redesign this settings page`
- `Use $v0ui for this UI`
- `make this look like v0`
- `build a modern shadcn/Tailwind frontend`

If the user invokes `@v0ui` or `$v0ui`, treat the rest of the message as the frontend brief to execute.

## Workflow

1. Inspect the existing project stack, design system, components, tokens, routes, and styling conventions.
2. Classify the surface as product app, admin/internal tool, marketing page, game, visual tool, or content site.
3. Follow `references/v0-frontend-rules.md` for the matching surface.
4. If no frontend stack exists, scaffold or create the required React/Next.js + TypeScript + Tailwind CSS + shadcn-compatible stack before implementing UI.
5. Create or reuse local shadcn-compatible components for the primitives the UI actually uses, such as button, badge, card, input, label, select, textarea, dialog/sheet, tabs, tooltip, and separator.
6. Wrap Radix primitives inside `components/ui/*`; do not import Radix primitives directly in app/page feature surfaces unless you are editing the wrapper itself.
7. Prefer existing components and tokens before adding custom CSS or extra dependencies.
8. Implement complete responsive UI, including empty, loading, error, hover, focus, disabled, selected, open, closed, and transition states when relevant.
9. Run the project and inspect the result in desktop and mobile viewports before claiming completion.

## Non-Negotiables

- Do not invent a new design system when the repo already has one.
- Do not ship generic AI UI: random gradient blobs, nested cards, one-hue palettes, oversized decoration, clipped text, or missing states.
- Do not create a landing page when the user asked for an app, tool, game, dashboard, or workflow surface.
- Do not hand-roll common controls when the stack has suitable primitives.
- Do not silently downgrade a greenfield `@v0ui` task to plain HTML/CSS/JS to avoid dependencies. Use the required stack, ask for permission if dependency installation is blocked, or state the blocker.
- Do not treat installed shadcn/Radix dependencies as shadcn compliance. App surfaces must use local shadcn-compatible UI components.
- Do not ship Dialog, Sheet, Drawer, Popover, Tooltip, or Tabs surfaces without accessible Radix behavior and visible `data-state` enter/exit transitions where the component opens or closes.
- Do not finish until the rendered UI has been checked for blank screens, overlap, overflow, broken assets, and responsive layout issues.
