# QiYuan's Web Site Conventions Reference

Subtask: `001_audit-site-conventions`
Date audited: 2026-03-08
Scope: Read-only audit of Jekyll/GitHub Pages source conventions.

---

## 1) Site Architecture

### 1.1 Project Structure (audited)

Key directories and files:

- `_config.yml`
- `_posts/` (8 files)
- `_blogs/` (1 file)
- `_figs/` (3 files)
- `_shots/` (1 file)
- `_vlogs/` (1 file)
- `_layouts/` (9 files)
- `_includes/` (15 files)
- `_data/social.yml`
- `public/css/` (`poole.css`, `hyde.css`, `syntax.css`)
- `public/fig_post/` (collection-specific figure assets)
- `public/shots/` (collection-specific photography assets)
- Static pages: `about.md`, `publication.md`, `notes.html`, `gallery.html`, `shots.html`, `Vlog.html`
- Aggregation pages: `index.html`, `timeline.md`, `timeline_2.md`
- Tag page generator: `tag_generator.py`

Notes:

- The subtask input said 14 includes, but repository currently has 15 include files.
- `default_post.html` exists but includes comments indicating it is not used.

### 1.2 Jekyll Configuration Highlights (`_config.yml`)

Configuration observed:

- Markdown engine: `kramdown`
- Kramdown input: `GFM`
- ToC levels: `1..2`
- Syntax highlighter: `rouge`
- Pagination: `paginate: 10`
- Pagination path: `"/blog/page:num/"`
- Plugins:
  - `jekyll-paginate`
  - `jekyll-archives`
  - `jekyll-commonmark-ghpages`
- Site URL: `https://qiyuan-zhang.github.io`
- `baseurl: ''`
- Disqus shortname: `qiyuan`

### 1.3 Collections and Permalinks

Collections defined in `_config.yml`:

- `figs`
  - `output: true`
  - `permalink: /:collection/:path/`
- `vlogs`
  - `output: true`
  - `permalink: /:collection/:path/`
- `shots`
  - `output: true`
  - `permalink: /:collection/:path/`
- `blogs`
  - `output: true`
  - `permalink: /:collection/:path/`

Core posts (`_posts`) use Jekyll default post behavior (filename date prefix drives post date URL semantics).

---

## 2) Content File Conventions

### 2.1 Filename Convention

Observed collection filename patterns:

- Posts: `YYYY-MM-DD-Title-With-Hyphens.md`
  - Example: `_posts/2024-08-30-Paper-Deep-DeePC.md`
- Blogs: `YYYY-MM-DD-Title-With-Hyphens.md`
  - Example: `_blogs/2024-04-05-DeePC-WWTPs.md`
- Figs: `YYYY-MM-DD-Title-With-Hyphens.md`
  - Example: `_figs/2024-03-29-Logo.md`
- Shots: `YYYY-MM-DD-Title-With-Hyphens.md`
  - Example: `_shots/2023-03-23-Daily-life.md`
- Vlogs: `YYYY-MM-DD-Title-With-Hyphens.md`
  - Example: `_vlogs/2024-01-02-Bye-Bye-2023.md`

### 2.2 Front Matter by Content Type

#### `_posts/` front matter

Typical fields observed:

- `layout: post`
- `title: "..."`
- `date: YYYY-MM-DD`
- `categories: ...` (space-separated tokens)
- `comments: true`
- `tags:` optional in layout/script support, but not currently present in audited post files

Real example:

```yaml
---
layout: post
title:  "Developed <span style='color:#e32724'>QYtool</span> toolbox"
date:   2024-08-29
categories: My-toolbox
comments: true
---
```

#### `_blogs/` front matter

Typical fields observed:

- `layout: blog`
- `title`
- `date`
- `categories`
- `comments: true`

Real example:

```yaml
---
layout: blog
title:  "DeePC for WWTPs"
date:   2024-04-05
categories: DeePC WWTPs
comments: true
---
```

#### `_figs/` front matter

Typical fields observed:

- `layout: fig`
- `title`
- `date`
- `categories`
- `comments: true`

Real example:

