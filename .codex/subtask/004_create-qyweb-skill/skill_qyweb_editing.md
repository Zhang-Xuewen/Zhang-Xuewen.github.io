# skill_qyweb_editing

## Purpose
Enable any AI assistant (Claude Code, Codex) to safely create, update, and maintain content on QiYuan's Web (Jekyll + Hyde theme on GitHub Pages) with conventions that match the existing repository.

## When to Use (Triggers)
- User asks to create a new note/post/blog/figure/shot/vlog.
- User asks to update existing content files in `_posts/`, `_blogs/`, `_figs/`, `_shots/`, or `_vlogs/`.
- User asks to edit static pages such as `about.md`, `publication.md`, `notes.html`, `gallery.html`, `shots.html`, or `Vlog.html`.
- User asks to update main page sections (`index.html`) or sidebar navigation (`_includes/sidebar.html`).
- User asks for front matter fixes, filename/date alignment, category cleanup, or asset path corrections.

## Inputs / Assumptions
- Project root: QiYuan's Web repository.
- Site architecture: Jekyll with Hyde-style layouts and custom collections.
- Key collections configured in `_config.yml`:
  - `blogs` -> permalink `/:collection/:path/`
  - `figs` -> permalink `/:collection/:path/`
  - `shots` -> permalink `/:collection/:path/`
  - `vlogs` -> permalink `/:collection/:path/`
- `_posts/` uses standard Jekyll post behavior.
- Content files are Markdown with YAML front matter.
- Layout files exist in `_layouts/` and collection mapping is:
  - `_posts` -> `layout: post`
  - `_blogs` -> `layout: blog`
  - `_figs` -> `layout: fig`
  - `_shots` -> `layout: shot`
  - `_vlogs` -> `layout: vlog`

## Step-by-Step Procedure

### 1) Site Overview and Routing Check
1. Confirm project root and inspect `_config.yml` collections/permalinks.
2. Confirm target collection/page requested by user.
3. Confirm sidebar links in `_includes/sidebar.html` if navigation is involved.
4. Confirm expected archive/list page behavior:
   - Notes page: `/notes/`
   - Gallery page: `/gallery/`
   - Shots page: `/shots/`
   - Vlogs page: `/vlogs/` (exists but currently not linked in sidebar)

### 2) Create a New `_posts/` Entry
1. Choose filename: `YYYY-MM-DD-Title-With-Hyphens.md` under `_posts/`.
2. Use post front matter field order exactly:
   - `layout`
   - `title`
   - `date`
   - `categories`
   - `comments`
3. Set `layout: post`, `comments: true`, and date format `YYYY-MM-DD`.
4. Keep category values as space-separated tokens; for multi-word names, use hyphen style (example: `Learning-notes`).
5. Optionally style title emphasis with inline HTML span:
   - `<span style='color:#e32724'>keyword</span>`
6. Draft body using existing site style (often summary blockquote, separator, section headings).
7. If adding local images, use existing path conventions (commonly under `public/fig_post/<folder>/...` when appropriate) or external URLs.
8. Verify filename date matches front matter date before finalizing.

### 3) Create a New `_blogs/` Entry
1. Save file in `_blogs/` with `YYYY-MM-DD-Title-With-Hyphens.md`.
2. Use front matter order: `layout`, `title`, `date`, `categories`, `comments`.
3. Set `layout: blog` and `comments: true`.
4. Keep categories space-separated (example: `DeePC WWTPs`).
5. Structure content as project/research update with technical sections and optional math/code.
6. Ensure date consistency between filename and front matter.

### 4) Create a New `_figs/` Entry
1. Save file in `_figs/` with `YYYY-MM-DD-Title-With-Hyphens.md`.
2. Use front matter order: `layout`, `title`, `date`, `categories`, `comments`.
3. Set `layout: fig` and `comments: true`.
4. Follow gallery HTML pattern inside `<div class="gallery">`.
5. Reference images with Liquid-prefixed path format:
   - `{{ '/' | relative_url }}public/fig_post/<FolderName>/<file>`
6. Ensure asset folder exists under `public/fig_post/`.
7. Ensure filename date equals front matter date.

