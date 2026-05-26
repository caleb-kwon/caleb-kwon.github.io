# Caleb Kwon - Academic Website

Quarto-based academic website deployed through GitHub Pages at `calebkwon.com`.

## Quick Start

Install Quarto once:

```bash
brew install quarto
```

Preview locally:

```bash
cd /Users/ck29972/Dropbox/Resume-Claude/website
quarto preview index.qmd
```

## Updating The Site

Do not run bare `quarto render` in this Dropbox-synced folder. Render individual files instead:

```bash
quarto render index.qmd
quarto render research.qmd
```

Render `cv.qmd` only when the CV page itself changes. After CV PDF changes, copy the PDF into the published folders:

```bash
cp ../main.pdf main.pdf
cp ../main.pdf docs/main.pdf
```

Commit and push from `website/`:

```bash
git add -A
git commit -m "Update site"
git push
```

## Homepage Notes

- `index.qmd` is the homepage source.
- `new_photo.png` is the active homepage portrait; `profile.jpg` is legacy.
- `styles.css` contains the main site styling.
- `homepage-fixes.css` is intentionally loaded after `styles.css` to override cached/older homepage rules on the live site.
- `archive/index-old.qmd` preserves the pre-redesign homepage.

## Tracking

RB2B visitor identification tracking was installed on May 26, 2026.

- Source snippet: `_includes/rb2b.html`
- Site-wide Quarto include: `_quarto.yml` under `format.html.include-in-header`
- Rendered pages updated directly: `docs/index.html`, `docs/research.html`, and `docs/cv.html`
- RB2B key: `1N5W0H75JDO5`

This is a direct global-header install, not a Google Tag Manager install. The site uses Quarto's Google Analytics setting, which emits `gtag.js`; it does not currently define a GTM container. If a GTM container is added later, do not also fire the same RB2B script through GTM unless the direct header include is removed.

When Quarto is available, render individual pages only. A page render should reinsert `_includes/rb2b.html` into the HTML header.

## Updating Publications

Edit the source publication entries in `main.tex` first, then update `research.qmd` to match and render:

```bash
quarto render research.qmd
```

## File Structure

```text
website/
├── _quarto.yml          # Site config and CSS includes
├── _includes/rb2b.html  # RB2B tracking snippet included in every HTML header
├── index.qmd            # Home page
├── research.qmd         # Publications
├── cv.qmd               # CV page
├── styles.css           # Main styling
├── homepage-fixes.css   # Homepage override/cache-busting styling
├── new_photo.png        # Active homepage portrait
├── main.pdf             # CV PDF
├── archive/             # Archived old homepage source
└── docs/                # Rendered GitHub Pages output
```
