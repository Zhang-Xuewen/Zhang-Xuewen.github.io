# AGENTS.md — Subtask 002: Validate Site Content Integrity and Build Readiness

## Role

You are a validation executor. Your job is to systematically check every content file in the Jekyll site for correctness against the conventions documented in subtask 001, attempt a Jekyll build, and produce a detailed validation report. You must NOT fix any issues — only detect and report them.

## Mandatory Startup

Before any work, execute these skills in order:
1. `/workflow-bootstrap`
2. `/scope-and-safety`

Then read the following files in order:
1. `.codex/subtask/002_validate-site-integrity/subtask.md` — your task spec
2. `.codex/subtask/002_validate-site-integrity/subtask-agents.md` — this file
3. `.codex/subtask/001_audit-site-conventions/site-conventions.md` — the conventions reference (your validation baseline)
4. `.codex/subtask_activity.md` — prior activity context

## Step-by-Step Execution Plan

### Step 1: Enumerate All Content Files

Run `rg --files _posts _blogs _figs _shots _vlogs | sort` to get the full list of content files to validate.

Record the count per collection directory.

### Step 2: Validate Front Matter (Python Script)

Write and run a Python script (in-memory, not saved to the project) that:

1. For each `.md` file in `_posts/`, `_blogs/`, `_figs/`, `_shots/`, `_vlogs/`:
   - Opens the file and extracts YAML front matter (content between first `---` and second `---`)
   - Parses the YAML using `yaml.safe_load()` — report any parse errors
   - Checks required fields are present: `layout`, `title`, `date`
   - Checks `categories` field is present (warn if missing, not error)
   - Checks `comments` field is present (warn if missing)
   - Validates `layout` value is one of: `post`, `blog`, `fig`, `shot`, `vlog`, `page` (or matches a file in `_layouts/`)
   - Validates `date` is in `YYYY-MM-DD` format
2. For each file, checks filename matches `YYYY-MM-DD-*.md` pattern
3. Compares filename date prefix with front matter `date` value (warn if different)
4. Outputs results as structured text: file path, pass/fail, list of issues

Use this Python approach (run via `python3 -c '...'` or a temp script):

```python
import os, yaml, re, glob, sys

results = []
layout_files = set(os.path.splitext(f)[0] for f in os.listdir('_layouts') if f.endswith('.html'))
collections = {
    '_posts': 'post',
    '_blogs': 'blog',
    '_figs': 'fig',
    '_shots': 'shot',
    '_vlogs': 'vlog'
}

for coll_dir, expected_layout in collections.items():
    files = sorted(glob.glob(f'{coll_dir}/*.md'))
    for filepath in files:
        issues = []
        filename = os.path.basename(filepath)

        # Check filename pattern
        if not re.match(r'\d{4}-\d{2}-\d{2}-.+\.md$', filename):
            issues.append(f'Filename does not match YYYY-MM-DD-*.md pattern')

        # Extract and parse front matter
        with open(filepath, 'r') as f:
            content = f.read()

        fm_match = re.match(r'^---\s*\n(.*?)\n---', content, re.DOTALL)
        if not fm_match:
            issues.append('No valid YAML front matter found')
            results.append((filepath, issues))
            continue

        try:
            fm = yaml.safe_load(fm_match.group(1))
        except yaml.YAMLError as e:
            issues.append(f'YAML parse error: {e}')
            results.append((filepath, issues))
            continue

        if not isinstance(fm, dict):
            issues.append('Front matter is not a dictionary')
            results.append((filepath, issues))
            continue

        # Required fields
        for field in ['layout', 'title', 'date']:
            if field not in fm:
                issues.append(f'Missing required field: {field}')

        # Recommended fields
        if 'categories' not in fm:
            issues.append(f'WARN: Missing categories field')
        if 'comments' not in fm:
            issues.append(f'WARN: Missing comments field')

        # Layout validation
        if 'layout' in fm:
            if fm['layout'] not in layout_files:
                issues.append(f'Layout "{fm["layout"]}" has no matching file in _layouts/')

        # Date format
        if 'date' in fm:
            date_str = str(fm['date'])[:10]
            if not re.match(r'^\d{4}-\d{2}-\d{2}$', date_str):
                issues.append(f'Date format invalid: {fm["date"]}')

            # Compare with filename date
            fn_date_match = re.match(r'(\d{4}-\d{2}-\d{2})', filename)
            if fn_date_match and fn_date_match.group(1) != date_str:
                issues.append(f'WARN: Filename date ({fn_date_match.group(1)}) differs from front matter date ({date_str})')

        status = 'PASS' if not [i for i in issues if not i.startswith('WARN')] else 'FAIL'
        results.append((filepath, issues, status))

# Output
for item in results:
    filepath = item[0]
    issues = item[1]
    status = item[2] if len(item) > 2 else 'FAIL'
    print(f'\n{status}: {filepath}')
    if issues:
        for issue in issues:
            print(f'  - {issue}')
    else:
        print(f'  - No issues found')
```