### 5) Create a New `_shots/` Entry
1. Save file in `_shots/` with `YYYY-MM-DD-Title-With-Hyphens.md`.
2. Use front matter order: `layout`, `title`, `date`, `categories`, `comments`.
3. Set `layout: shot` and `comments: true`.
4. Follow gallery HTML pattern inside `<div class="gallery">`.
5. Use shots path convention:
   - `{{ '/' | relative_url }}public/shots/<YYYY-MM-DD-slug>/<file>`
6. Ensure matching image directory exists under `public/shots/`.
7. Ensure filename date equals front matter date.

### 6) Create a New `_vlogs/` Entry
1. Save file in `_vlogs/` with `YYYY-MM-DD-Title-With-Hyphens.md`.
2. Use front matter order: `layout`, `title`, `date`, `categories`, `comments`.
3. Set `layout: vlog` and `comments: true`.
4. Include both:
   - A markdown link to the Bilibili video page.
   - A `<div class="video">` wrapper containing the Bilibili `<iframe>` embed.
5. Optionally use `<span style='color:#e32724'>...</span>` in title for emphasis.
6. Ensure filename date equals front matter date.

### 7) Update Existing Content File
1. Open the target file and preserve existing front matter fields/order unless user requested metadata changes.
2. Change only requested sections; avoid unrelated reformatting.
3. Keep layout unchanged for that collection type.
4. If updating date/title/slug, ensure filename-date consistency and links remain valid.
5. Recheck categories format and any image/video paths changed.

### 8) Update Static Pages
1. For page files (for example `about.md`, `publication.md`, `notes.html`, `gallery.html`, `shots.html`, `Vlog.html`), preserve `layout: page` and existing permalink behavior.
2. Apply minimal, scoped edits.
3. If editing category-rendered list pages (`notes.html`, `gallery.html`, `shots.html`, `Vlog.html`), preserve hyphen display logic:
   - `replace: "-", " "`
4. Verify modified links and referenced assets exist.

### 9) Update Main Page / Sidebar Navigation
1. Main page changes: edit `index.html` only in targeted sections.
2. Sidebar changes: edit `_includes/sidebar.html` and preserve existing manual link order style unless user asks otherwise.
3. Current sidebar includes: Home, Notes, Shots, Gallery, Publication, About.
4. If adding/removing nav items, verify permalink targets exist and maintain social links include.

### 10) Pre-Commit Validation Rules
1. YAML front matter parses successfully.
2. `layout` value exists in `_layouts/` and matches collection.
3. Filename matches `YYYY-MM-DD-Title-With-Hyphens.md`.
4. Filename date matches front matter `date`.
5. Categories follow site convention (space-separated tokens; hyphenated multi-word values).
6. Referenced local images/videos/files actually exist.
7. For figs/shots, Liquid relative URL prefix is present.

## Do / Don't

### Do
- Do keep edits minimal and targeted.
- Do preserve existing writing style and structure patterns.
- Do keep front matter field names and order consistent.
- Do use layout mapping strictly by collection.
- Do validate file paths and dates before final output.

### Don't
- Don't fabricate conventions not present in site references.
- Don't change unrelated files when updating one piece of content.
- Don't introduce new metadata schemas unless requested.
- Don't use YAML list syntax for categories in this site unless user explicitly requests a schema migration.
- Don't break gallery/video HTML wrapper patterns used by existing layouts.

## Artifacts / Outputs
- New or updated Markdown/HTML file(s) in the requested site location.
- Optional short change summary with:
  - target files,
  - what changed,
  - validation checks performed,
  - remaining user decisions (if any).

## Quality Checklist
- [ ] Correct target location selected (`_posts`, `_blogs`, `_figs`, `_shots`, `_vlogs`, or static page).
- [ ] Front matter fields present and in expected order.
- [ ] Layout value matches collection (`post/blog/fig/shot/vlog`).
- [ ] Filename format valid (`YYYY-MM-DD-Title-With-Hyphens.md`).
- [ ] Filename date equals front matter date.
- [ ] Categories use site convention.
- [ ] All referenced local assets exist.
- [ ] Figs/shots image paths use `{{ '/' | relative_url }}` prefix.
- [ ] Vlog embeds include markdown link plus `<div class="video">` iframe block.
- [ ] Navigation updates preserve sidebar structure and valid permalinks.

