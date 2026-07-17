# hero

Personal website built with [Hugo](https://gohugo.io/) (extended) and the
[Blowfish](https://blowfish.page/) theme, deployed to GitHub Pages.

## Quick start

```bash
# Clone WITH the theme submodule
git clone --recurse-submodules https://github.com/hamurana/hero.git
cd hero

# Serve locally with live reload (includes drafts)
hugo server -D
# → http://localhost:1313/hero/

# Production build into public/
hugo --gc --minify
```

Requires **Hugo extended** (Blowfish needs it): `brew install hugo`.

## Creating content

```bash
hugo new content posts/my-post/index.md
```

Put a `featured.jpg` next to a post's `index.md` to give it a hero/thumbnail
image.

## Where the look-and-feel is controlled

| File | Controls |
| --- | --- |
| [config/_default/params.toml](config/_default/params.toml) ⭐ | Colour scheme, light/dark mode, header & footer style, homepage layout, what metadata articles/lists show |
| [config/_default/languages.en.toml](config/_default/languages.en.toml) | Site title, author name/avatar/bio/social links |
| [config/_default/menus.en.toml](config/_default/menus.en.toml) | Header and footer navigation |
| [config/_default/markup.toml](config/_default/markup.toml) | Code-block highlighting, table-of-contents depth |
| [config/_default/hugo.toml](config/_default/hugo.toml) | Base URL, taxonomies, search output, related content |
| [assets/css/custom.css](assets/css/custom.css) | Free-form CSS overrides (loaded after theme styles) |

Every file is commented inline — open it and the options explain themselves.
Any `[article]` option can also be overridden per page via front matter.

## Deployment

Pushing to `main` triggers
[.github/workflows/gh-pages.yml](.github/workflows/gh-pages.yml), which builds
the site and publishes it to **https://hamurana.github.io/hero/**.

One-time setup: on GitHub, go to **Settings → Pages** and set
*Build and deployment → Source* to **GitHub Actions**.

## Updating the theme

Blowfish is a git submodule at `themes/blowfish`:

```bash
git submodule update --remote --merge themes/blowfish
```
