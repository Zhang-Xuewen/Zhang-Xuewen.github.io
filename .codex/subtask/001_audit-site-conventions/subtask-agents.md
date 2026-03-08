# Subtask 001 Execution Instructions

## Objective

Produce a comprehensive site conventions reference document by reading and analyzing all key files in the Jekyll site.

## Steps

### Step 1: Read site configuration
- Read `_config.yml` to extract collections, plugins, pagination, permalink patterns, and site metadata.

### Step 2: Analyze content files across all collections
- Read all files in `_posts/` — note front matter fields, title formatting, category usage, date format.
- Read all files in `_blogs/` — note any differences from `_posts/`.
- Read all files in `_figs/` — note image embedding patterns.
- Read all files in `_shots/` — note photography-specific conventions.
- Read all files in `_vlogs/` — note video embedding patterns (Bilibili iframes).

### Step 3: Examine layouts and includes
- Read all files in `_layouts/` — map the inheritance hierarchy, identify shared patterns.
- Read key includes: `sidebar.html`, `head.html`, `tablecontentbar.html`, `social_links.html`.
- Note the category collector includes: `collectblogcategories.html`, `collectfigscategories.html`, etc.

### Step 4: Review static pages
- Read `about.md`, `publication.md`, `notes.html`, `gallery.html`, `shots.html`, `Vlog.html`.
- Note front matter patterns for pages vs. posts.

### Step 5: Check asset organization
- List contents of `public/css/`, `public/images/`, `public/fig_post/`, `public/shots/`.
- Note path patterns used in content files to reference images.

### Step 6: Read data files
- Read `_data/social.yml` for social link structure.

### Step 7: Analyze writing style
- From the posts read in Step 2, extract observations about:
  - Tone (technical, personal, mixed)
  - Heading depth (h2, h3 typical?)
  - Use of code blocks, math, lists
  - Link style (inline vs. reference)
  - Image embedding style

### Step 8: Compile the reference document
- Write `site-conventions.md` in `.codex/subtask/001_audit-site-conventions/`.
- Organize by the sections defined in `subtask.md`.
- Include concrete examples from actual files (with file paths).

### Step 9: Verify accuracy
- Cross-check at least 3 conventions against their source files.
- Ensure front matter examples are copied from real posts, not invented.

## Acceptance Checks

- [ ] `site-conventions.md` exists and is >200 lines
- [ ] All 5 collections documented with front matter examples from real files
- [ ] Naming convention documented with real filename examples
- [ ] Layout hierarchy accurately mapped
- [ ] Navigation/sidebar structure documented
- [ ] Asset paths documented per collection
- [ ] At least 3 conventions verified against source files

## Risks / Rollback

- **Risk**: Missing a collection or convention. **Mitigation**: Use `find` or `ls` to enumerate all directories and files systematically.
- **Rollback**: This subtask only creates files in `.codex/subtask/001_audit-site-conventions/`. Delete that directory to fully roll back.
- **Note**: This is a read-only analysis task. No site files should be modified.
