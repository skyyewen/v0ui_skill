# V0 Frontend Rules

## Core Principle

Make the output modern by controlling defaults. v0-like quality comes from consistent component systems, design tokens, familiar layout patterns, restrained visual decisions, complete states, state-driven motion, and rendered verification.

The default visual target is minimal commercial SaaS polish: white background, black or near-black text, neutral borders, generous whitespace, clean product panels, smooth transitions, and clear human-computer interaction feedback. Use restrained color accents for important states, brand marks, charts, and primary emphasis. Reserve pure-black filled controls for truly primary actions; ordinary selected navigation, step markers, filters, badges, and status chips should feel quiet.

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

## Minimal SaaS Visual Mode

Use this visual mode by default for `@v0ui` work.

- Color: default to a Vercel-inspired neutral palette, not a monochrome UI. When no existing theme overrides it, use a near-white app background around `#fafafa`, strong headings around `#261b17`, body/navigation text around `#575757`, white cards, quiet neutral borders, and token equivalents such as `background`, `foreground`, `zinc`, `neutral`, `muted`, `muted-foreground`, `border`, `card`, and `card-foreground`. Pure black should be a scarce emphasis color, not a general selected-state color.
- Primary actions: default to black or `zinc-950` with white text for the highest-priority command on the screen. Secondary actions should be neutral, outline, or ghost. Avoid multiple black-filled buttons unless they are genuinely equivalent primary commands.
- Navigation and tabs: active sidebar items, tabs, and segmented controls should usually use a light neutral selected row or pill (`muted`, `zinc-100`, `neutral-100`), dark text, subtle border or shadow, and neutral icons. Do not make ordinary navigation tabs black-filled just because they are selected.
- Workflow steps and chips: numbered steps, progress markers, status badges, filters, and informational chips should use neutral rings, borders, muted fills, or small accents. Do not use pure black filled circles or pills for passive ordering information.
- Accents: important positions should use small, purposeful color. Use restrained brand/status accents for logos, project avatars, product icons, active navigation marks, badges, charts, warnings, progress, or selected states. Avoid turning the whole chrome teal, blue, purple, green, or orange by default.
- Density: prefer calm, low-to-medium information density. Leave visible whitespace around the main workflow, but keep operational screens usable and scannable.
- Spacing: use generous page padding, panel padding, and grid gaps where the layout can support it. The UI should feel spacious, not sparse or unfinished.
- Cards and panels: favor clean SaaS panels with neutral borders, subtle shadows, and stable proportions. Use `rounded-lg`, `rounded-xl`, or the project's radius token by default; use `rounded-2xl` for large feature panels when it improves the composition.
- Composition: prefer a centered product workspace, clear sidebar/header navigation, and balanced grids over a compressed enterprise dashboard. Tables should appear when the task is truly data-heavy, not as the default visual answer.
- Interaction: every clickable surface should have visible hover, focus-visible, active, selected, disabled, loading, and open/closed feedback where relevant.
- Motion: use short, smooth transitions such as `transition-colors`, `transition-shadow`, `transition-transform`, `duration-150`, `duration-200`, and `ease-out`. Avoid abrupt state changes and avoid excessive animation.
- Shadows and borders: use subtle shadows and neutral borders. Let whitespace, hierarchy, and interaction feedback carry the design before adding decoration.

### Vercel-Inspired Neutral Palette

Use these values as a practical default when the project has no stronger theme tokens:

- App background: `#fafafa` or the closest `background` token.
- Card and input surfaces: white or the closest `card` token, with a quiet neutral border.
- Strong text, headings, primary labels: `#261b17`, `zinc-950`, `neutral-950`, or the closest `foreground` token.
- Body text, sidebar labels, descriptions, metadata: `#575757`, `zinc-600`, `neutral-600`, or the closest `muted-foreground` token.
- Disabled or tertiary text: a softer neutral such as `zinc-400` or `neutral-400`.

Do not force these exact hex values over an existing design system. Map them into the local CSS variables or Tailwind theme when possible.

### Semantic Icon And Accent Color

Neutral structure should not mean every icon is gray. Use color where it carries meaning or identity:

- Success, completed, synced, accepted: emerald or green icon/text accents.
- Pending, waiting, needs review, queued: amber or orange accents.
- Error, blocked, destructive, policy risk: red accents.
- Info, running, live, analytics, deploy/build activity: sky, cyan, or blue accents.
- AI, automation, generation, model, sparkle-like actions: violet, cyan, or a small brand accent when appropriate.
- Product marks, project avatars, integration logos, chart series, and progress indicators may be colorful even inside an otherwise neutral page.

