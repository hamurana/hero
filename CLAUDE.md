# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal website built with **Hugo (extended)** and the **Blowfish** theme,
deployed to GitHub Pages at https://hamurana.github.io/hero/.

The theme lives at `themes/blowfish` as a **git submodule** — never edit files
under `themes/`; override via `config/_default/`, `assets/css/custom.css`, or
by copying a template into `layouts/`.

## Commands

```bash
hugo server -D                          # local dev server with drafts
hugo --gc --minify                      # production build → public/
hugo new content posts/<slug>/index.md  # new post (page bundle)
git submodule update --remote --merge themes/blowfish  # update theme
```

Hugo extended is required (Blowfish needs it for asset processing).

## Configuration layout

Hugo config is split across `config/_default/` (all files are heavily
commented inline):

- `hugo.toml` — engine config: baseURL, taxonomies, outputs (the homepage
  `JSON` output powers Blowfish search — don't remove it)
- `params.toml` — main look-and-feel: colorScheme, dark mode, header/footer,
  homepage layout, article/list display toggles
- `languages.en.toml` — site title + author profile block
- `menus.en.toml` — header/footer navigation
- `markup.toml` — Goldmark/highlighting; `highlight.noClasses = false` is
  required for the theme's code styling

Per-page front matter overrides any `[article]`/`[list]` param.

## Deployment

`.github/workflows/gh-pages.yml` builds and deploys on push to `main` using
the official GitHub Pages actions (`actions/configure-pages` supplies the
baseURL at build time). Checkout uses `submodules: recursive` — required for
the theme. GitHub Pages source must be set to "GitHub Actions" in repo
settings (one-time manual step).

## Known quirks

- Blowfish's declared Hugo compatibility range may lag the installed Hugo
  version, producing a `Module "blowfish" is not compatible` WARN at build
  time; it is harmless as long as the build succeeds.