```yaml
---
layout: fig
title:  "My logo"
date:   2024-03-29
categories: Logo B&W
comments: true
---
```

#### `_shots/` front matter

Typical fields observed:

- `layout: shot`
- `title`
- `date`
- `categories`
- `comments: true`

Real example:

```yaml
---
layout: shot
title:  "Daily life"
date:   2023-03-23
categories: Daido-Moriyama
comments: true
---
```

#### `_vlogs/` front matter

Typical fields observed:

- `layout: vlog`
- `title`
- `date`
- `categories`
- `comments: true`

Real example:

```yaml
---
layout: vlog
title:  "Bye Bye <span style='color:#e32724'>2023</span>!"
date:   2024-01-01
categories: Big-day
comments: true
---
```

### 2.3 Title Styling Convention

Inline HTML title styling exists in front matter title strings for emphasis, typically:

- `<span style='color:#e32724'>...</span>` inside `title`

Examples:

- `_posts/2024-04-15-Developed-deepctools.md`
- `_posts/2024-04-25-Developed-modlinear.md`
- `_posts/2024-08-30-Paper-Deep-DeePC.md`
- `_vlogs/2024-01-02-Bye-Bye-2023.md`
- `Vlog.html` page title also uses inline `<span>` color styling

### 2.4 Date Format Convention

Observed front matter date values consistently use ISO date form:

- `YYYY-MM-DD`

Examples: `2024-08-30`, `2024-03-28`, `2023-03-23`, `2024-01-01`.

---

## 3) Categories and Tags

### 3.1 Category Value Shape

Categories are written as space-separated tokens in front matter (not YAML list brackets in audited files).

Example:

- `categories: Learning-notes CasADi`
- `categories: Logo B&W`

### 3.2 Hyphen Naming Pattern and Display Logic

Display templates convert hyphen to spaces when rendering archive headings:

- `{{ category_name | replace: "-", " " }}` in `notes.html`
- same pattern in `gallery.html`, `shots.html`, `Vlog.html`

Implication:

- Intended convention supports multi-word category labels via hyphen joining.

Observed status:

- Many categories follow hyphen style (`Learning-notes`, `My-toolbox`, `Big-day`, `Daido-Moriyama`)
- Some categories are single-token or symbol forms (`Paper`, `B&W`, `CasADi`, `WWTPs`)

### 3.3 Known Categories by Collection (from current content)

`_posts`:

- `Learning-notes`
- `CasADi`
- `MATLAB`
- `My-toolbox`
- `Paper`

`_blogs`:

- `DeePC`
- `WWTPs`

`_figs`:

- `Freshness`
- `B&W`
- `Logo`

`_shots`:

- `Daido-Moriyama`

`_vlogs`:

- `Big-day`

### 3.4 Tag System

Tag tooling is present but currently minimally used in content:

- `tag_generator.py` scans `_posts/*.md` for `tags:` line in front matter
- It recreates `tag/<tag>.md` pages with `layout: tagpage`
- `post.html` and collection layouts render `page.tags` if present
- `head.html` includes `collecttags.html`

Current audited content status:

- No `tags:` fields found in `_posts`, `_blogs`, `_figs`, `_shots`, or `_vlogs` files.

---

## 4) Layout Hierarchy and Rendering

### 4.1 Primary Hierarchy

Base:

- `default.html`
  - includes `head.html`
  - includes `google_analytics.html`
  - includes `sidebar.html`
  - renders `{{ content }}`

Derived layout files with front matter `layout: default`:

- `page.html`
- `post.html`
- `blog.html`
- `fig.html`
- `shot.html`
- `vlog.html`
- `tagpage.html`

Additional layout:

- `default_post.html` (marked as not used in comments)

### 4.2 Common Elements in Post-Like Layouts

`post.html`, `blog.html`, `fig.html`, `shot.html`, `vlog.html` share patterns:

- Include `tablecontentbar.html` (ToC/date side bar)
- Title render: `<h1 class="post-title-new">{{ page.title }}</h1>`
- Meta line: date + categories
- `page.tags` rendering block with tag links (`/tag/<tag>`)
- "Recent Posts" block (collection-aware logic varies)
- Link to `/timeline`
- Disqus include gated by `page.comments`

