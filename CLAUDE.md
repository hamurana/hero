# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Neo Wang's personal website built with **Hugo (extended)** and the **Blowfish**
theme, deployed to GitHub Pages at **https://ncw.co.nz/** (custom domain;
repo: hamurana/hero — the old https://hamurana.github.io/hero/ URL redirects).

The theme lives at `themes/blowfish` as a **git submodule** — never edit files
under `themes/`; override via `config/_default/`, `assets/css/custom.css`, or
by copying a template into `layouts/`.

## Commands

```bash
hugo server -D                          # local dev server with drafts → http://localhost:1313/
hugo --gc --minify                      # production build → public/
hugo new content posts/<slug>/index.md  # new post (page bundle)
git submodule update --remote --merge themes/blowfish  # update theme
```

Hugo extended is required (Blowfish needs it for asset processing).

## Design intent

The site's look-and-feel deliberately mirrors **blowfish.page** (the theme's
docs site), whose source is the theme's own `themes/blowfish/exampleSite/`.
The config was derived from `exampleSite/config/_default/` — but **only the
visual configuration**: content, menus, and identity are Neo's own. Keep it
that way; don't reintroduce exampleSite content, extra languages, or Blowfish
branding.

Deliberate deviations from blowfish.page (all commented in params.toml):
- Article dates shown, lists sorted by date and grouped by year (blog, not docs)
- `pagerSize = 12` instead of 102
- View counters off (`showViews = false`) — need a user-owned Firebase project
- Buy-me-a-coffee widget disabled, Google Analytics and Firebase IDs removed:
  the exampleSite ships the theme author's personal account IDs — **never copy
  those back in**

Homepage uses the built-in `background` layout (fullscreen animated
`background.svg` from theme assets with profile overlay) — blowfish.page's
`custom` layout only adds its layout-switcher demo and sponsors sections on top
of the same look.

## Configuration layout

Hugo config is split across `config/_default/` (commented inline):

- `hugo.toml` — engine config: baseURL, taxonomies, outputs (the homepage
  `JSON` output powers Blowfish search — don't remove it)
- `params.toml` — main look-and-feel: colorScheme, dark mode default,
  header/footer, homepage layout, article/list display toggles
- `languages.en.toml` — site title ("Hero") + author profile (Neo Wang);
  commented slots for a header logo and avatar image
- `menus.en.toml` — header nav (Posts, About, Tags, GitHub icon) + footer
- `markup.toml` — Goldmark with block attributes and math passthrough;
  `highlight.noClasses = false` is required for the theme's code styling

Per-page front matter overrides any `[article]`/`[list]` param (see
`content/about.md` for an example).

## Table of Contents

`showTableOfContents = true` under `[article]` in `params.toml` turns the ToC
on for all posts by default; override per-post with `showTableOfContents:
false/true` in front matter. `smartTOC = true` (also in `params.toml`) enables
scroll-spy active-heading highlighting via the theme's own JS — no extra work
needed.

`markup.toml` sets `[tableOfContents] startLevel = 2, endLevel = 4`. **Post
headings must start at `##` (H2)**, not `###` — if the first heading is below
`startLevel`, Goldmark wraps the whole list in an extra empty `<li>`, breaking
the ToC's indentation. `##` for top-level sections, `###` for subsections.

`assets/css/custom.css` carries ToC-specific styling (leading `▸` marker per
link, hover/active-state color, monospace font) as a working example of the
override pattern — extend those rules rather than duplicating the `.toc`
selectors.

## Deployment

`.github/workflows/gh-pages.yml` builds and deploys on push to `main` using
the official GitHub Pages actions (`actions/configure-pages` supplies the
baseURL at build time). Checkout uses `submodules: recursive` — required for
the theme. GitHub Pages source must be set to "GitHub Actions" in repo
settings (one-time manual step); until then the workflow fails at the
"Configure Pages" step with a Pages-site-not-found error.

**Custom domain**: `ncw.co.nz`, DNS managed at **Hover** — apex A records to
the four GitHub Pages IPs (185.199.108–111.153), `www` CNAME to
`hamurana.github.io`. The domain is set in repo Settings → Pages (with
"Enforce HTTPS"); with Actions-based deploys it lives only in those settings —
no `CNAME` file in the repo. `actions/configure-pages` picks it up, so builds
get the right baseURL automatically.

## Known quirks

- Blowfish's declared Hugo compatibility range may lag the installed Hugo
  version, producing a `Module "blowfish" is not compatible` WARN at build
  time; it is harmless as long as the build succeeds.
- Blowfish resolves images from `assets/` (theme or site), not `static/` —
  e.g. `defaultBackgroundImage = "/img/background.svg"` resolves to
  `themes/blowfish/assets/img/background.svg`.
- In Claude Code's sandboxed Bash tool, `hugo server` binds inside the
  sandbox's own network namespace — it is **not** reachable from the actual
  GUI browser (e.g. opening `localhost:1313` in Safari fails to connect).
  Visual/UI verification can't rely on taking a screenshot of a locally
  launched browser; instead check rendered output via `curl`/`grep` on the
  HTML and compiled CSS bundle in `public/`, or ask the user for a
  screenshot.
