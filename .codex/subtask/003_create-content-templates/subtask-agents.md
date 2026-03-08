# AGENTS.md — Subtask 003: Create Reusable Content Templates for Each Collection Type

## Role

You are a template creator. Your job is to produce ready-to-use Markdown template files for each of the site's 5 content types, plus a quick-reference guide. All templates must precisely follow the conventions documented in the site-conventions.md reference and validated in subtask 002.

## Mandatory Startup

Before any work, execute these skills in order:
1. `/workflow-bootstrap`
2. `/scope-and-safety`

Then read the following files in order:
1. `.codex/subtask/003_create-content-templates/subtask.md` — your task spec
2. `.codex/subtask/003_create-content-templates/subtask-agents.md` — this file
3. `.codex/subtask/001_audit-site-conventions/site-conventions.md` — the conventions reference (your authoritative source)
4. `.codex/subtask/002_validate-site-integrity/validation-report.md` — validation findings
5. `.codex/subtask_activity.md` — prior activity context
6. `.codex/reviewer/next_step.json` — reviewer instructions

## Step-by-Step Execution Plan

### Step 1: Read Existing Content Examples

Read at least one real content file from each collection to understand the exact structure:

- `_posts/2024-08-29-Developed-QYtool.md` — example post with HTML title styling
- `_posts/2022-09-22-Introduction-to-Casadi.md` — example technical post with code/math
- `_blogs/2024-04-05-DeePC-WWTPs.md` — example blog
- `_figs/2024-03-29-Logo.md` — example fig post
- `_shots/2023-03-23-Daily-life.md` — example shots post
- `_vlogs/2024-01-02-Bye-Bye-2023.md` — example vlog post

Pay attention to:
- Exact front matter field names and ordering
- How content is structured (headings, images, code blocks, iframes)
- Spacing and formatting patterns

### Step 2: Create Template Directory

```bash
mkdir -p .codex/subtask/003_create-content-templates/templates
```

### Step 3: Create Post Template

Create `.codex/subtask/003_create-content-templates/templates/post-template.md`

The post template must include:

**Front matter** (exact field order from existing posts):
```yaml
---
layout: post
title:  "Your Post Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---
```

**Guide comments** (HTML comments):
- Filename instruction: `<!-- Save as: YYYY-MM-DD-Your-Title.md in _posts/ -->`
- Category guidance: `<!-- Known categories: Learning-notes, My-toolbox, Paper. Use hyphen-separated multi-word categories. -->`
- Title styling note: `<!-- For emphasis, use: <span style='color:#e32724'>keyword</span> in the title -->`

**Body structure** reflecting typical post patterns:
- `#` heading for major section
- `##` and `###` for subsections (technical posts use Roman numeral prefixes like I., II., III.)
- Triple-backtick code block example (no language token, matching existing convention)
- Inline math example: `$...$`
- Display math example using `$$...$$`
- Image embedding example: `![description](image-url)`
- Link example: `[text](url)`

### Step 4: Create Blog Template

Create `.codex/subtask/003_create-content-templates/templates/blog-template.md`

**Front matter**:
```yaml
---
layout: blog
title:  "Your Blog Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---
```

**Guide comments**:
- `<!-- Save as: YYYY-MM-DD-Your-Title.md in _blogs/ -->`
- `<!-- Known categories: DeePC, WWTPs. Space-separated for multiple categories. -->`
- `<!-- Blog posts appear in timeline_2.md (/timeline_personal/) -->`

**Body**: Similar to post but oriented toward project/research commentary.

### Step 5: Create Fig Template

Create `.codex/subtask/003_create-content-templates/templates/fig-template.md`

**Front matter**:
```yaml
---
layout: fig
title:  "Your Artwork Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---
```

**Guide comments**:
- `<!-- Save as: YYYY-MM-DD-Your-Title.md in _figs/ -->`
- `<!-- Known categories: Freshness, B&W, Logo. -->`
- `<!-- Images go in: public/fig_post/Your-Folder-Name/ -->`
- `<!-- Image path format: {{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image.jpg -->`