### 4.3 Collection-Specific Category Helpers

Included category gatherers:

- `collectblogcategories.html`
- `collectfigscategories.html`
- `collectshotscategories.html`
- `collectvlogscategories.html`

Used both in list pages and collection post layouts to compute category sets.

### 4.4 Tag Archive Layout

`tagpage.html`:

- Iterates `site.tags[page.tag]`
- Outputs tagged post list
- Includes `archive.html` tag cloud/archive links section

---

## 5) Navigation, Sidebar, and Timeline Logic

### 5.1 Sidebar Navigation Source

Navigation is hardcoded in `_includes/sidebar.html` (manual order):

1. Home (`/`)
2. Notes (`/notes`)
3. Shots (`/shots`)
4. Gallery (`/gallery`)
5. Publication (`/publication`)
6. About (`/about`)

Special behavior:

- Site title has clickable "i" linking to `/blog` (hidden/secret route motif)

### 5.2 Social Links Data Flow

- Data file: `_data/social.yml`
- Rendering include: `_includes/social_links.html`
- Sidebar includes `social_links.html`
- Current social keys:
  - `email`
  - `linkedin`
  - `github`
  - `google-scholar`
  - `bilibili`
  - `unsplash`

Each entry uses `id`, `href`, `title`, `fa-icon`, `path`.

### 5.3 Timeline and Aggregation Pages

`timeline.md` (`/timeline/`):

- Concatenates `site.posts + site.figs + site.vlogs + site.shots`
- Sorts by `date` descending
- Groups output by year
- For `posts` collection label shown as `Notes`
- For `vlogs`, title displayed as plain text (no link)
- For other collections, title linked to `post.url`

`timeline_2.md` (`/timeline_personal/`):

- Similar year grouping format
- Uses only `site.blogs`

Collection archive-like pages:

- `notes.html` loops `site.categories` (post categories)
- `gallery.html` loops `site.figs` by collected fig categories
- `shots.html` loops `site.shots` by collected shot categories
- `Vlog.html` loops `site.vlogs` by collected vlog categories

All these pages include a "Timeline of posts" link to `/timeline`.

---

## 6) Asset Organization and Path Conventions

### 6.1 CSS and Styling Roles

- `public/css/poole.css`
  - Base typography, elements, code styles, gallery/video/password box styles
- `public/css/hyde.css`
  - Sidebar layout, table-of-content bar, responsive two-sidebar layout behavior
- `public/css/syntax.css`
  - Rouge/Pygments code highlight color classes

### 6.2 Font and Icons

From `_includes/head.html`:

- Google Font: `East Sea Dokdo`
- Font Awesome CDN: `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.7.0/css/all.min.css`

### 6.3 Image Asset Path Patterns

Observed conventions:

- Figure posts (`_figs`) embed assets under:
  - `{{ '/' | relative_url }}public/fig_post/<FolderName>/<file>`
  - Example folder names: `Messiness`, `Black-and-White`, `Logo`

- Shot posts (`_shots`) embed assets under:
  - `{{ '/' | relative_url }}public/shots/<YYYY-MM-DD-slug>/<file>`
  - Example: `public/shots/2023-03-23-Daily-life/1.jpg`

- Home page uses `public/images/*` assets for decorative section headers.

### 6.4 Video Embedding Convention

`_vlogs` content pattern:

- A markdown link to Bilibili video page
- HTML `<div class="video">` wrapper
- Embedded Bilibili `<iframe src="https://player.bilibili.com/player.html?...">`

---

## 7) Writing Style Observations

### 7.1 Tone and Formality

Observed style across content:

- Predominantly technical and instructional in `_posts` and `_blogs`
- Personal/creative and concise in `_figs`, `_shots`, `_vlogs`
- Mixed voice: practical notes + project documentation + personal media logs

### 7.2 Heading Depth and Structure

Common pattern:

- `#` major sections
- `##` and `###` for nested technical steps
- Heavy use of section prefixes (`I.`, `II.`, `III.`) in technical posts

