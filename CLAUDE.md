# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A static site published via GitHub Pages at https://memfrag.github.io/guides/. It hosts standalone coding guides and architecture documents as plain HTML pages, with one index page listing them all. There is no build step, framework, or package manager — just HTML, CSS, and a small amount of vanilla JS.

## Local preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000/. No install step is needed first.

## Architecture

- `index.html` is the landing page. It does not hardcode the list of guides — it fetches `guides.json` at runtime and renders each entry into `.guide-list`.
- `guides.json` is the single source of truth for what appears on the index. Each entry needs `title`, `path`, `description`, and `updated` (used for sort order, newest first); `tags` is optional.
- `docs/` holds one HTML file per guide. Each guide is a fully standalone page (own `<head>`, own content). Guides come in two flavours: **shared-style** pages that link `../assets/style.css` and reuse its classes, and **self-styled** pages that carry their own embedded design and ignore the shared stylesheet entirely (e.g. `docs/swiftui-alignment.html`). Both are fine — don't retrofit a self-styled page onto the shared stylesheet.
- The one element every guide must have, whichever flavour it is, is `<a class="back-link" href="../index.html">&larr; All guides</a>` near the top of the content. A shared-style page gets it for free from `assets/style.css`; a self-styled page should define its own `.back-link` rule in its embedded CSS, matching that page's own type and colours rather than importing the shared one.
- `assets/style.css` is the shared stylesheet for the index and any guide that opts into it. It defines light/dark theming via `prefers-color-scheme` and shared classes (`.guide-list`, `.tag`, `.back-link`, etc.).
- `.nojekyll` is present so GitHub Pages serves files as-is instead of running Jekyll processing.

## Adding a new guide

1. Either copy `docs/example-guide.html` as a starting point (shared style), or write a fully self-styled page — see the `docs/` note above.
2. Make sure the page has a `.back-link` to `../index.html`, styled to fit that page.
3. Add a matching entry to `guides.json` (`title`, `path`, `description`, `tags`, `updated`).
4. Commit and push — the index page picks up the new entry automatically, no other file needs to change.
