# Quick Reference: QiYuan's Web Content Templates

## 1. When to Use Each Collection Type

- `_posts/`: Technical notes, learning notes, toolbox announcements, paper publications. Displayed on Notes page (`/notes/`).
- `_blogs/`: Research project commentary and extended discussions. Displayed on Blog page (`/blog/`) and personal timeline (`/timeline_personal/`).
- `_figs/`: Artwork, digital art, photography art. Displayed on Gallery page (`/gallery/`).
- `_shots/`: Street photography series and photo collections. Displayed on Shots page (`/shots/`).
- `_vlogs/`: Video logs (Bilibili embeds). Displayed on Vlog page (`/vlogs/`), not linked in sidebar navigation.

## 2. Filename Pattern

- Use `YYYY-MM-DD-Title-With-Hyphens.md`.
- Date in filename should match the `date` field in front matter.
- Existing validation found 3 date mismatches in older files; avoid adding new mismatches.

## 3. Required vs Optional Front Matter Fields

| Field | Required | Notes |
|-------|----------|-------|
| `layout` | Yes | Must match collection: `post`, `blog`, `fig`, `shot`, `vlog` |
| `title` | Yes | May include `<span style='color:#e32724'>...</span>` for emphasis |
| `date` | Yes | Format: `YYYY-MM-DD` |
| `categories` | Yes | Space-separated, hyphen-joined multi-word (e.g., `Learning-notes`) |
| `comments` | Yes | Always `true` in existing content |
| `tags` | Optional | Supported by tag system but not currently used in content |

## 4. Asset Path Conventions

- Posts: usually external image URLs or inline markdown images.
- Figs: `public/fig_post/<FolderName>/<file>` with `{{ '/' | relative_url }}` prefix.
- Shots: `public/shots/<YYYY-MM-DD-slug>/<file>` with `{{ '/' | relative_url }}` prefix.
- Vlogs: Bilibili iframe embed inside `<div class="video">` wrapper.

## 5. Category Naming Rules

- Multi-word categories use hyphens, e.g., `Learning-notes`, `My-toolbox`, `Big-day`, `Daido-Moriyama`.
- Display templates convert hyphens to spaces, e.g., `Learning-notes` -> `Learning notes`.
- Multiple categories are space-separated, e.g., `categories: DeePC WWTPs`.
- Use known categories per collection as shown in each template.

## 6. Common Pitfalls

- Do not use YAML list syntax like `[cat1, cat2]` for categories; use a space-separated string.
- Keep filename date and front matter `date` consistent.
- Do not omit `comments: true`; comments rendering depends on it.
- In figs/shots, keep the Liquid prefix `{{ '/' | relative_url }}` for correct URL resolution.
- Avoid categories with spaces; use hyphen-separated form instead.
- Remember `/vlogs/` exists but is not currently linked in sidebar navigation.
