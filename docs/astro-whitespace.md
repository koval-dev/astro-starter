# Astro whitespace rendering

Investigated on November 4, 2026, with Astro 7.4.5 installed.

## What changed

Astro 7 changed the default `compressHTML` from `true` to `'jsx'`.
With the new default, inline content separated only by a source newline can
render without a separating space. Astro's migration guide demonstrates this
with `<span>hello</span>` and `<em>world</em>` on separate lines rendering as
`helloworld`. This is a documented breaking change, rather than intermittent
browser behavior. [Astro v7 migration guide](https://docs.astro.build/en/guides/upgrade-to/v7/#new-default-whitespace-handling-compresshtml-jsx),
[implementation PR #16965](https://github.com/withastro/astro/pull/16965).

The configuration reference distinguishes three modes: `'jsx'` uses JSX
whitespace rules, `true` uses HTML-aware compression, and `false` preserves
source whitespace. The setting applies to development and production builds.
Ordinary same-line spaces are preserved by `'jsx'`; a source newline is not a
reliable separator at an expression or inline-element boundary.
[Astro configuration reference](https://docs.astro.build/en/reference/configuration-reference/#compresshtml).

## Evidence in this starter

- `package.json` declares `astro: ^7.4.5`; the installed version is 7.4.5.
- `astro.config.mjs` does not override `compressHTML`.
- The installed default in
  `node_modules/astro/dist/core/config/schemas/defaults.js` is `'jsx'`.
- Before the fix, `Footer.astro` put `{currentYear}` and `{companyName}` on
  consecutive source lines. Both generated pages (`dist/index.html` and
  `dist/404.html`) contained `&copy; 2026Your Company. All rights reserved.`

These local observations match the documented Astro 7 change.

## Audit findings

The source and generated HTML audit found two missing separators:

| Location | Before correction | Required separator |
| --- | --- | --- |
| `src/components/Footer.astro` | `© 2026Your Company. All rights reserved.` | Between the year and company name |
| `src/components/TypographyExample.astro` | `It uses thetext-lead utility...` | Between `the` and the inline `text-lead` span |

Both depend on a source newline to separate adjacent inline content. The
correction adds an explicit `{" "}` at each boundary, retaining Astro's default
compression mode. The audit covered all ten `.astro` source files and both
generated pages. No other missing inline separators were found. Footer contact
lines use separate block elements, while buttons and social links use layout
spacing, so they do not need textual spaces between those elements.

## Verification

- A fresh build reproduced the original footer problem. Assertions on the
  generated copyright and typography text failed before the correction and
  passed afterward.
- A minimal compiler/rendering comparison produced `2026Your Company` with
  `compact: 'jsx'`, `2026 Your Company` with `compact: true`, and a retained
  newline with `compact: false`, isolating the whitespace mode as the cause.
- `npm run build` passed after both corrections. Rendered HTML assertions passed
  for the copyright on both pages and seven typography paragraphs containing
  inline markup.
- Direct compilation and rendering of the actual footer passed six prop cases:
  defaults, full contact details, social links, minimal company details, custom
  styling, and custom logo/additional HTML with an escaped company name. This
  includes the variants demonstrated by the unmounted `FooterExamples.astro`.
- Browser access was unavailable, so narrow/wide visual layout and keyboard
  checks could not be performed. The sandbox also blocked HTTP requests to the
  local preview; output assertions inspected the built HTML files directly.

The assertions were ad hoc checks; no automated test runner or lint script is
configured. The build does not perform full TypeScript checking. A successful
build alone does not establish correct rendered spacing.

## Writing reliable inline text

Use explicit spaces at meaningful boundaries that span source lines:

```astro
&copy; {currentYear}{" "}
{companyName}. All rights reserved.
```

The same pattern applies to prose containing inline links, emphasis, spans, or
components. Astro recommends `{" "}` for missing separators; reverting globally
to `compressHTML: true` is an alternative when the previous behavior is wanted
throughout a project. [Astro v7 migration guide](https://docs.astro.build/en/guides/upgrade-to/v7/#new-default-whitespace-handling-compresshtml-jsx).

For formatting tools, the official Astro Prettier plugin exposes
`astroCompressHTML` to match the compiler mode. If a project overrides
`compressHTML`, keep the formatter's corresponding setting in sync so wrapping
does not change rendered text. [Astro Prettier plugin documentation](https://github.com/withastro/prettier-plugin-astro#astro-compress-html).
