# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository

Personal portfolio website for Hugo Moronval, deployed via GitHub Pages from the `main` branch at **https://moronvalhugo.github.io**.

Development happens on the feature branch `claude/create-deploy-index-WVg7L`. To deploy changes, push to that branch then either open a PR to `main`, or use the `mcp__github__push_files` tool to commit directly to `main`.

## Pages

| File | URL | Purpose |
|------|-----|---------|
| `index.html` | `/` | Homepage — hero, stats, cards, about |
| `cv.html` | `/cv.html` | Interactive digital CV |
| `portfolio.html` | `/portfolio.html` | Case studies (5 companies) |
| `cv-print.html` | `/cv-print.html` | A4 printable CV (Chrome → Ctrl+P → Save PDF) |
| `cv-teaser.html` | `/cv-teaser.html` | One-page PDF teaser for job sites |
| `home/index.html` | `/home/` | Old landing page, noindexed |

## Design System

All pages share the same CSS design tokens — never hardcode colors:

```css
--bg:      #F5F2EC  /* beige background */
--ink:     #1A1A1A  /* body text */
--ink2:    #555–#777 /* secondary text */
--accent:  #C8A96B  /* gold */
--border:  #E0DDD6  /* dividers */
--black:   #0D0D0D  /* dark backgrounds */
```

Fonts (loaded from Google Fonts):
- **Bricolage Grotesque** weight 800 — all headings, uppercase
- **Space Grotesk** weights 300–700 — body text

## Assets

All images live in `assets/`. When a user uploads a file via GitHub.com, it often gets a double extension (e.g. `photo-hugo.jpg.jpg`). Always check the actual filename with `git ls-tree origin/main assets/` before referencing it in HTML/CSS.

Compress images before committing:
```bash
# JPEG
convert input.jpg -quality 78 -strip output.jpg
# PNG
pngquant --quality=60-80 --force --output file.png file.png
```

## Key CSS Patterns

**Hamburger mobile menu** — implemented on all 3 main pages. CSS class `.nav-mobile.open` toggles via JS `classList.toggle`. The overlay is a fixed full-screen div with id `navMobile`.

**Aperçu grid** in `portfolio.html` uses class `.apercu-grid` (5 columns desktop → 2 columns mobile via `@media (max-width: 900px)`). Do not use inline `style="display:grid"` on this element — it can't be overridden by media queries.

**Gold watermark text** on aperçu cards: `position:absolute`, `font-size:72px`, `color:rgba(200,169,107,.13)`, behind content using `z-index:1` on the inner div.

**Photo watermark** on index/cv: `position:fixed`, right side, `mix-blend-mode:multiply`, `filter:grayscale(100%)`, masked with a left-fade gradient.

**A4 print pages** (`cv-print.html`, `cv-teaser.html`): use `@page { size: A4; margin: 0; }` and `html, body { width: 210mm; height: 297mm; }`. Always add `.page { margin-top: 0 !important; }` in `@media print` to cancel the screen-only `margin-top` from the print bar.

## Portfolio Case Studies

Each study in `portfolio.html` has an `id` for anchor navigation from the aperçu section:
`#cosmogroup`, `#hpc`, `#3rois`, `#carre-rond`, `#epsi`

## Contact Info

- Tel: `07 82 24 66 10` / `+33782246610`
- Email: `moronval.hugo@gmail.com`
- LinkedIn: `https://www.linkedin.com/in/hugo-moronval/`
- Location: Hazebrouck (59), mobile région lilloise
