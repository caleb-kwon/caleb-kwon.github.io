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

### Removing RB2B

Removing RB2B from the website means removing the site code and then updating the rendered GitHub Pages output. This is separate from any account-side RB2B cancellation or dashboard cleanup.

Removing RB2B does not remove Google Analytics. Leave the Quarto `google-analytics` setting in place unless the goal is also to remove GA.

1. Remove the header include from `_quarto.yml`:

```yaml
format:
  html:
    include-in-header:
      - _includes/rb2b.html
```

If RB2B is the only header include, remove the entire `include-in-header` block.

2. Delete `_includes/rb2b.html`.

3. Render individual pages only:

```bash
quarto render index.qmd
quarto render research.qmd
quarto render cv.qmd
```

4. Verify the public HTML no longer contains RB2B:

```bash
rg -n "reb2b|1N5W0H75JDO5|ddwl4m2hdecbv" _quarto.yml docs/*.html
```

This command should return no matches. The README may still mention RB2B for historical documentation.

5. Commit and push from `website/`:

```bash
git add _quarto.yml docs/index.html docs/research.html docs/cv.html docs/search.json
git add -u _includes/rb2b.html
git commit -m "Remove RB2B tracking"
git push
```

6. After GitHub Pages refreshes, verify the live site:

```bash
curl -fsSL https://calebkwon.com | rg "reb2b|1N5W0H75JDO5|ddwl4m2hdecbv"
```

This should return no matches. If the site still shows RB2B immediately after pushing, wait a few minutes or use a cache-busting query string before concluding the removal failed.

To fully eliminate RB2B beyond the website code, also disable or delete the relevant site/property in the RB2B dashboard. Removing the website script stops new page loads from firing RB2B; dashboard cleanup prevents accidental future reuse.

## Updating Publications

Edit the source publication entries in `main.tex` first, then update `research.qmd` to match and render:

```bash
quarto render research.qmd
```

### Publication Display Notes

- On `research.qmd`, "The Effects of Fair Workweek Laws on Worker Schedules" is listed in Published as a Management Science paper with no `(Forthcoming)` label.
- In the Published section, it should appear before "Supply Chain Management in the AI Era."
- On `index.qmd`, the selected-research card for the worker-schedules paper should read `with A. Raman / Management Science`, also with no forthcoming label.
- After publication display changes, render the affected page plus `index.qmd` if the homepage card changed, then commit the rendered `docs/` output and `docs/search.json`.

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
