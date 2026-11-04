# Color Guidelines

[global.css](../src/styles/global.css) defines the current color values in its
`@theme` block. Refer to that source when customizing the palette.

## Token usage

| Token | Purpose | Example utility |
| --- | --- | --- |
| `primary` | Brand identity and emphasis | `bg-primary` |
| `secondary` | Main solid buttons and supporting actions | `bg-secondary` |
| `accent` | Highlights and emphasis | `bg-accent` |
| `danger` | Destructive actions | `bg-danger` |
| `danger-hover` / `danger-active` | Destructive action states | `hover:bg-danger-hover` |
| `light` | Light surfaces and text on dark surfaces | `bg-light` / `text-light` |
| `dark` | Dark surfaces and text on light surfaces | `bg-dark` / `text-dark` |

Color utilities can also be used for borders, focus rings, and other visual
states. Pick foreground and background combinations based on the rendered
contrast; a palette is not automatically accessible in every combination.

## Customizing the palette

Update the existing declarations in `global.css` so components that use the
semantic tokens inherit the change. When adding a reusable semantic color,
define its token there as well.

The light and dark colors derive from the primary color with `color-mix()`.
Review those surfaces and their text colors after changing the primary color.

For the project's styling rules and UI checks, read the
[UI conventions](./coding-standards.md).
