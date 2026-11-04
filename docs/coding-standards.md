# UI conventions

Use these conventions when changing components, layouts, or styles.

## Design tokens

- [global.css](../src/styles/global.css) owns the color tokens and semantic
  typography utilities. Change reusable tokens there rather than copying values
  into components or documentation.
- Use project color tokens instead of generic Tailwind palettes. White, black,
  and transparent are allowed where appropriate for contrast or composition.
- For content, use `text-h1` through `text-h6`, `text-p`, `text-lead`, `text-small`,
  `text-quote`, and `text-eyebrow` as appropriate. Keep deliberate component size
  variants, such as button sizes, within the component's variant API.

## Layout and spacing

- Preserve the existing page gutters: `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`.
- Use `space-y-*` for stacked content and `gap-*` for flex or grid layouts.
- Use padding for component boundaries and margins for positioning when needed.
  Choose spacing values consistent with the surrounding component.

## Components and interactivity

- Prefer static `.astro` components. Use native browser scripts for simple
  behavior; add framework components and hydration when the feature needs them.
- Reuse shared prop types from `src/types/` where they apply. Keep each prop
  contract defined in one place rather than maintaining duplicate interfaces.
- Preserve public prop names, defaults, and variants unless the task changes
  them. Document API changes under `docs/components/` and link new component
  documentation from the [documentation index](README.md).
- Match the existing icon style. Inline SVGs and reusable SVG components are
  supported; select an icon library only when the task requires one.

## UI verification

For changed UI, inspect the affected pages at narrow and wide viewport widths.
Check text wrapping, overflow, relevant component variants, and keyboard use.

Prefer native HTML semantics and visible focus states. Add ARIA for names or
states that native semantics do not express; hide decorative icons from
assistive technology. Check contrast for the actual foreground/background pair,
including hover, focus, and disabled states where applicable. A token name alone
does not establish accessible contrast.

Existing examples contain styling and prop-type inconsistencies. Apply these
conventions to the requested changes and keep unrelated cleanup scoped separately.