## Conventions Quick-Reference

### Front Matter by Collection (Exact Field Order)
| Collection | Field Order | Layout | Typical Asset Path |
|---|---|---|---|
| `_posts/` | `layout`, `title`, `date`, `categories`, `comments` | `post` | Usually external URLs or `public/fig_post/<folder>/...` |
| `_blogs/` | `layout`, `title`, `date`, `categories`, `comments` | `blog` | Often external URLs; optional local figures |
| `_figs/` | `layout`, `title`, `date`, `categories`, `comments` | `fig` | `public/fig_post/<FolderName>/<file>` |
| `_shots/` | `layout`, `title`, `date`, `categories`, `comments` | `shot` | `public/shots/<YYYY-MM-DD-slug>/<file>` |
| `_vlogs/` | `layout`, `title`, `date`, `categories`, `comments` | `vlog` | Bilibili link + iframe embed |

### Naming and Style Rules
- Filename pattern: `YYYY-MM-DD-Title-With-Hyphens.md`.
- Date format: `YYYY-MM-DD`.
- Category naming: space-separated values; multi-word display names should be hyphen-separated in source.
- Category display behavior: templates replace `-` with spaces.
- Title emphasis pattern: `<span style='color:#e32724'>...</span>`.

### Verified Asset Path Conventions
- Figs: `public/fig_post/Black-and-White/...`, `public/fig_post/Logo/...`, `public/fig_post/Messiness/...`.
- Shots: `public/shots/2023-03-23-Daily-life/...`.

## Inline Templates

### Template: `_posts/` (`post-template.md`)
```md
---
layout: post
title:  "Your Post Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---

<!-- Save as: YYYY-MM-DD-Your-Title.md in _posts/ -->
<!-- Known categories: Learning-notes, My-toolbox, Paper. Use hyphen-separated multi-word categories. -->
<!-- For emphasis, use: <span style='color:#e32724'>keyword</span> in the title -->
<!-- Images go in: public/fig_post/your-slug/ when using local assets -->

> One-sentence summary of the post.

---

# I. Main Topic

## 1. Background

Write context, goals, and assumptions.

### 1.1 Key Point

Use inline math like $x \in \mathbb{R}^{n}$ when needed.

## 2. Method

```
# Example command or code block (existing convention: no language token)
pip install your-package
```

Display math example:

$$
\min_{u} \sum_{k=0}^{N-1} \|y_k-y^r\|_Q^2 + \|u_k\|_R^2
$$

## 3. Results

- Add an image: ![result figure](https://example.com/your-image.png)
- Add a related link: [Project link](https://example.com)

## 4. Notes

Add version notes, references, or license details if needed.
```

### Template: `_blogs/` (`blog-template.md`)
```md
---
layout: blog
title:  "Your Blog Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---

<!-- Save as: YYYY-MM-DD-Your-Title.md in _blogs/ -->
<!-- Known categories: DeePC, WWTPs. Space-separated for multiple categories. -->
<!-- Blog posts appear in timeline_2.md (/timeline_personal/) -->
<!-- Images go in: public/fig_post/your-slug/ or external URLs depending on content -->

> One-paragraph summary of this research/project update.

---

# I. Project Context

## 1. Problem Setup

Describe system, objective, and constraints.

## 2. Main Update

- What changed since the last update
- Why it matters
- Current limitations

## 3. Technical Snapshot

```
# Example command or snippet
python run_experiment.py --config configs/default.yaml
```

Math example: $y = f(u)$

$$
\tilde{u} = [u_1, u_2, u_1^2, u_2^2]^T
$$

## 4. Figure and Links

![progress figure](https://example.com/progress.png)

- [Repository](https://example.com)
- [Related notes](/notes/)
```

### Template: `_figs/` (`fig-template.md`)
```md
---
layout: fig
title:  "Your Artwork Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---

<!-- Save as: YYYY-MM-DD-Your-Title.md in _figs/ -->
<!-- Known categories: Freshness, B&W, Logo. -->
<!-- Images go in: public/fig_post/Your-Folder-Name/ -->
<!-- Image path format: {{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image.jpg -->

> Short note about this artwork series.

---

<div class="gallery">
<h1> Series Title 1 </h1>
<img align='center' src="{{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image1.jpg" width='800'>

<h1> Series Title 2 </h1>
<img align='center' src="{{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image2.jpg" width='800'>

<h1> Vertical Cover </h1>
<img align='center' src="{{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image3.jpg" width='500'>
</div>
```

