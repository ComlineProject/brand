# Comline brand

Single source of truth for the Comline mark, favicons, and colour tokens.
Every other repo (docs site, web apps, package registry frontend, READMEs)
**vendors a pinned copy** of the file it needs rather than linking here at
runtime — this repo is where the canonical version lives and where changes
are made first.

## Contents

```
logo/
  mark.svg          the mark, fill="currentColor" — inherits the surrounding text colour
  mark-tomato.svg   the mark in Comline tomato (#E5442E), for light backgrounds
  mark-cream.svg    the mark in cream (#FFE1D8), for tomato / dark backgrounds
favicon/
  favicon.svg       the mark in cream on a tomato rounded-square — browser tabs
  favicon.png       raster fallback for clients that don't take SVG favicons
third-party/
  github-mark-dark.svg / github-mark-light.svg   GitHub's Octocat (their asset, their licence)
  gitlab-mark.svg                                GitLab's mark (their asset, their licence)
tokens.json         colour tokens (tomato, cream)
```

## Which file where

| Context | File |
|---|---|
| Header/logo on a coloured (tomato or dark) surface | `logo/mark-cream.svg` |
| Logo on a white / light surface | `logo/mark-tomato.svg` |
| Inline in body text, buttons, anywhere the colour should follow text | `logo/mark.svg` |
| Browser tab / bookmark icon | `favicon/favicon.svg`, with `favicon/favicon.png` as fallback |
| "View on GitHub / GitLab" links | the matching file in `third-party/` |

## Colours

| Token | Hex | Use |
|---|---|---|
| tomato | `#E5442E` | primary — logo on light, favicon background, accents |
| cream | `#FFE1D8` | the mark on tomato/dark, favicon foreground |

Also in `tokens.json` for tooling.

## The mark

A 4×4 grid of rounded squares on a `0 0 100 100` viewBox, one row left
implicit as negative space. It carries `role="img"` and
`aria-label="Comline"` so it announces correctly when used on its own; drop
the `aria-label` (and add `aria-hidden="true"`) when it sits next to the
word "Comline" in text.

## Don'ts

- Don't recolour the mark outside the two brand colours (or `currentColor`).
- Don't add a background panel to `mark*.svg` — the favicon is the only
  version with a container.
- Don't distort: scale uniformly, keep the viewBox.
- Don't hotlink these files across repos. Copy the one you need in and note
  the commit you took it from.

## Licensing

The Comline name and mark are **trademarks**, not open-licensed assets — see
[`TRADEMARK.md`](TRADEMARK.md). Use them to *refer to* the project freely;
don't use them as the identity of your own product or fork. This is the half
of "a fork can copy the code but can't *be* Comline" that the code licenses
don't cover. Rationale:
[docs → Design → Licensing](https://github.com/ComlineProject/docs).

## Updating a consumer

When a file here changes, bump the vendored copy in each consumer:

- `docs` — `docs/docs/docs/assets/` (`mkdocs.yml` `theme.logo` / `theme.favicon`)
- `package-management/package-registry-frontend` — `static/images/comline/`, `static/favicon.*`
- `web/*` — per-app `static/` (SvelteKit)