**Body**: Image gallery pattern using the Liquid relative_url approach observed in existing fig posts:
```markdown
<img src="{{ '/' | relative_url }}public/fig_post/Your-Folder-Name/image1.jpg">
```

### Step 6: Create Shot Template

Create `.codex/subtask/003_create-content-templates/templates/shot-template.md`

**Front matter**:
```yaml
---
layout: shot
title:  "Your Photo Series Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---
```

**Guide comments**:
- `<!-- Save as: YYYY-MM-DD-Your-Title.md in _shots/ -->`
- `<!-- Known categories: Daido-Moriyama. -->`
- `<!-- Images go in: public/shots/YYYY-MM-DD-Your-Title/ -->`
- `<!-- Image path format: {{ '/' | relative_url }}public/shots/YYYY-MM-DD-Your-Title/1.jpg -->`

**Body**: Photo grid/series pattern matching existing shot posts.

### Step 7: Create Vlog Template

Create `.codex/subtask/003_create-content-templates/templates/vlog-template.md`

**Front matter**:
```yaml
---
layout: vlog
title:  "Your Vlog Title"
date:   YYYY-MM-DD
categories: Category-Name
comments: true
---
```

**Guide comments**:
- `<!-- Save as: YYYY-MM-DD-Your-Title.md in _vlogs/ -->`
- `<!-- Known categories: Big-day. -->`
- `<!-- Title styling: use <span style='color:#e32724'>keyword</span> for emphasis -->`
- `<!-- Vlog page (Vlog.html) is NOT currently in sidebar navigation -->`

**Body**: Bilibili video embedding pattern:
```html
[Watch on Bilibili](https://www.bilibili.com/video/YOUR_VIDEO_ID)

<div class="video">
<iframe src="https://player.bilibili.com/player.html?bvid=YOUR_BV_ID&page=1&high_quality=1"
  scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true">
</iframe>
</div>
```

### Step 8: Create Quick-Reference Guide

Create `.codex/subtask/003_create-content-templates/templates/quick-reference.md`

Include these sections:

1. **When to Use Each Collection Type**
   - `_posts/`: Technical notes, learning notes, toolbox announcements, paper publications — displayed on Notes page (`/notes/`)
   - `_blogs/`: Research project commentary and extended discussions — displayed on Blog page (`/blog/`) via pagination, and in personal timeline (`/timeline_personal/`)
   - `_figs/`: Artwork, digital art, photography art — displayed on Gallery page (`/gallery/`)
   - `_shots/`: Street photography series, photo collections — displayed on Shots page (`/shots/`)
   - `_vlogs/`: Video logs (Bilibili embeds) — displayed on Vlog page but NOT in sidebar

2. **Filename Pattern**
   - `YYYY-MM-DD-Title-With-Hyphens.md`
   - Date in filename SHOULD match the `date` field in front matter (3 existing mismatches noted in validation)

3. **Required vs Optional Front Matter Fields**

   | Field | Required | Notes |
   |-------|----------|-------|
   | `layout` | Yes | Must match collection: `post`, `blog`, `fig`, `shot`, `vlog` |
   | `title` | Yes | May include `<span style='color:#e32724'>...</span>` for emphasis |
   | `date` | Yes | Format: `YYYY-MM-DD` |
   | `categories` | Yes | Space-separated, hyphen-joined multi-word (e.g., `Learning-notes`) |
   | `comments` | Yes | Always `true` in existing content |
   | `tags` | Optional | Supported by tag system but not currently used in content |

4. **Asset Path Conventions**
   - Posts: External image URLs or inline
   - Figs: `public/fig_post/<FolderName>/<file>` — use `{{ '/' | relative_url }}` prefix
   - Shots: `public/shots/<YYYY-MM-DD-slug>/<file>` — use `{{ '/' | relative_url }}` prefix
   - Vlogs: Bilibili iframe embed inside `<div class="video">` wrapper

