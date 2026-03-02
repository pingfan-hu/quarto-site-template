# New Site Setup

You are helping the user build a new website from this Quarto template. The template is general-purpose — it can serve any kind of site. Let the user's purpose drive all decisions.

---

## Step 1: Understand the Purpose

Ask the user these questions in a single message:

1. **What is this site for?** Describe it in a sentence or two. (e.g. "documentation for my open source library", "portfolio for my design studio", "course website for a machine learning class", "company landing page for a SaaS product")
2. **Who is the audience?** (e.g. developers, students, clients, general public)
3. **What are the main sections/pages you need?** List them, or say "not sure yet" and we'll figure it out together.
4. **Do you have a name/title for the site?**
5. **Do you have a domain or URL?** (or type "not yet")

Wait for the user's answers before continuing.

---

## Step 2: Propose a Site Structure

Based on their answers, propose:

- A navbar structure (which pages to keep, rename, add, or remove)
- What content each page should have
- Whether social/external links in the navbar make sense (and which ones)
- A suggested color direction (just a word — "professional blue", "warm earthy", "bold and high-contrast", etc. — don't pick a hex yet)

Present this as a clear proposal and ask: **"Does this structure work, or would you like to adjust anything?"**

Wait for confirmation or changes before proceeding.

---

## Step 3: Collect Remaining Details

Based on the confirmed structure, ask for only the details that are actually needed — no more. For example:

- Only ask for social links if they belong in this site's navbar
- Only ask for color hex if they want to customize (otherwise suggest keeping the default or picking from common options)
- Only ask for a repo URL if they want GitHub edit/issue links on pages
- Only ask for author name if the site has authored content (posts, papers, etc.)

Group all remaining questions into one message. Wait for answers.

---

## Step 4: Make All File Edits

Make every edit that follows from steps 2–3. Touch only what's needed for this specific site. Common edits include:

### `_quarto.yml`
- Update `website.title`
- Update `website.description`
- Update `website.site-url` (use placeholder if unknown)
- Update `website.repo-url` if applicable
- Update footer text
- Update `link-external-filter` regex to match the site's domain
- Restructure `navbar.left` to match the confirmed page structure (rename hrefs and text, remove unused pages, add new ones if needed)
- Update or remove `navbar.right` social links based on what's relevant
- Remove academic-specific settings if not needed (e.g. ORCID, Google Scholar)

### `index.qmd`
- Update `title` and `description` (top-level frontmatter keys)
- Rewrite the page structure to match the site's purpose (homepage for a product is different from a personal bio)
- Update or remove `about.links` as appropriate

### `single-page.qmd` (or rename/repurpose it)
- Update `description` (top-level frontmatter key)
- Rewrite sections to fit the site's purpose (e.g. "About the Project" instead of "About Me")
- If this page doesn't fit the site at all, note it for deletion

### `listing-default.qmd` and `listing-grid.qmd`
- Rename titles and descriptions to fit (e.g. "Blog" → "Updates", "Projects" → "Case Studies")
- Update `description` (top-level frontmatter key)

### `styles/theme.scss`
- Update primary color if user specified one (replace `#5654A2` throughout, including dark mode variant near `#7c7ac4`)

### `chunks/intro.qmd`
- Rewrite the intro block to match the site's purpose and voice

### Metadata files (`listing-default/_metadata.yml`, `listing-grid/_metadata.yml`)
- Update author/title fields if applicable

---

## Step 5: Report & Checklist

After all edits, print:

```
✅ Done. Here's what was changed:
[list every file edited and what changed]

📋 What's left:

REQUIRED — won't render correctly without these:
  □ Add images/homepage.png — [describe what image makes sense for this site]
  □ Add images/card.png — social share card (1200×630px)
  □ Add images/favicon.png — square icon (32×32px or larger)

CONTENT:
  [list only the content files relevant to this specific site's structure]
  □ chunks/intro.qmd — [specific guidance based on site purpose]
  □ [other content files to write]
  □ Delete or replace example posts/projects in listing folders

OPTIONAL:
  [list only pages that were discussed but deferred]

NEXT STEP:
  □ Run: quarto preview — to see the site locally
```

Keep the checklist specific to this site — don't include irrelevant items like ORCID if it's a product site.
