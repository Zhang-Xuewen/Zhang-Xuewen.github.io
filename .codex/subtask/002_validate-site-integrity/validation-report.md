# Validation Report — Subtask 002

Date: 2026-03-09
Subtask: `002_validate-site-integrity`

## 1) Summary

- Overall status: FAIL
- Collections validated: 14 files total (`_posts`: 8, `_blogs`: 1, `_figs`: 3, `_shots`: 1, `_vlogs`: 1)
- Front matter parse failures: 0
- Front matter non-fatal warnings: 3
- Missing layout references: 0
- Orphaned layouts (informational): 4
- Build fatal errors: 1
- Build warnings: 0
- Internal link spot check: FAIL (found 2 qualifying internal links; required >= 3)

## 2) Front Matter Validation Results

| File | Status | Issues |
|---|---|---|
| `_posts/2022-09-22-Introduction-to-Casadi.md` | PASS | No issues found |
| `_posts/2023-02-07-Matlab-plot.md` | PASS | WARN: Filename date (2023-02-07) differs from front matter date (2023-02-27) |
| `_posts/2024-03-28-Introduction-to-Jekyll.md` | PASS | No issues found |
| `_posts/2024-04-15-Developed-deepctools.md` | PASS | No issues found |
| `_posts/2024-04-17-Upload-package-to-PyPI.md` | PASS | No issues found |
| `_posts/2024-04-25-Developed-modlinear.md` | PASS | No issues found |
| `_posts/2024-08-29-Developed-QYtool.md` | PASS | No issues found |
| `_posts/2024-08-30-Paper-Deep-DeePC.md` | PASS | No issues found |
| `_blogs/2024-04-05-DeePC-WWTPs.md` | PASS | No issues found |
| `_figs/2023-02-03-Messiness.md` | PASS | WARN: Filename date (2023-02-03) differs from front matter date (2023-02-26) |
| `_figs/2023-03-12-Black-and-White.md` | PASS | No issues found |
| `_figs/2024-03-29-Logo.md` | PASS | No issues found |
| `_shots/2023-03-23-Daily-life.md` | PASS | No issues found |
| `_vlogs/2024-01-02-Bye-Bye-2023.md` | PASS | WARN: Filename date (2024-01-02) differs from front matter date (2024-01-01) |

## 3) Filename Convention Results

- Filename pattern violations (`YYYY-MM-DD-*.md`): None


- Filename date vs front matter `date` mismatches: 
  - `_posts/2023-02-07-Matlab-plot.md`: Filename date (2023-02-07) differs from front matter date (2023-02-27)
  - `_figs/2023-02-03-Messiness.md`: Filename date (2023-02-03) differs from front matter date (2023-02-26)
  - `_vlogs/2024-01-02-Bye-Bye-2023.md`: Filename date (2024-01-02) differs from front matter date (2024-01-01)

## 4) Layout Reference Integrity

- Layout files in `_layouts/`: `blog`, `default`, `default_post`, `fig`, `page`, `post`, `shot`, `tagpage`, `vlog`
- Layout values referenced by content: `blog`, `fig`, `post`, `shot`, `vlog`
- Missing referenced layouts: None
- Orphaned layouts (informational only): `default`, `default_post`, `page`, `tagpage`

## 5) Jekyll Build Results

Build command attempted: `bundle exec jekyll build`

- `Gemfile` present: Yes
- `bundle` available: Yes (`/usr/bin/bundle`)
- `jekyll` binary on PATH: No
- `bundle install` not run: forbidden by subtask constraints (no gem installation during validation)
- Build result: FAIL (fatal tooling error)

### Categorized output

- Fatal errors:
  - /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/rubygems.rb:283:in `find_spec_for_exe': Could not find 'bundler' (2.5.7) required by your /Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/QiYuan's Web-github/Gemfile.lock. (Gem::GemNotFoundException)

- Warnings:
  - None

- Success indicators:
  - None


### Full build output

```text
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/rubygems.rb:283:in `find_spec_for_exe': Could not find 'bundler' (2.5.7) required by your /Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/QiYuan's Web-github/Gemfile.lock. (Gem::GemNotFoundException)
To update to the latest version installed on your system, run `bundle update --bundler`.
To install the missing version, run `gem install bundler:2.5.7`
	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/rubygems.rb:302:in `activate_bin_path'
	from /usr/bin/bundle:23:in `<main>'
```

## 6) Internal Link Spot Check

### Static page permalinks vs sidebar links

- Static page permalinks found:
  - `about.md` -> `/about/`
  - `publication.md` -> `/publication/`
  - `notes.html` -> `/notes/`
  - `gallery.html` -> `/gallery/`
  - `shots.html` -> `/shots/`
  - `Vlog.html` -> `/vlogs/`
- Sidebar navigation links found: `/`, `/about/`, `/blog/`, `/gallery/`, `/notes/`, `/publication/`, `/shots/`
- Permalinks missing from sidebar: `/vlogs/`

### Content-file internal links (spot check)

1. `_posts/2024-08-30-Paper-Deep-DeePC.md` -> `#license` (valid)
2. `_posts/2024-08-30-Paper-Deep-DeePC.md` -> `#citation` (valid)

Result: FAIL — fewer than 3 internal content links were available to verify.

## 7) Recommendations (Informational, No Fixes Applied)

1. Resolve tooling mismatch by installing Bundler `2.5.7` (or aligning `Gemfile.lock` with installed bundler) in a controlled environment, then rerun `bundle exec jekyll build`.
2. Review and align filename date/front matter `date` in the 3 mismatch files to reduce metadata ambiguity.
3. Add at least 3 explicit internal links in posts/blogs to core pages (`/notes/`, `/gallery/`, `/publication/`, etc.) to satisfy integrity spot checks.
4. Decide whether `/vlogs/` should be exposed in sidebar navigation; currently it exists as a permalink but not in sidebar.

## Notes

- Mandatory prerequisite merge with `origin/main` was completed before validation (`8072bd8`).
- Validation task made no direct content/layout/config edits; only read-only checks plus report artifacts under `.codex/subtask/002_validate-site-integrity/`.
