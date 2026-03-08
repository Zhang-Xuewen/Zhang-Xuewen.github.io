# Subtask 002: Validate Site Content Integrity and Build Readiness

## Scope

Validate that all content files in the Jekyll site have correct front matter, consistent conventions, and that the site can build without fatal errors. Produce a validation report documenting any issues found.

## Inputs

- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — conventions reference (from subtask 001)
- All content files: `_posts/`, `_blogs/`, `_figs/`, `_shots/`, `_vlogs/`
- `_layouts/` — to verify layout references
- `_config.yml` — to verify collection configuration
- `Gemfile` — for Jekyll build dependencies

## Outputs

- `.codex/subtask/002_validate-site-integrity/validation-report.md` — detailed validation results

## Validation Checks to Perform

### 1. Front Matter Validation
For every `.md` file in `_posts/`, `_blogs/`, `_figs/`, `_shots/`, `_vlogs/`:
- YAML front matter is parseable (no syntax errors)
- Required fields present: `layout`, `title`, `date`
- `layout` value matches an existing file in `_layouts/`
- `date` is in valid `YYYY-MM-DD` format
- `categories` field is present (may be empty but should exist)

### 2. Filename Convention Check
- All content filenames match `YYYY-MM-DD-*.md` pattern
- Date in filename is consistent with `date` in front matter

### 3. Layout Reference Integrity
- Every `layout` value referenced in front matter has a corresponding `.html` file in `_layouts/`
- No orphaned layouts (layouts that exist but are never referenced — document but don't flag as error)

### 4. Jekyll Build Test
- Run `bundle exec jekyll build` in the project directory
- Capture and categorize output: errors vs. warnings
- Document any build failures with specific error messages

### 5. Internal Link Spot Check
- Check that `permalink` values in static pages correspond to actual navigation links in `sidebar.html`
- Verify at least 3 internal links from content files point to valid targets

## Acceptance Criteria

1. All content files have valid YAML front matter (no parse errors)
2. Every content file has required fields: layout, title, date, categories
3. Layout values match actual layout files in `_layouts/`
4. Jekyll build completes without fatal errors (warnings acceptable but documented)
5. Validation report lists any issues found with specific file paths and descriptions

## Verification

- Run a YAML front matter validation across all content files using Python
- Attempt `bundle exec jekyll build` and capture output
- Report includes pass/fail status per file

## Forbidden Actions

- Do NOT modify any site content files, layouts, includes, or config
- Do NOT fix any issues found — only report them
- Do NOT install new gems or change the Gemfile
- Do NOT create files outside of `.codex/subtask/002_validate-site-integrity/`
- Do NOT commit or push anything
