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

## Updating Publications

Edit the source publication entries in `main.tex` first, then update `research.qmd` to match and render:

```bash
quarto render research.qmd
```

## File Structure

```text
website/
├── _quarto.yml          # Site config and CSS includes
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
