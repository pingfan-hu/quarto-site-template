# Quarto Academic Website Template

A personal academic website template built with [Quarto](https://quarto.org/), styled with Bootstrap (flatly/darkly themes), and deployed via GitHub Actions to Netlify.

## Quick Start

1. Use this as a GitHub template repo (click "Use this template")
2. Clone your new repo
3. Search for all `# CHANGE` comments — they mark every spot that needs your info
4. Rename template files and folders to your preferred names (see below)
5. Add your images to `images/` (see required images below)
6. Run `quarto preview` to see your site locally

## Required Images

Place these in `images/`:

| File | Used for |
|------|----------|
| `homepage.png` | Homepage profile photo (shown next to bio) |
| `about.png` | Single-page banner (wide, ~800px) |
| `card.png` | Open Graph / social share card |
| `favicon.png` | Browser tab icon |

## Project Structure

```
├── _quarto.yml                  # Master config — update name, URLs, social links
├── _variables.yml               # Reusable shortcodes for links/tools
├── index.qmd                    # Homepage
├── single-page.qmd              # Example single page (e.g. rename to about.qmd)
├── listing-default.qmd          # Example default listing page (e.g. rename to blog.qmd)
├── listing-grid.qmd             # Example grid listing page (e.g. rename to projects.qmd)
├── papers.qmd                   # Publications page
├── talks.qmd                    # Talks/presentations (R-generated from CSV)
├── cv.qmd                       # CV (renders to PDF)
├── resume.qmd                   # Resume (renders to PDF)
│
├── chunks/                      # Reusable content included with {{< include >}}
│   ├── intro.qmd                # Short bio — used in index.qmd and single-page.qmd
│   ├── skills.qmd               # Skills list — used in single-page.qmd, cv.qmd, resume.qmd
│   └── example-paper.qmd       # Template for a paper card in papers.qmd
│
├── listing-default/             # Content folder for listing-default.qmd (e.g. rename to blog/)
│   ├── _metadata.yml            # Sets author for all posts
│   ├── banners/                 # Banner images for the listing
│   └── 2024-01-01-example-post/
│       └── index.qmd
│
├── listing-grid/                # Content folder for listing-grid.qmd (e.g. rename to projects/)
│   ├── _metadata.yml            # Hides title metadata on project pages
│   ├── banners/                 # Banner images for the grid
│   └── 2024-example-project/
│       └── index.qmd
│
├── talks/
│   └── talks.csv                # Add a row per talk/poster — auto-renders on talks page
│
├── files/                       # PDF papers and documents (linked from papers.qmd)
├── images/                      # Site-wide images (see above)
├── styles/
│   └── theme.scss               # All custom styling (SCSS + CSS)
│
├── _extensions/
│   ├── cv/                      # Custom LaTeX format for PDF CV/Resume
│   └── quarto-ext/              # FontAwesome icons ({{< fa brands github >}})
│
└── .github/workflows/
    └── build.yml                # GitHub Actions: render & deploy to Netlify
```

## Renaming Template Files and Folders

The listing pages and their content folders are named generically. To rename them (e.g. `listing-default` → `blog`), update these four things consistently:

| What | Example |
|------|---------|
| The `.qmd` file | `listing-default.qmd` → `blog.qmd` |
| The content folder | `listing-default/` → `blog/` |
| `contents:` in the `.qmd` front matter | `contents: listing-default` → `contents: blog` |
| Resources path in `_quarto.yml` | `listing-default/banners/` → `blog/banners/` |
| `image:` path in each item's front matter | `/listing-default/banners/...` → `/blog/banners/...` |

The same applies to `listing-grid` → `projects` (or any name you prefer).

## Adding Content

### New Post (in listing-default)
Create `listing-default/YYYY-MM-DD-your-slug/index.qmd` with this front matter:
```yaml
---
title: "Your Post Title"
image: "/listing-default/banners/YYYY-MM-DD-your-slug.png"
date: "YYYY-MM-DD"
categories: [Category1, Category2]
description: "One sentence description."
---
```

### New Project (in listing-grid)
Create `listing-grid/YYYY-your-slug/index.qmd` with this front matter:
```yaml
---
title: "Your Project Title"
image: "/listing-grid/banners/YYYY-your-slug.png"
author:
  - name: "[Your Name](https://yourdomain.com)"
date: "Month, YYYY"
categories: [Category1, Category2]
description: "One sentence description."
---
```

### New Talk or Poster
Add a row to `talks/talks.csv`:
```
YYYY-MM-DD,"Talk Title",[Event Name](https://event.url),"City, Country",repo-name,slide
```
- `Type` = `slide` (shows slides + PDF + GitHub buttons) or `poster` (shows PDF only)
- `Name` = your GitHub repo name for the slides (used to build the GitHub Pages URL)
- Place the PDF at `talks/repo-name.pdf`
- Set `github_username` at the top of `talks.qmd`

### New Paper Card
Copy `chunks/example-paper.qmd` to `chunks/YYYY-journal-slug.qmd`, fill in your citation, then add `{{< include /chunks/YYYY-journal-slug.qmd >}}` to `papers.qmd`.

## Deployment

### Netlify Setup
1. Connect your GitHub repo to Netlify
2. Add two secrets to your GitHub repo (Settings → Secrets → Actions):
   - `NETLIFY_AUTH_TOKEN` — from Netlify user settings
   - `NETLIFY_SITE_ID` — from your Netlify site settings
3. Push to `main` — GitHub Actions will render and deploy automatically

### Local Preview
```bash
quarto preview    # Live-reload preview
quarto render     # Full build to _site/
```

## CV / Resume PDF

The `cv.qmd` and `resume.qmd` use a custom LaTeX format (`_extensions/cv/`). Font files are in `_extensions/cv/fonts/`. If you want different fonts, update `preamble.tex` accordingly — or remove the `\usepackage{fontspec}` block to use the default LaTeX font.

Requires TinyTeX (installed automatically by the GitHub Action, or run `quarto install tinytex` locally).
