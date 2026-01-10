# Caleb Kwon - Academic Website

Quarto-based academic website. Auto-deploys to GitHub Pages.

## Quick Start

### 1. Install Quarto (one-time)
```bash
# Mac
brew install quarto

# Or download from: https://quarto.org/docs/get-started/
```

### 2. Add your profile photo
Place a photo named `profile.jpg` in this folder.

### 3. Preview locally
```bash
cd website
quarto preview
```

### 4. Deploy to GitHub Pages
```bash
quarto render
git add .
git commit -m "Update site"
git push
```

## Updating Publications

Edit `main.tex` (source of truth), then run Claude Code:
> "Update my website publications from main.tex"

## File Structure

```
website/
├── _quarto.yml    # Site config
├── index.qmd      # Home page
├── research.qmd   # Publications
├── cv.qmd         # CV page
├── styles.css     # Custom styling
├── main.pdf       # CV PDF
└── profile.jpg    # Your photo
```