5. **Category Naming Rules**
   - Multi-word categories use hyphens: `Learning-notes`, `My-toolbox`, `Big-day`, `Daido-Moriyama`
   - Display templates convert hyphens to spaces: `Learning-notes` → `Learning notes`
   - Multiple categories are space-separated: `categories: DeePC WWTPs`
   - Known categories per collection listed in each template

6. **Common Pitfalls**
   - Don't use YAML list syntax `[cat1, cat2]` for categories — use space-separated string
   - Keep filename date consistent with front matter `date` to avoid confusion
   - Don't forget `comments: true` — Disqus comments are gated by this field
   - Image paths in figs/shots must use Liquid `{{ '/' | relative_url }}` prefix for correct base URL resolution
   - Don't add categories not following the hyphen-naming pattern if they contain spaces
   - Vlog page `/vlogs/` is not currently linked in sidebar navigation

### Step 9: Verify Template Quality

After creating all templates, verify:

1. Read back each template file and check:
   - Front matter is valid YAML (parseable)
   - Field order matches existing content conventions
   - Layout value is correct for the collection
   - Guide comments are present and accurate
   - Body structure includes relevant examples

2. Run a Python validation check on all template files:
```python
import yaml, re, os, glob

templates = glob.glob('.codex/subtask/003_create-content-templates/templates/*.md')
for t in templates:
    if t.endswith('quick-reference.md'):
        continue
    with open(t) as f:
        content = f.read()
    fm_match = re.match(r'^---\s*\n(.*?)\n---', content, re.DOTALL)
    if not fm_match:
        print(f'FAIL: {t} - no front matter')
        continue
    try:
        fm = yaml.safe_load(fm_match.group(1))
        print(f'PASS: {t} - layout={fm.get("layout")}, fields={list(fm.keys())}')
    except:
        print(f'FAIL: {t} - YAML parse error')
```

3. **Build verification** (best effort):
   - The Jekyll build environment may not be available locally (Bundler 2.5.7 not installed — see subtask 002 findings).
   - If `bundle exec jekyll build` works, test by temporarily copying `post-template.md` to `_posts/2099-01-01-Template-Test.md`, building, and removing it.
   - If the build environment is unavailable, document this and skip the build verification. This is acceptable given the known environment constraint from subtask 002.

### Step 10: Generate Output Manifest and Result Report

Create these files:

1. `.codex/subtask/003_create-content-templates/output_manifest.json` — list all output artifacts with type, description, verify_hint
2. `.codex/subtask/003_create-content-templates/result.md` — execution report (actions taken, commands run, changed files, key output, acceptance check results, next steps)

## Acceptance Checks (Self-Verify Before Completing)

Before declaring completion, verify:

- [ ] 5 template files exist: `post-template.md`, `blog-template.md`, `fig-template.md`, `shot-template.md`, `vlog-template.md`
- [ ] `quick-reference.md` exists with all 6 required sections
- [ ] Each template has valid YAML front matter with correct `layout` value
- [ ] Front matter field order matches existing content: `layout`, `title`, `date`, `categories`, `comments`
- [ ] Each template includes HTML comment guides for filename, categories, and asset paths
- [ ] Templates reference the `YYYY-MM-DD-Slug.md` naming convention
- [ ] No existing site files have been modified
- [ ] All output files are within `.codex/subtask/003_create-content-templates/`
- [ ] `output_manifest.json` and `result.md` have been created

## Forbidden Actions

- Do NOT modify any existing site files
- Do NOT leave test posts in any collection folder after verification
- Do NOT create files outside of `.codex/subtask/003_create-content-templates/`
- Do NOT commit or push anything
- Do NOT introduce new front matter fields not already used in the site
- Do NOT fabricate categories or conventions not documented in site-conventions.md

## Output Directory

All outputs must go to: `.codex/subtask/003_create-content-templates/`
