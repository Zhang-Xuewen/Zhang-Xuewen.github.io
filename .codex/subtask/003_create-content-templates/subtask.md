# Subtask 003: Create Reusable Content Templates for Each Collection Type

## Scope

Create ready-to-use Markdown template files for each of the site's 5 content types (post, blog, fig, shot, vlog), plus a quick-reference guide. Templates must precisely follow the conventions documented in subtask 001 and validated in subtask 002.

## Inputs

- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — conventions reference
- `.codex/subtask/002_validate-site-integrity/validation-report.md` — validated patterns
- Existing content files as examples (at least 1 per collection)

## Outputs

- `.codex/subtask/003_create-content-templates/templates/post-template.md`
- `.codex/subtask/003_create-content-templates/templates/blog-template.md`
- `.codex/subtask/003_create-content-templates/templates/fig-template.md`
- `.codex/subtask/003_create-content-templates/templates/shot-template.md`
- `.codex/subtask/003_create-content-templates/templates/vlog-template.md`
- `.codex/subtask/003_create-content-templates/templates/quick-reference.md`

## Template Requirements

### Each Template Must Include

1. **Front matter block** with all fields used in that collection, in the same order as existing posts:
   - `layout`: set to the correct collection layout
   - `title`: placeholder with note about HTML span styling convention
   - `date`: placeholder in `YYYY-MM-DD` format
   - `categories`: placeholder with examples of existing categories for that collection
   - `comments`: set to `true`
   - Any other fields observed in that collection

2. **Body structure** reflecting the typical content patterns:
   - Heading hierarchy (h2, h3 as typically used)
   - Placeholder sections matching the type of content
   - Image embedding example using the correct asset path for that collection
   - Code block example (for technical posts)
   - Math rendering example (for technical posts)

3. **Inline comments** (HTML comments `<!-- -->`) guiding what to fill in:
   - Filename instruction: `<!-- Save as: YYYY-MM-DD-Your-Title.md in _posts/ -->`
   - Category guidance: `<!-- Categories used: Learning-notes, My-toolbox, Paper, etc. -->`
   - Image path guidance: `<!-- Images go in: public/fig_post/your-slug/ -->`

### Quick-Reference Guide Must Include

1. When to use each collection type (posts vs. blogs vs. figs vs. shots vs. vlogs)
2. Filename pattern reminder
3. Required vs. optional front matter fields per type
4. Asset path conventions per type
5. Category naming rules (hyphen-separated, displayed with spaces)
6. Common pitfalls to avoid

## Acceptance Criteria

1. One template per collection type with correct layout and front matter fields
2. Templates use exact field names, ordering, and formatting from existing content
3. Each template includes guiding comments/placeholders
4. Templates follow the `YYYY-MM-DD-Slug.md` naming convention with instructions
5. Quick-reference guide covers when to use each collection and key conventions

## Verification

- Place a test post using the `post-template.md` into `_posts/` with a future date
- Run `bundle exec jekyll build` to confirm it builds without errors
- Remove the test post after verification

## Forbidden Actions

- Do NOT modify any existing site files
- Do NOT leave test posts in any collection folder after verification
- Do NOT create files outside of `.codex/subtask/003_create-content-templates/`
- Do NOT commit or push anything
- Do NOT introduce new front matter fields not already used in the site