Keep colored accents small and semantic: icon color, dot, thin ring, tiny badge, chart line, progress segment, or avatar fill. Do not make ordinary navigation, whole sidebars, panel backgrounds, or large empty decorative shapes colorful by default.

## Shadcn-Compatible Component Layer

Installing shadcn, Radix, Tailwind, or lucide dependencies is not enough. A greenfield React/Tailwind `@v0ui` result must expose and use a local shadcn-compatible component layer.

- Create or reuse `src/components/ui/` wrappers for the primitives actually used by the app.
- Minimum app/dashboard set: `button`, `badge`, `card`, `input`, `label`, `select`, `textarea`, `separator`, and either `dialog` or `sheet` when overlays are used. Add `tabs`, `tooltip`, `dropdown-menu`, `table`, or `form` when the surface needs them.
- Components should use Tailwind tokens, CSS variables, `cn`, `class-variance-authority` where useful, `forwardRef`, and `asChild` for composable interactive primitives.
- Feature files, route files, and `App.tsx` should import local UI components, not raw `@radix-ui/*` primitives. Direct Radix imports belong inside `components/ui/*` wrappers unless there is a documented exception.
- Do not call a UI shadcn-like if it only has one or two wrappers such as Button and Badge while the rest of the app uses hand-rolled controls.

## Dialog, Sheet, And Radix Motion

Overlays must feel like shadcn/Radix UI, not instant DOM toggles.

- Dialog, Sheet, Drawer, Popover, Dropdown, Tooltip, and Tabs must use accessible Radix behavior or an equivalent existing component primitive.
- Overlay/backdrop elements need open/closed fade transitions, such as `data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=open]:fade-in-0 data-[state=closed]:fade-out-0`.
- Center dialogs need open/closed fade, zoom, and slight slide transitions.
- Right-side sheets/drawers need `data-[state=open]:slide-in-from-right` and `data-[state=closed]:slide-out-to-right` or equivalent directional motion.
- Include duration/easing classes and reduced-motion compatibility when the project already supports it.
- If Tailwind animation classes require `tailwindcss-animate`, custom keyframes, or global CSS, add the configuration. Do not leave animation class names inert.
- Include close controls, title/description structure, focus management, escape/outside-click behavior through Radix, and scroll containment for long content.

## Surface Classification

Choose the correct UI mode before coding:

| Surface | Default direction |
| --- | --- |
| SaaS, CRM, admin, internal tool | Minimal commercial SaaS UI with white space, neutral panels, scannable workflows, rare black primary actions, quiet navigation states, and restrained accents |
| Settings, forms, onboarding | Clear hierarchy, generous spacing, strong validation, stable controls, obvious progress |
| Data-heavy dashboard | Summaries and filters first, tables only when useful, preserve breathing room even in dense views |
| Marketing or landing page | Strong first-viewport signal, real product/place/person imagery, spacious commercial composition, clear conversion path |
| Game or visual tool | Actual usable experience first, expressive visuals, stable controls |
| Content site | Readability, navigation, search/discovery, generous spacing, restrained decoration |

If the brief is ambiguous, infer from user goals and the current app. Ask only when choosing wrong would force a major rewrite.

## Component Discipline

Prefer component primitives over custom markup:

- Buttons: use icon-only or icon + short label when the action is familiar.
- Forms: use labels, helper text, validation, errors, disabled states, and clear submit behavior.
- Tables: include sorting/filter affordances, empty states, pagination or scrolling constraints when needed.
- Navigation: include active states and predictable hierarchy.
- Dialogs and drawers: use local Dialog/Sheet wrappers, include title, description when useful, primary action, cancel/close path, focus behavior, scroll containment, and visible open/close motion.
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
- Default to calm layouts with clear whitespace, fewer competing regions, and generous gutters.
- Keep page sections unframed. Use cards for repeated items, modals, genuinely framed tools, and product panels.
- Do not put cards inside cards.
- Avoid tiny packed dashboard tiles unless the user explicitly asks for a high-density operational tool.
- For apps and tools, make the primary workflow visible on the first screen.
- For landing pages, make the brand, product, place, person, or offer the first-viewport signal and leave a hint of the next section visible.
- Match text size to container size. Use compact headings inside panels, cards, sidebars, dashboards, and tool surfaces.

## Visual Rules

