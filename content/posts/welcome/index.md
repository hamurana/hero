---
title: "Welcome to Hero"
date: 2026-07-17
description: "A first post showing the front matter options that shape how an article looks."
summary: "How this site is put together, and where to change how it looks."
tags: ["hugo", "blowfish"]
categories: ["meta"]
---

This is a sample post. Delete it once you have real content.

## Where the look-and-feel lives

| What you want to change | File to edit |
| --- | --- |
| Colours, dark mode, header/footer style, homepage layout | `config/_default/params.toml` |
| Site title, author name/avatar/social links | `config/_default/languages.en.toml` |
| Navigation menus | `config/_default/menus.en.toml` |
| Code highlighting, TOC depth | `config/_default/markup.toml` |
| Free-form CSS tweaks | `assets/css/custom.css` |

## Code blocks

Syntax highlighting and the copy button come from `markup.toml` +
`enableCodeCopy` in `params.toml`:

```go
func main() {
    fmt.Println("Hello, Blowfish!")
}
```

## Per-post appearance

Any `[article]` option from `params.toml` can be overridden per post in the
front matter — for example `showHero`, `heroStyle`, or `showTableOfContents`.
To give a post a hero/thumbnail image, drop a file named `featured.*`
(e.g. `featured.jpg`) into the post's folder next to `index.md`.
