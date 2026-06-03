---
name: v0ui
description: Use when building, redesigning, or modifying frontend web apps, pages, dashboards, SaaS/admin tools, forms, tables, settings screens, landing pages, or interactive tools where the user wants v0-like modern UI quality, React, Next.js, Tailwind, shadcn/ui, responsive polish, or strict frontend generation constraints.
---

# V0 Frontend Constraints

Create modern, polished, v0-like frontend work by narrowing the design space: reuse the existing stack, use the required greenfield stack when no stack exists, prefer component primitives, rely on design tokens, apply proven layout patterns, include real interaction states, and verify the rendered UI.

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
5. Prefer existing components and tokens before adding custom CSS or extra dependencies.
6. Implement complete responsive UI, including empty, loading, error, hover, focus, disabled, and selected states when relevant.
7. Run the project and inspect the result in desktop and mobile viewports before claiming completion.

## Non-Negotiables

- Do not invent a new design system when the repo already has one.
- Do not ship generic AI UI: random gradient blobs, nested cards, one-hue palettes, oversized decoration, clipped text, or missing states.
- Do not create a landing page when the user asked for an app, tool, game, dashboard, or workflow surface.
- Do not hand-roll common controls when the stack has suitable primitives.
- Do not silently downgrade a greenfield `@v0ui` task to plain HTML/CSS/JS to avoid dependencies. Use the required stack, ask for permission if dependency installation is blocked, or state the blocker.
- Do not finish until the rendered UI has been checked for blank screens, overlap, overflow, broken assets, and responsive layout issues.