### Step 3: Layout Reference Integrity Check

1. List all layout files: `ls _layouts/*.html`
2. Extract all `layout:` values from content files using `rg -n "^layout:" _posts/*.md _blogs/*.md _figs/*.md _shots/*.md _vlogs/*.md`
3. Cross-reference: every layout value referenced must have a corresponding file in `_layouts/`
4. Document any orphaned layouts (layouts that exist but are never referenced by any content file — note these as informational, not errors)

### Step 4: Jekyll Build Test

Attempt the Jekyll build. Follow this sequence:

1. Check if `Gemfile` exists: `ls Gemfile 2>/dev/null`
2. Check if `bundle` is available: `which bundle 2>/dev/null`
3. If bundle is available and Gemfile exists:
   - Run `bundle install --path vendor/bundle 2>&1 | tail -20` (capture output)
   - Run `bundle exec jekyll build 2>&1 | tail -40` (capture output)
4. If bundle is NOT available:
   - Try: `gem install bundler 2>&1 | tail -10` then retry
   - If gem is not available either, try: `jekyll build 2>&1 | tail -40`
   - If Jekyll is not available, document that the build test could not be performed and explain why
5. Categorize build output:
   - **Fatal errors**: anything that prevents build completion
   - **Warnings**: deprecation notices, missing optional features
   - **Success indicators**: "done" or site generation messages
6. Record the full build output in the validation report

**Important**: If Jekyll/bundler/ruby tooling is not installed, document this clearly as "Build test skipped — tooling not available" with specifics. Do NOT install gems or modify the Gemfile (forbidden action).

### Step 5: Internal Link Spot Check

1. Extract `permalink:` values from static pages: `rg -n "^permalink:" about.md publication.md notes.html gallery.html shots.html Vlog.html`
2. Compare permalink paths against sidebar navigation links from `_includes/sidebar.html`
3. Check at least 3 internal links from content files:
   - Pick links from `_posts/` or `_blogs/` content that reference other site pages
   - Verify the targets exist as files or are valid collection URLs
4. Document findings

### Step 6: Compile Validation Report

Create the validation report at `.codex/subtask/002_validate-site-integrity/validation-report.md` with these sections:

1. **Summary**: Overall pass/fail status, counts of issues by severity
2. **Front Matter Validation Results**: Per-file results table (file, status, issues)
3. **Filename Convention Results**: List any files that don't match the pattern
4. **Layout Reference Integrity**: Cross-reference results, orphaned layouts
5. **Jekyll Build Results**: Full build output, categorized errors/warnings
6. **Internal Link Spot Check**: Results of link verification
7. **Recommendations**: Prioritized list of issues to address (informational only — do NOT fix them)

### Step 7: Generate Output Manifest and Result Report

Create these files:

1. `.codex/subtask/002_validate-site-integrity/output_manifest.json` — list all output artifacts with type, description, verify_hint
2. `.codex/subtask/002_validate-site-integrity/result.md` — execution report following the standard format (actions taken, commands run, changed files, key output, acceptance check results, blockers, next steps)

## Acceptance Checks (Self-Verify Before Completing)

Before declaring completion, verify:

- [ ] All `.md` files in all 5 collection directories have been checked for YAML validity
- [ ] Every content file has been checked for required fields (layout, title, date, categories)
- [ ] Layout values have been cross-referenced against `_layouts/*.html`
- [ ] Jekyll build has been attempted OR clearly documented as skipped with reason
- [ ] Validation report exists at `.codex/subtask/002_validate-site-integrity/validation-report.md`
- [ ] Report lists specific file paths for any issues found
- [ ] No site files have been modified (read-only validation only)
- [ ] output_manifest.json and result.md have been created

## Forbidden Actions

- Do NOT modify any site content files, layouts, includes, or config
- Do NOT fix any issues found — only report them
- Do NOT install new gems or change the Gemfile
- Do NOT create files outside of `.codex/subtask/002_validate-site-integrity/`
- Do NOT commit or push anything
- Do NOT run `bundle install` if it would modify the project's Gemfile.lock in a way that breaks things — use `--path vendor/bundle` to isolate

## Output Directory

All outputs must go to: `.codex/subtask/002_validate-site-integrity/`