### Template: `_shots/` (`shot-template.md`)
```md
---
layout: shot
title:  "Your Photo Series Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---

<!-- Save as: YYYY-MM-DD-Your-Title.md in _shots/ -->
<!-- Known categories: Daido-Moriyama. -->
<!-- Images go in: public/shots/YYYY-MM-DD-Your-Title/ -->
<!-- Image path format: {{ '/' | relative_url }}public/shots/YYYY-MM-DD-Your-Title/1.jpg -->

> Brief description of the photo set.

---

<div class="gallery">
    <h1>Frame 1</h1>
    <img align='center' src="{{ '/' | relative_url }}public/shots/YYYY-MM-DD-Your-Title/1.jpg" width='500'>

    <h1>Frame 2</h1>
    <img align='center' src="{{ '/' | relative_url }}public/shots/YYYY-MM-DD-Your-Title/2.jpg" width='500'>

    <h1>Frame 3</h1>
    <img align='center' src="{{ '/' | relative_url }}public/shots/YYYY-MM-DD-Your-Title/3.jpg" width='500'>
</div>
```

### Template: `_vlogs/` (`vlog-template.md`)
```md
---
layout: vlog
title:  "Your Vlog Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---

<!-- Save as: YYYY-MM-DD-Your-Title.md in _vlogs/ -->
<!-- Known categories: Big-day. -->
<!-- Title styling: use <span style='color:#e32724'>keyword</span> for emphasis -->
<!-- Vlog page (Vlog.html) is NOT currently in sidebar navigation -->
<!-- Video embeds use Bilibili iframe inside <div class="video"> wrapper -->

> One-line summary of this vlog episode.

---

[Watch on Bilibili](https://www.bilibili.com/video/YOUR_VIDEO_ID)

<div class="video">
<iframe src="https://player.bilibili.com/player.html?bvid=YOUR_BV_ID&page=1&high_quality=1"
  scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true">
</iframe>
</div>
```

## Common Pitfalls (From Validation Report)
- Three existing files have filename-date mismatch warnings; avoid adding new mismatches:
  - `_posts/2023-02-07-Matlab-plot.md` (front matter date `2023-02-27`)
  - `_figs/2023-02-03-Messiness.md` (front matter date `2023-02-26`)
  - `_vlogs/2024-01-02-Bye-Bye-2023.md` (front matter date `2024-01-01`)
- `/vlogs/` exists as a page permalink but is currently not shown in sidebar navigation.
- Bundler/Jekyll local build may fail in this environment due to Bundler version mismatch (`2.5.7` required by `Gemfile.lock`), so rely on content-level checks if build tooling is unavailable.
- Internal content-to-content links are sparse; when useful, add meaningful internal links to improve navigability.

## Examples

### Example A: Create a new post
User request: "Create a new note about Koopman lifting for DeePC."
1. Create `_posts/YYYY-MM-DD-Koopman-Lifting-for-DeePC.md`.
2. Use post template with `layout: post`, `comments: true`.
3. Set title, date, and categories such as `Learning-notes DeePC`.
4. Keep opening blockquote summary and sectioned technical structure.
5. Validate YAML, filename-date match, and links/assets.

### Example B: Create a new figure entry
User request: "Add a new gallery entry for a Logo iteration."
1. Create `_figs/YYYY-MM-DD-Logo-Iteration.md`.
2. Use `layout: fig` and gallery block format.
3. Put images in `public/fig_post/Logo-Iteration/`.
4. Reference each image with `{{ '/' | relative_url }}public/fig_post/Logo-Iteration/<file>`.
5. Validate image files exist and front matter is complete.

### Example C: Update sidebar navigation
User request: "Expose Vlogs in sidebar."
1. Edit `_includes/sidebar.html`.
2. Add a nav link for `/vlogs/` in requested order.
3. Preserve existing style/classes and social links include.
4. Verify `Vlog.html` permalink remains `/vlogs/`.
5. Confirm only sidebar file changed for this operation.
