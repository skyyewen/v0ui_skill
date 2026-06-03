# V0 Frontend Rules

## Core Principle

Make the output modern by controlling defaults. v0-like quality comes from consistent component systems, design tokens, familiar layout patterns, restrained visual decisions, complete states, and rendered verification.

## V0-Inspired Output Contract

Use v0's useful constraints as a project-safe contract, not as a platform clone.

- Deliver complete, runnable UI changes. Do not leave TODOs, partial snippets, dead primary actions, or comments asking the user to fill in missing code.
- Before implementing a React component or page, decide the structure, accessibility, styling, responsive behavior, media, dependencies, and runtime limits.
- Prefer one cohesive implementation path. Avoid scattering the requested UI across unnecessary files or abstractions.
- Use the same language as the user's brief for visible UI copy unless the product already uses another language.
- Escape JSX text that contains `<`, `>`, `{`, `}`, or backticks so rendered content does not break the component.
- Use type-only imports for TypeScript types, such as `import type` or `import { type Foo }`, when supported by the codebase.
- Prefer native Web APIs and browser features when they are sufficient.
- Treat v0 preview rules as inspiration only. Do not copy v0-only MDX block metadata, forced `Component` default exports, `/placeholder.svg` URLs, Vercel Blob-only media rules, blanket fetch bans, or blanket dynamic import bans into real projects.

## Stack Defaults

Use the existing project stack first. Do not migrate frameworks or styling systems unless the user asks.

If there is no existing frontend stack, this is a greenfield frontend. The default stack is required, not optional:

- React or Next.js with TypeScript
- Tailwind CSS
- shadcn/ui or an equivalent local component system
- Radix primitives for accessible behavior
- lucide-react for common icons
- CSS variables or Tailwind theme tokens for colors, radius, spacing, and shadows

Do not deliver plain HTML/CSS/JS for a greenfield `@v0ui` task unless the user explicitly requests static/no-dependency output.

If installing or scaffolding dependencies is blocked by network, package-manager, permission, or environment limits:

1. Try the needed command through the normal approval/escalation flow.
2. If it is still blocked, stop and report the blocker.
3. Do not silently substitute a lower-stack implementation.

When an existing app already uses plain HTML/CSS/JS, preserve that stack unless the user asks for a React/Tailwind migration.

## Surface Classification

Choose the correct UI mode before coding:

| Surface | Default direction |
| --- | --- |
| SaaS, CRM, admin, internal tool | Dense, quiet, utilitarian, easy to scan, optimized for repeated work |
| Settings, forms, onboarding | Clear hierarchy, strong validation, stable controls, obvious progress |
| Data-heavy dashboard | Tables, filters, summaries, tabs, charts only when useful |
| Marketing or landing page | Strong first-viewport signal, real product/place/person imagery, clear conversion path |
| Game or visual tool | Actual usable experience first, expressive visuals, stable controls |
| Content site | Readability, navigation, search/discovery, restrained decoration |

If the brief is ambiguous, infer from user goals and the current app. Ask only when choosing wrong would force a major rewrite.

## Component Discipline

Prefer component primitives over custom markup:

- Buttons: use icon-only or icon + short label when the action is familiar.
- Forms: use labels, helper text, validation, errors, disabled states, and clear submit behavior.
- Tables: include sorting/filter affordances, empty states, pagination or scrolling constraints when needed.
- Navigation: include active states and predictable hierarchy.
- Dialogs and drawers: include title, description when useful, primary action, cancel/close path, focus behavior.
- Settings: use toggles for binary options, selects/menus for option sets, sliders/inputs for numeric values, segmented controls for modes.
- Toolbars: use icons with tooltips for familiar actions.

Use lucide-react icons when available. Do not manually draw icons unless the app already uses a custom icon system.

## Accessibility

- Use semantic landmarks such as `main`, `header`, `nav`, `section`, `aside`, and `footer` when they match the page structure.
- Connect labels to form controls with `htmlFor` and `id`, or use accessible component-library equivalents.
- Add ARIA roles and attributes only when native semantics are insufficient.
- Include `aria-live` for dynamic status updates such as timers, async results, toast-like inline status, or validation summaries.
- Use `sr-only` text for icon-only buttons or controls whose visual label is not descriptive enough.
- Add useful `alt` text for informative images. Use empty alt text only for decorative images.
- Preserve visible focus states and keyboard reachability for every interactive control.

## Layout Rules

- Use stable dimensions for fixed-format elements such as boards, toolbars, grids, counters, and tiles.
- Use responsive constraints: `minmax`, `max-width`, `aspect-ratio`, `overflow-auto`, and breakpoint-specific layout changes.
- Keep page sections unframed. Use cards only for repeated items, modals, and genuinely framed tools.
- Do not put cards inside cards.
- Avoid oversized hero sections for operational tools.
- For apps and tools, make the primary workflow visible on the first screen.
- For landing pages, make the brand, product, place, person, or offer the first-viewport signal and leave a hint of the next section visible.
- Match text size to container size. Use compact headings inside panels, cards, sidebars, dashboards, and tool surfaces.

