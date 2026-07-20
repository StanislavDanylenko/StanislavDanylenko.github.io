# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static personal portfolio/CV website deployed via GitHub Pages. No build step, no package manager, no framework — all content is hand-authored HTML.

## How to preview

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 8080
```

## Tech stack

- **Tailwind CSS** — Play CDN JS runtime (`js/vendor/tailwind.min.js`), no build step. Config is an inline `tailwind.config` block in `<head>`.
- **Alpine.js v3** — `js/vendor/alpine.min.js` (loaded with `defer`). Used for mobile menu toggle, bio collapse, and scroll-to-top visibility.
- **Bootstrap Icons v1.10.2** — `css/vendor/bootstrap-icons.min.css` + fonts at `css/vendor/fonts/`. Icon classes: `bi-*`.
- **Inter font** — local woff2 files at `css/font/inter/` (weights 400/600/700), declared via `@font-face` in `css/styles.css`.
- All vendor assets are local — no CDN requests at runtime.

## Structure

Everything lives in a single `index.html`. Sections are identified by `id="section-*"` anchors (in DOM order):

1. `section-summary` — name, bio, social links; Alpine collapse for full bio
2. `section-main-skills` — primary skills as divided list
3. `section-secondary-skills` — secondary/OPS/experience skills
4. `section-education` — university degrees
5. `section-languages` — spoken languages (side-by-side with education on desktop)
6. `section-work-experience` — 8 projects, each in a 3-column grid; `<span id="work-period">` is populated by inline JS
7. `section-other-activities` — articles + Java mentor role
8. `section-interests` — badge chips
9. `section-android` — two Android app cards

The page has two nav variants rendered in parallel:
- **Desktop sidebar** (`<aside>`, `hidden md:flex`, fixed left) — visible ≥768 px
- **Mobile navbar** (`<div x-data="{ open: false }"`, `md:hidden`, fixed top) — hamburger toggle via Alpine.js

Both navs list the same 9 section links in the same order. Keep them in sync when adding sections.

## Styling

- `css/styles.css` — only `@font-face` declarations (Inter + Montserrat). No other custom CSS.
- All visual styling is Tailwind utility classes directly in HTML.
- Color palette: `bg-slate-950` page, `bg-slate-900` sidebar, `bg-slate-800` section cards, `text-indigo-400` accent, `border-slate-700` dividers.
- `css/vendor/bootstrap.min.css` and `js/vendor/bootstrap.bundle.min.js` are kept on disk but not loaded.

## Content conventions

- All content changes happen in `index.html`.
- Section card pattern: `<section id="section-*" class="bg-slate-800 rounded-xl border border-slate-700 p-6">`.
- Section heading pattern: `<h2 class="text-xs font-semibold uppercase tracking-widest text-slate-400 mb-4">`.
- Work experience project entries use a `grid grid-cols-1 md:grid-cols-3` layout; the right column is `md:col-span-2`.
- Skills are plain list items with `divide-y divide-slate-700`; interest badges use `bg-indigo-950 text-indigo-300 border border-indigo-800 rounded-full`.
- `sitemap.xml` lists the single URL; update `<lastmod>` when making significant content changes.
