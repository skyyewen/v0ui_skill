# v0ui_skill

> A v0-like frontend constraint skill for generating modern, polished React/Next.js/Tailwind/shadcn UI.

## Overview

`v0ui_skill` provides the `v0-frontend-constraints` skill. It helps an AI coding agent produce frontend work with tighter defaults: existing design systems first, component primitives, Tailwind tokens, responsive layouts, complete UI states, and browser verification.

The goal is not to copy v0. The goal is to reproduce the useful constraint pattern behind v0-style output.

## Install

```bash
npx skills add skyyewen/v0ui_skill
```

## Usage

Invoke the skill from a coding agent that supports skills:

```text
@v0ui build a SaaS dashboard for subscription metrics
```

```text
$v0ui redesign this settings page with shadcn/ui and Tailwind
```

```text
Use v0-frontend-constraints to build this frontend.
```

## What It Enforces

- React/Next.js, Tailwind, shadcn/ui, Radix, and lucide-react as preferred defaults when no stack exists
- Existing project conventions before new abstractions
- Component primitives before custom controls
- Tokens for color, spacing, radius, border, and shadow
- Dense, utilitarian layouts for SaaS/admin/product tools
- Real visual assets for sites and games when useful
- Complete hover, focus, disabled, loading, empty, error, and selected states
- Desktop and mobile browser verification before completion

## Directory Structure

```text
v0ui_skill/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── v0-frontend-rules.md
```

## License

MIT