- Use tokens for color, border, radius, shadow, and spacing.
- Prefer `#fafafa`-like near-white app backgrounds, white cards, `#261b17`-like strong text, and `#575757`-like body text when no existing theme overrides them.
- Reserve black filled treatments for true primary actions; do not rely on pure black for ordinary selected or status states.
- Do not use pure-black filled backgrounds for ordinary selected navigation, sidebar tabs, segmented tabs, step numbers, filter chips, badges, or informational statuses. Use muted neutral surfaces, subtle borders, small accents, or font weight for these lower-priority states.
- For Vercel-like dashboards, keep the left navigation selected state light gray with dark text and a neutral icon; keep black buttons rare and action-oriented.
- For Vercel-like dashboards, use colorful semantic icons or tiny accents for statuses, project avatars, product marks, integrations, progress, warnings, success, and errors. Avoid making all icons black, gray, or the same neutral color when they represent different states.
- Use clean SaaS cards and panels with neutral borders, subtle shadows, and measured radius. Major panels should feel calm and useful, not like compact table containers.
- Prefer generous whitespace and calm information density over compact enterprise density.
- Avoid one-note palettes dominated by a single hue family.
- Avoid default blue or indigo as the primary visual identity unless the project brand, existing tokens, or user request calls for it.
- Avoid default purple/purple-blue gradient aesthetics unless the product brand requires it.
- Avoid green, teal, blue, purple, or orange as the default app chrome when no brand is specified.
- Avoid decorative gradient orbs, blobs, and bokeh backgrounds.
- Avoid pure black text on pure white when a softer foreground token exists.
- Keep shadows subtle; if a shadow is visually loud, reduce it or use border/surface contrast instead.
- Do not use negative letter spacing.
- Do not scale font size with viewport width.
- Text must not overflow, clip, overlap, or occlude controls at mobile or desktop sizes.

## Motion And Interaction

Use motion only when it clarifies state or improves perceived quality.

- Add hover, focus-visible, active, selected, disabled, loading, success, error, and empty states when relevant.
- Add `data-state` based transitions for Radix open/closed surfaces. No instant modal, drawer, popover, dropdown, or tooltip transitions unless the user explicitly asks for no motion.
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
- In React/Tailwind projects, route and feature files should import from the local `components/ui/*` layer instead of using raw Radix primitives directly.
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
5. Open and close every dialog, sheet, drawer, popover, dropdown, and tooltip touched by the work. Verify visible enter/exit transitions and focus behavior.
6. Search feature surfaces for direct `@radix-ui/*` imports. Keep them only in local UI wrappers or document the exception.
7. Verify Tailwind animation utilities or custom keyframes are configured when the UI uses animation class names.
8. Fix visual or runtime defects before claiming the UI is complete.

If verification cannot run, state the exact command that failed or the environmental blocker.

## Common Mistakes

| Mistake | Fix |
| --- | --- |
| Starting with decoration | Start with workflow, hierarchy, controls, and states |
| Building a colored dense admin dashboard for a shadcn/v0-like brief | Use the minimal SaaS visual mode: `#fafafa`-like background, soft dark text, neutral panels, clear whitespace, restrained semantic accents, and smooth interaction feedback |
| Making the interface look like a black-and-white wireframe | Keep the structural UI neutral, but add semantic color to status icons, project avatars, product marks, chart series, progress, warnings, success, errors, and AI actions |
| Making every selected item black-filled | Reserve black fill for true primary actions; use light neutral active states for sidebars, tabs, step indicators, filters, badges, and statuses |
| Avoiding dependencies by outputting static HTML in a greenfield task | Use the required React/Next.js, TypeScript, Tailwind, and shadcn-compatible stack or report the installation blocker |
| Installing shadcn/Radix dependencies but only creating Button and Badge | Build the local UI component layer for every primitive the surface uses |
| Using `@radix-ui/react-dialog` directly in `App.tsx` or route files | Wrap Radix in `components/ui/dialog` or `components/ui/sheet`, then import the wrapper |
| Shipping instant modals or drawers with no `data-state` animation | Add open/closed fade, zoom, or directional slide transitions and verify them in browser |
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
- Vercel-inspired neutral foundation used by default: `#fafafa`-like background, `#261b17`-like strong text, and `#575757`-like body text or equivalent tokens
- Black filled controls reserved for truly primary actions
- Navigation tabs, workflow steps, filters, badges, and status chips use quiet neutral selected states
- Restrained semantic color accents used for statuses, project avatars, product marks, charts, progress, warnings, success, errors, and AI actions
- Generous whitespace and calm information density present
- Smooth hover, focus, selected, loading, and open/closed feedback present
- Clean SaaS cards or panels used where cards are appropriate
- Shadcn-compatible local component layer present
- Component primitives reused through local UI wrappers
- Radix primitives wrapped in `components/ui/*`
- Dialog/sheet/popover enter and exit transitions verified
- Tailwind animation utilities or keyframes configured when needed
- Accessibility basics covered
- Tokens used for theme values
- Responsive desktop and mobile layout
- Complete states for interactive controls
- No nested cards or decorative blobs
- No text overflow or overlap
- Realistic content and edge states
- Browser verification completed