## Visual Rules

- Use tokens for color, border, radius, shadow, and spacing.
- Prefer neutral surfaces with one intentional accent color.
- Avoid one-note palettes dominated by a single hue family.
- Avoid default blue or indigo as the primary visual identity unless the project brand, existing tokens, or user request calls for it.
- Avoid default purple/purple-blue gradient aesthetics unless the product brand requires it.
- Avoid decorative gradient orbs, blobs, and bokeh backgrounds.
- Avoid pure black text on pure white when a softer foreground token exists.
- Keep shadows subtle; if a shadow is visually loud, reduce it or use border/surface contrast instead.
- Do not use negative letter spacing.
- Do not scale font size with viewport width.
- Text must not overflow, clip, overlap, or occlude controls at mobile or desktop sizes.

## Motion And Interaction

Use motion only when it clarifies state or improves perceived quality.

- Add hover, focus-visible, active, selected, disabled, loading, success, error, and empty states when relevant.
- Keep transitions short and consistent.
- Avoid stacking many micro-animations on the same surface.
- Respect reduced-motion patterns if the codebase already supports them.
- Loading states should preserve layout size to avoid shift.

## Data And Content Completeness

Mock data should make the UI feel real enough to evaluate:

- Use realistic names, counts, dates, statuses, and labels.
- Include at least one empty or edge state for workflows that can be empty.
- Include error and validation messages for forms.
- Avoid placeholder text like TODO, lorem ipsum, or "coming soon" unless the user asks for placeholder content.

## Images And Assets

Websites and games should use visual assets when visual inspection matters.

- Prefer actual product/place/object/person media when available.
- Use generated or searched bitmap images when a specific visual is needed and no repo asset exists.
- Use project-local placeholders or existing asset conventions. Do not hard-code v0-specific placeholder paths unless the app already supports them.
- Avoid dark, blurred, cropped, stock-like, or purely atmospheric media when users need to inspect the subject.
- Use stable aspect ratios and object-fit rules so media cannot break the layout.
- Do not use inline SVG illustrations as a substitute for real media unless the project style is explicitly vector-first.
- Avoid iframes, videos, or heavy embeds unless the user explicitly needs them and the target environment supports them.

## Implementation Rules

- Preserve the repo's architecture, routing, state management, styling conventions, and import aliases.
- Keep edits scoped to the requested frontend surface.
- Prefer small local helpers over broad abstractions unless an established pattern exists.
- Use semantic HTML and accessible labels.
- Keep client/server boundaries correct in Next.js. Use `"use client"` only where interactivity requires it.
- Avoid secrets or backend assumptions when building static UI prototypes. Use fetch/network calls only when the project already has the data layer or the user explicitly asks for real integration.
- Use dynamic imports or lazy loading only when they fit the project framework and solve a real bundle, route, or rendering issue.
- Do not leave TODO comments, dead controls, or nonfunctional primary actions without an explicit reason.

## Verification

Before final response:

1. Run the relevant build, lint, typecheck, test, or dev server command when available and practical.
2. Open the app in a browser when the target is a local frontend.
3. Check at least one desktop viewport and one mobile viewport.
4. Look for blank screens, console errors, broken imports, broken icons, missing assets, overflow, overlap, clipped text, layout shift, and unreachable controls.
5. Fix visual or runtime defects before claiming the UI is complete.

If verification cannot run, state the exact command that failed or the environmental blocker.

## Common Mistakes

| Mistake | Fix |
| --- | --- |
| Starting with decoration | Start with workflow, hierarchy, controls, and states |
| Avoiding dependencies by outputting static HTML in a greenfield task | Use the required React/Next.js, TypeScript, Tailwind, and shadcn-compatible stack or report the installation blocker |
| Building custom controls from scratch | Use existing primitives or shadcn/Radix equivalents |
| Making every surface a card | Use full-width sections and reserve cards for repeated items |
| Using a single color family everywhere | Use neutral surfaces plus one intentional accent |
| Ignoring mobile until the end | Design responsive structure while implementing |
| Shipping a screenshot-good but unusable UI | Add states, interactions, labels, and verification |
| Treating "modern" as gradients | Treat modern as consistency, spacing, hierarchy, and restraint |

## Quick Checklist

- Existing stack respected
- Greenfield stack requirement followed
- Output contract followed
- Component primitives reused
- Accessibility basics covered
- Tokens used for theme values
- Responsive desktop and mobile layout
- Complete states for interactive controls
- No nested cards or decorative blobs
- No text overflow or overlap
- Realistic content and edge states
- Browser verification completed
