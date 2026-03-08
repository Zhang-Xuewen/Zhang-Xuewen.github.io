# Subtask 001: Audit Site Structure and Document Conventions Reference

## Scope

Thoroughly analyze the QiYuan's Web Jekyll/GitHub Pages site and produce a comprehensive conventions reference document. This document will serve as the authoritative guide for all future content creation and editing operations on the site.

## Inputs

- `_config.yml` — site configuration, collections, plugins, permalink patterns
- `_posts/` — standard Jekyll blog posts (8 files)
- `_blogs/` — custom collection for personal research notes
- `_figs/` — custom collection for artwork/figures
- `_shots/` — custom collection for photography
- `_vlogs/` — custom collection for video logs
- `_layouts/` — 9 layout files defining page structure
- `_includes/` — 14 include partials
- `_data/social.yml` — social link data
- `public/css/` — poole.css, hyde.css, syntax.css
- `about.md`, `publication.md`, `notes.html`, `gallery.html`, `shots.html`, `Vlog.html` — static pages
- `_includes/sidebar.html` — navigation structure
- `tag_generator.py` — tag page generation script

## Outputs

- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — comprehensive conventions reference

## What the Reference Document Must Cover

### 1. Site Architecture
- Directory structure overview
- Jekyll configuration highlights (markdown engine, highlighter, pagination, plugins)
- Custom collections and their configuration (output, layout, permalink)

### 2. Content File Conventions
- Filename pattern: `YYYY-MM-DD-Title-With-Hyphens.md`
- Front matter fields for each content type:
  - `_posts/`: layout, title, date, categories, comments, tags (optional)
  - `_blogs/`: layout, title, date, categories, comments
  - `_figs/`: layout, title, date, categories, comments
  - `_shots/`: layout, title, date, categories, comments
  - `_vlogs/`: layout, title, date, categories, comments
- Title styling conventions (inline HTML spans with color)
- Date format: `YYYY-MM-DD`

### 3. Categories & Tags
- Category naming: hyphen-separated words (e.g., `Learning-notes`, `My-toolbox`)
- Display logic: hyphens replaced with spaces in templates
- Known categories per collection
- Tag system: `tag_generator.py` generates pages from `_posts/` tags

### 4. Layout Hierarchy
- `default.html` → `page.html`, `post.html`, `blog.html`, `fig.html`, `shot.html`, `vlog.html`
- Common elements: ToC bar, category display, recent posts, Disqus comments
- `tagpage.html` for tag archive pages

### 5. Navigation & Sidebar
- Sidebar links and order
- Social links from `_data/social.yml`
- Timeline pages and their content aggregation logic

### 6. Asset Organization
- CSS files and their roles
- Image paths per collection:
  - `_figs` → `public/fig_post/<slug>/`
  - `_shots` → `public/shots/<YYYY-MM-DD-slug>/`
- Font usage (East Sea Dokdo via Google Fonts)
- Font Awesome icons (CDN v5.7.0)

### 7. Writing Style Observations
- Tone and formality level from existing posts
- Heading depth patterns
- Code block and math rendering conventions (MathJax support)
- Link and image embedding patterns

## Acceptance Criteria

1. Reference document covers all 5 content collections with accurate front matter field listings
2. Reference includes exact naming conventions, category patterns, and layout assignments
3. Reference documents the site navigation structure accurately
4. Reference captures the inline HTML title styling convention
5. Reference includes image asset path conventions for each collection
6. All information is verified against actual site files — no fabricated details

## Verification

- Cross-check at least 3 documented conventions against actual site files
- Verify that front matter examples match real posts

## Forbidden Actions

- Do NOT modify any site files (source code, content, config, CSS)
- Do NOT create files outside of `.codex/subtask/001_audit-site-conventions/`
- Do NOT run Jekyll build or install gems (that is subtask 002's job)
- Do NOT reorganize or rename any project files
