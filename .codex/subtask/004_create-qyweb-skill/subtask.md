# Subtask 004: Create QiYuan Web Editing Skill for Claude and Codex (REVISION 2)

## Human Instruction (2026-03-09 00:57)

> "the generate skill is not right, use the skill skill_creator to generate, need to follow the skill format and give example/templates, like the other skill, also need to create a separate skill folder for this created skill"

## What Changed from Iteration 1

- The skill must be a **folder** (`qyweb_editing/`) containing `SKILL.md` — NOT a standalone `.md` file
- `SKILL.md` must have **YAML frontmatter** with `name` and `description` fields
- Old standalone `skill_qyweb_editing.md` files must be **removed** from all deployment locations
- The skill CONTENT from iteration 1 was correct — only the FORMAT/structure needs to change

## Scope

Restructure the QiYuan Web editing skill into the correct skill-creator folder format (`qyweb_editing/SKILL.md` with YAML frontmatter) and redeploy to all target locations. Remove old standalone format files.

## Inputs

- `.codex/subtask/004_create-qyweb-skill/skill_qyweb_editing.md` — previous iteration's content (reuse, don't rewrite)
- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — conventions reference
- `.codex/subtask/002_validate-site-integrity/validation-report.md` — validation results and known issues
- `.codex/subtask/003_create-content-templates/templates/` — template files
- `/Users/qy/.claude/skills/paper_writing/SKILL.md` — reference for correct folder-based skill format

## Outputs

The skill must be deployed as a FOLDER at each location:

1. `.codex/subtask/004_create-qyweb-skill/qyweb_editing/SKILL.md` — working copy
2. `/Users/qy/.claude/skills/qyweb_editing/SKILL.md` — Claude Code skills
3. `/Users/qy/.codex/skills/qyweb_editing/SKILL.md` — Codex skills
4. `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/qyweb_editing/SKILL.md` — backup

Old standalone files to REMOVE:
- `/Users/qy/.claude/skills/skill_qyweb_editing.md`
- `/Users/qy/.codex/skills/skill_qyweb_editing.md`
- `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/skill_qyweb_editing.md`

## Required SKILL.md Format

```yaml
---
name: qyweb-editing
description: Create, update, and manage content on QiYuan's Web (Jekyll/Hyde on GitHub Pages). Use this skill whenever the user asks to create new posts, blogs, figures, photo shots, or vlogs, edit existing content files, update the main page or sidebar navigation, fix front matter issues, or manage image/video assets for the site.
---
```

Followed by the standard skill sections:
- Purpose
- When to Use (Triggers)
- Inputs / Assumptions
- Step-by-Step Procedure (per collection type + static pages + navigation)
- Do / Don't
- Artifacts / Outputs
- Quality Checklist
- Conventions Quick-Reference (table)
- Inline Templates (all 5 collection types)
- Common Pitfalls
- Examples (concrete scenarios)

## Acceptance Criteria

1. Skill is organized as a folder `qyweb_editing/` containing `SKILL.md` — NOT a standalone `.md` file
2. `SKILL.md` has YAML frontmatter with `name` and `description` fields
3. Skill content is complete and self-contained (all 5 collection types, procedures, templates, examples)
4. Skill is deployed as folders to all 3 external target locations
5. Old standalone `skill_qyweb_editing.md` files are removed from all 3 external locations
6. Skill content is verified against `site-conventions.md` for accuracy

## Forbidden Actions

- Do NOT modify any existing site files (content, layouts, config, CSS)
- Do NOT modify outputs from subtasks 001–003
- Do NOT commit or push anything
- Do NOT fabricate conventions not documented in `site-conventions.md`
