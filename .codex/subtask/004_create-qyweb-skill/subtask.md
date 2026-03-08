# Subtask 004: Create QiYuan Web Editing Skill for Claude and Codex

## Scope

Consolidate all knowledge gathered from subtasks 001–003 into a single, reusable skill file that enables any AI assistant (Claude Code, Codex) to create, update, and manage content on the QiYuan's Web Jekyll/GitHub Pages site. The skill must be self-contained — an assistant reading only the skill file should be able to perform any standard content operation correctly.

## Inputs

- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — comprehensive conventions reference
- `.codex/subtask/002_validate-site-integrity/validation-report.md` — validation results and known issues
- `.codex/subtask/003_create-content-templates/templates/` — all template files and quick-reference guide
- Existing site files as needed for verification

## Outputs

The same skill file must be placed in all 4 locations:

1. `.codex/subtask/004_create-qyweb-skill/skill_qyweb_editing.md` — working copy in subtask dir
2. `/Users/qy/.claude/skills/skill_qyweb_editing.md` — Claude Code skills folder
3. `/Users/qy/.codex/skills/skill_qyweb_editing.md` — Codex skills folder
4. `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/skill_qyweb_editing.md` — backup location

## Skill File Requirements

### Standard Skill Format

The skill must follow this structure:

```
# skill_qyweb_editing

## Purpose
[What this skill enables]

## When to Use (Triggers)
[When to activate this skill]

## Inputs / Assumptions
[What the skill expects]

## Step-by-Step Procedure
[Detailed procedures for each operation type]

## Do / Don't
[Rules and constraints]

## Artifacts / Outputs
[What the skill produces]

## Quality Checklist
[Verification steps]

## Examples
[Concrete examples of common operations]
```

### Content the Skill Must Cover

1. **Site Overview**: Brief description of the QiYuan's Web site architecture (Jekyll/Hyde, 5 collections, GitHub Pages)

2. **Content Operations — Step-by-Step Procedures for**:
   - Creating a new post in `_posts/`
   - Creating a new blog entry in `_blogs/`
   - Creating a new figure post in `_figs/`
   - Creating a new shot in `_shots/`
   - Creating a new vlog in `_vlogs/`
   - Updating an existing content file
   - Updating static pages (about, publication, etc.)
   - Updating the main page / sidebar navigation

3. **Conventions Reference** (condensed from subtask 001):
   - Front matter fields per collection type (exact field names and order)
   - Filename convention: `YYYY-MM-DD-Title-With-Hyphens.md`
   - Category naming: hyphen-separated, display with spaces
   - Title styling: inline HTML `<span>` convention
   - Asset paths per collection (`public/fig_post/`, `public/shots/`, etc.)
   - Layout assignments per collection type

4. **Templates**: Include the full template for each collection type inline (from subtask 003)

5. **Validation Rules**: Key rules to check before committing new content:
   - YAML front matter is valid
   - Layout value matches an existing layout
   - Date in filename matches front matter date
   - Images referenced actually exist
   - Categories follow naming conventions

6. **Common Pitfalls**: Known issues from the validation report (subtask 002)

## Acceptance Criteria

1. Skill file is complete and self-contained — covers all 5 collection types with step-by-step creation instructions
2. Skill follows the standard skill file format (Purpose, Triggers, Procedure, Do/Don't, Examples)
3. Front matter conventions are accurate and match actual site files
4. Skill includes inline templates for each collection type
5. Skill is deployed to all 4 required locations (subtask dir + 3 external paths)
6. Skill content is verified against `site-conventions.md` for accuracy

## Verification

- Cross-check at least 3 conventions in the skill against `site-conventions.md` and actual site files
- Confirm the skill file exists and is identical in all 4 target locations
- Walk through one skill procedure mentally (e.g., "create a new post") and verify every instruction is correct

## Forbidden Actions

- Do NOT modify any existing site files (content, layouts, config, CSS)
- Do NOT modify outputs from subtasks 001–003
- Do NOT create files other than the skill file in the 4 specified locations
- Do NOT commit or push anything
- Do NOT fabricate conventions not documented in `site-conventions.md`
