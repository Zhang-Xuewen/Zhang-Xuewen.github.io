# Subtask 004 Execution Instructions (REVISION 2)

## CRITICAL: Human Instruction — Skill Format Must Change

The previous iteration produced a standalone `skill_qyweb_editing.md` file. The human says:
> "the generate skill is not right, use the skill skill_creator to generate, need to follow the skill format and give example/templates, like the other skill, also need to create a separate skill folder for this created skill"

**What this means:**
1. The skill must be a **folder** named `qyweb_editing/` containing a `SKILL.md` file — NOT a standalone `.md` file.
2. `SKILL.md` must have **YAML frontmatter** with `name` and `description` fields.
3. The skill content must follow the same format as other skills (e.g., `paper_writing/SKILL.md`, `pdf/SKILL.md`).
4. Old standalone `skill_qyweb_editing.md` files must be **removed** from all deployment locations.

## Objective

Recreate the QiYuan Web editing skill in the correct skill-creator folder format and deploy to all 3 external locations.

## Reference: Correct Skill Folder Structure

```
qyweb_editing/
└── SKILL.md          # Required — YAML frontmatter + skill body
```

### SKILL.md YAML Frontmatter (REQUIRED)

```yaml
---
name: qyweb-editing
description: Create, update, and manage content on QiYuan's Web (Jekyll/Hyde on GitHub Pages). Use this skill whenever the user asks to create new posts, blogs, figures, photo shots, or vlogs, edit existing content files, update the main page or sidebar navigation, fix front matter issues, or manage image/video assets for the site. Trigger for any mention of QiYuan's Web, the Jekyll site, or content collections (_posts, _blogs, _figs, _shots, _vlogs).
---
```

## Steps

### Step 0: Clean up old standalone skill files

Remove the old standalone `skill_qyweb_editing.md` from all locations:
- `rm -f /Users/qy/.claude/skills/skill_qyweb_editing.md`
- `rm -f /Users/qy/.codex/skills/skill_qyweb_editing.md`
- `rm -f "/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/skill_qyweb_editing.md"`

### Step 1: Read all upstream artifacts

- Read `.codex/subtask/001_audit-site-conventions/site-conventions.md` — primary conventions source.
- Read `.codex/subtask/002_validate-site-integrity/validation-report.md` — common pitfalls and known issues.
- Read all template files in `.codex/subtask/003_create-content-templates/templates/` — to embed in the skill.
- Read `.codex/subtask/003_create-content-templates/templates/quick-reference.md` — collection type usage guide.
- Read the PREVIOUS iteration's skill file at `.codex/subtask/004_create-qyweb-skill/skill_qyweb_editing.md` — reuse its content but restructure into the correct format.

### Step 2: Read reference skills for format guidance

- Read `/Users/qy/.claude/skills/paper_writing/SKILL.md` — example of correct folder-based skill format with YAML frontmatter.
- Note the pattern: YAML frontmatter (`name`, `description`) at top, then standard sections.

### Step 3: Read key site files for verification

- Read `_config.yml` to verify collection configuration.
- Read one example file from each collection for front matter verification.
- Read `_includes/sidebar.html` to verify navigation structure.

### Step 4: Create the skill in folder format

1. Create directory: `.codex/subtask/004_create-qyweb-skill/qyweb_editing/`
2. Create `SKILL.md` inside that directory with:
   - **YAML frontmatter** (name: `qyweb-editing`, description: comprehensive trigger description)
   - **All standard sections**: Purpose, When to Use (Triggers), Inputs/Assumptions, Step-by-Step Procedure, Do/Don't, Artifacts/Outputs, Quality Checklist, Examples
   - **Conventions Quick-Reference** table (front matter fields, layouts, asset paths per collection)
   - **Inline Templates** for all 5 collection types (post, blog, fig, shot, vlog)
   - **Common Pitfalls** from validation report
   - **Concrete Examples** showing real usage scenarios

3. The skill content should be essentially the same as the previous iteration's `skill_qyweb_editing.md` — the CONTENT was correct, only the FORMAT was wrong. Restructure, don't rewrite from scratch.

### Step 5: Deploy to all locations as folders

Create the skill folder at each location:
1. `.codex/subtask/004_create-qyweb-skill/qyweb_editing/SKILL.md` (already created in Step 4)
2. `/Users/qy/.claude/skills/qyweb_editing/SKILL.md`
3. `/Users/qy/.codex/skills/qyweb_editing/SKILL.md`
4. `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/qyweb_editing/SKILL.md`

Use `mkdir -p` to create directories, then `cp` the SKILL.md to each.
Verify all copies are identical using `diff -q` or SHA256.

### Step 6: Final verification

- Confirm all 3 external `qyweb_editing/SKILL.md` files exist and are identical.
- Confirm old standalone `skill_qyweb_editing.md` files are removed from all 3 external locations.
- Confirm YAML frontmatter has `name` and `description` fields.
- Confirm no site files were modified.

## Acceptance Checks

- [ ] Old standalone `skill_qyweb_editing.md` removed from all 3 external locations
- [ ] `qyweb_editing/SKILL.md` exists in `.codex/subtask/004_create-qyweb-skill/`
- [ ] `SKILL.md` has YAML frontmatter with `name` and `description` fields
- [ ] Skill covers all 5 collection types with step-by-step creation procedures
- [ ] Skill includes inline templates for each collection type
- [ ] Skill follows standard folder-based format matching other skills (paper_writing, pdf, etc.)
- [ ] Skill deployed as folder to `/Users/qy/.claude/skills/qyweb_editing/`
- [ ] Skill deployed as folder to `/Users/qy/.codex/skills/qyweb_editing/`
- [ ] Skill deployed as folder to workflow settings backup path
- [ ] All 3 external copies are identical to the subtask working copy
- [ ] No site files were modified

## Risks / Rollback

- **Risk**: Old standalone files left behind. **Mitigation**: Step 0 explicitly removes them.
- **Risk**: YAML frontmatter missing or malformed. **Mitigation**: Copy exact frontmatter from Step 4 template.
- **Rollback**: Delete `qyweb_editing/` folders from all locations.
- **Note**: This subtask writes files outside the project path (to skills folders). This is explicitly requested by the human instruction.
