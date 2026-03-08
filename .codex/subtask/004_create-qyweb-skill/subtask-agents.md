# Subtask 004 Execution Instructions

## Objective

Create a comprehensive, self-contained QiYuan Web editing skill file and deploy it to all 4 required locations.

## Steps

### Step 1: Read all upstream artifacts
- Read `.codex/subtask/001_audit-site-conventions/site-conventions.md` — this is the primary source for conventions.
- Read `.codex/subtask/002_validate-site-integrity/validation-report.md` — extract common pitfalls and known issues.
- Read all template files in `.codex/subtask/003_create-content-templates/templates/` — these will be embedded in the skill.
- Read `.codex/subtask/003_create-content-templates/templates/quick-reference.md` — for the collection type usage guide.

### Step 2: Read key site files for verification
- Read `_config.yml` to verify collection configuration references in the skill.
- Read one example file from each collection (`_posts/`, `_blogs/`, `_figs/`, `_shots/`, `_vlogs/`) to verify front matter conventions.
- Read `_includes/sidebar.html` to verify navigation structure references.

### Step 3: Draft the skill file
- Create `skill_qyweb_editing.md` in `.codex/subtask/004_create-qyweb-skill/`.
- Follow the standard skill file format from `subtask.md`.
- Structure the skill with these major sections:
  1. **Purpose** — managing QiYuan's Web Jekyll site content
  2. **When to Use (Triggers)** — triggered when user asks to create/edit website content, add posts, update pages
  3. **Inputs / Assumptions** — project path, Jekyll site structure exists
  4. **Step-by-Step Procedure** — organized by operation type:
     - Subsection per collection type (post, blog, fig, shot, vlog) with create/update steps
     - Static page update procedure
     - Main page / navigation update procedure
  5. **Conventions Quick-Reference** — condensed table of front matter fields, layouts, asset paths per collection
  6. **Inline Templates** — full template content for each collection type
  7. **Validation Checklist** — rules to check before committing
  8. **Do / Don't** — safety rules
  9. **Common Pitfalls** — from validation report
  10. **Examples** — concrete examples of "create a new post about X" walkthrough

### Step 4: Verify skill accuracy
- Cross-check front matter fields in the skill against `site-conventions.md` for each collection type.
- Cross-check at least 2 asset path conventions against actual site directories.
- Walk through the "create a new post" procedure and verify each instruction is correct.

### Step 5: Deploy to all locations
- Copy the skill file to all 4 target locations:
  1. `.codex/subtask/004_create-qyweb-skill/skill_qyweb_editing.md` (already created in Step 3)
  2. `/Users/qy/.claude/skills/skill_qyweb_editing.md`
  3. `/Users/qy/.codex/skills/skill_qyweb_editing.md`
  4. `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/skill_qyweb_editing.md`
- Create target directories if they don't exist.
- Verify all 4 copies are identical using diff or checksum.

### Step 6: Final verification
- Confirm all 4 files exist and have the same content.
- Verify the skill file is >150 lines (it should be comprehensive).
- Confirm no site files were modified.

## Acceptance Checks

- [ ] `skill_qyweb_editing.md` exists in `.codex/subtask/004_create-qyweb-skill/`
- [ ] Skill covers all 5 collection types with step-by-step creation procedures
- [ ] Skill includes inline templates for each collection type
- [ ] Skill follows standard format (Purpose, Triggers, Procedure, Do/Don't, Examples)
- [ ] Front matter conventions verified against `site-conventions.md`
- [ ] Skill deployed to `/Users/qy/.claude/skills/`
- [ ] Skill deployed to `/Users/qy/.codex/skills/`
- [ ] Skill deployed to workflow settings backup path
- [ ] All 4 copies are identical
- [ ] No site files were modified

## Risks / Rollback

- **Risk**: Inaccurate conventions in the skill. **Mitigation**: Always reference `site-conventions.md` as the source of truth; cross-check against actual site files.
- **Risk**: Target directories don't exist. **Mitigation**: Create them with `mkdir -p` before copying.
- **Rollback**: Delete `skill_qyweb_editing.md` from all 4 locations. The subtask dir can be removed entirely.
- **Note**: This subtask writes files outside the project path (to skills folders). This is explicitly requested by the human instruction and is the intended behavior.
