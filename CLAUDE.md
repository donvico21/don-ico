# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A static single-page website for **Don Ico**, a protest music artist based in Singapore with Filipino diaspora roots. There is no build step, no package manager, and no framework — the entire site is `index.html`.

To preview: open `index.html` directly in a browser.

## Architecture

All CSS lives in an inline `<style>` block in `<head>`. All JavaScript lives in two inline `<script>` blocks at the bottom of `<body>`. Everything is self-contained in `index.html`.

### Page Sections (in order)

- `#hero` — full-viewport background (`Main Page Background.png`), artist name, CTA
- `#about` — bio + metadata sidebar
- `#music` — 3-column release card grid
- `#videos` — YouTube iframe embeds
- `#gratitude` — masonry photo grid of physical CD supporters
- `#stream` — streaming/download platform links
- `footer`

### Lightbox

A single `#lightbox` modal handles two use cases:
- **Gratitude Gallery**: clicking any `.gallery-item` opens the whole gallery; navigate with arrows, keyboard (`←`/`→`/`Esc`), or touch swipe.
- **Album artwork**: clicking a `.card-cover.has-gallery` opens only that release's images. Paths are stored as a JSON array in the element's `data-images` attribute (URL-encoded relative paths).

## Content Changes

### Adding a new release

Add an `<article class="card">` inside `.releases` in `#music`. Required parts:
- `.card-cover.has-gallery` with `data-images='[...]'` — JSON array of URL-encoded relative paths for artwork lightbox
- `.badge` span (use class `new` for the latest release)
- `.card-date`, `.card-title`, `.card-desc`
- `.tracklist` → `.tl-list` with `<li>` items (`tl-name`, optional `tl-feat`, `tl-dur`)
- `.card-actions` with `<a class="card-link">` per platform; add class `spotify`, `apple`, or `ytmusic` for colored variants

### Adding Gratitude Gallery photos

1. Place image in `Gratitude Gallery/`
2. Add a `<figure class="gallery-item" data-name="Name">` block inside `#galleryGrid` matching the existing pattern

## Design Tokens

| Variable | Value | Use |
|---|---|---|
| `--bg` | `#0c0c0c` | Page background |
| `--bg-card` | `#141414` | Card backgrounds |
| `--accent` | `#d4930a` | Gold accent |
| `--red` | `#b83030` | "New/Latest" badge |
| `--text` | `#f0ece4` | Primary text |
| `--muted` | `#777` | Labels, secondary text |
| `--border` | `#222` | Dividers |
| `--max` | `1100px` | Max content width |

Fonts: **Oswald** (headings/logos) and **Inter** (body), loaded from Google Fonts.

## Responsive Breakpoints

- `≤ 900px` — releases go 2-column, about grid stacks, gallery goes 3-column
- `≤ 680px` — hamburger nav, releases go 1-column, gallery goes 2-column
- `≤ 400px` — gallery goes 1-column