### 7.3 Code and Math Conventions

Code:

- Triple-backtick fenced blocks, usually untyped (no explicit language token)
- Command snippets and tree listings frequent

Math:

- Inline `$...$` and display-like math text used in technical notes
- MathJax enabled globally through `_includes/mathjax.html`

### 7.4 Link and Image Embedding Patterns

Links:

- Mostly inline markdown links: `[label](url)`
- Some reference-style links used (example in CasADi post)

Images:

- Markdown image syntax for externally hosted images in posts
- Raw HTML `<img>` for gallery/shot and multi-image layout control

### 7.5 Excerpt and Intro Pattern

Many posts begin with:

- A blockquote summary (`> ...`)
- Separator line (`---`)
- Then body sections

This creates a compact teaser-like excerpt for listing pages.

---

## 8) Static Page Conventions

### 8.1 Page Front Matter Pattern

Static pages generally use:

- `layout: page`
- `title:`
- Optional `permalink:`
- Optional `description:`

Example (`notes.html`):

```yaml
---
layout: page
permalink: /notes/
title: Notes
description: Here are notes encompassing a variety of topics.
---
```

### 8.2 Special Page Notes

- `blog.html` is intentionally protected/under construction and includes password logic (`check.html`).
- `Vlog.html` uses uppercase file name but permalink `/vlogs/`.
- `index.html` is `layout: page` and aggregates multiple content types with manual sections.

---

## 9) Verified Convention Cross-Checks (minimum 3)

Cross-check A: Layout mapping by collection

- `_posts/*` use `layout: post`
- `_blogs/*` use `layout: blog`
- `_figs/*` use `layout: fig`
- `_shots/*` use `layout: shot`
- `_vlogs/*` use `layout: vlog`

Evidence files:

- `_posts/2024-08-30-Paper-Deep-DeePC.md`
- `_blogs/2024-04-05-DeePC-WWTPs.md`
- `_figs/2024-03-29-Logo.md`
- `_shots/2023-03-23-Daily-life.md`
- `_vlogs/2024-01-02-Bye-Bye-2023.md`

Cross-check B: Category display hyphen replacement logic

- Render logic `replace: "-", " "` verified in:
  - `notes.html`
  - `gallery.html`
  - `shots.html`
  - `Vlog.html`

Cross-check C: Collection permalink configuration

- `/:collection/:path/` confirmed in `_config.yml` for `figs`, `vlogs`, `shots`, `blogs`.

Cross-check D: Sidebar navigation order and social link include

- Link order and static routes confirmed in `_includes/sidebar.html`.
- Social links include confirmed via `{% include social_links.html %}` and `_data/social.yml` schema.

Cross-check E: Asset path conventions

- `_figs` source points to `public/fig_post/...` in multiple files.
- `_shots` source points to `public/shots/YYYY-MM-DD-slug/...` in `_shots/2023-03-23-Daily-life.md`.

---

## 10) Practical Authoring Checklist (for future edits)

When adding new content:

- Use correct directory by content type (`_posts`, `_blogs`, `_figs`, `_shots`, `_vlogs`).
- Name file as `YYYY-MM-DD-Title-With-Hyphens.md`.
- Set matching `layout` (`post/blog/fig/shot/vlog`).
- Include `title`, `date`, `categories`, `comments: true`.
- Keep date format `YYYY-MM-DD`.
- Use hyphenated category names for multi-word categories (for consistent display behavior).
- For stylized titles, embed `<span style='color:#e32724'>...</span>` as needed.
- For fig assets, place files under `public/fig_post/<slug-or-folder>/`.
- For shot assets, place files under `public/shots/<YYYY-MM-DD-slug>/`.
- For vlog entries, include both Bilibili link and iframe pattern used in existing file.
- Keep opening summary blockquote and sectioned structure to match site style.

---

## 11) Audit Boundaries and Notes

- No source/content/config/CSS files were modified.
- No build, dependency install, or Jekyll run was executed.
- Outputs were created only under `.codex/subtask/001_audit-site-conventions/`.

