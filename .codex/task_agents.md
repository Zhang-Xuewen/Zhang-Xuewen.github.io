# AGENTS.md — QY-Web (Run 2)

## Original Objectives

You are an assistant responsible for managing a personal website hosted on GitHub Pages (github.io). Your role is to help create new posts, update existing pages, and modify website content according to the user's instructions. When generating or editing content, follow the user's previous writing style, tone, and formatting so that new updates remain consistent with the existing posts and structure of the site. Ensure the output is suitable for directly integrating into the website files (e.g., Markdown) and only modify what is necessary.

## Completed Work

- **Site conventions audit**: 609-line reference documenting all 5 collections, layouts, navigation, asset paths, writing style, and categories (`001_audit-site-conventions/site-conventions.md`)
- **Site integrity validation**: All 14 content files validated — 0 YAML errors, 0 missing fields, 0 missing layouts; 3 legacy filename-date mismatches documented (`002_validate-site-integrity/`)
- **Content templates**: 5 collection-specific templates (post, blog, fig, shot, vlog) + quick-reference guide (`003_create-content-templates/templates/`)
- **qyweb_editing skill v1**: 418-line skill deployed to 3 locations — but created manually, not via skill_creator; missing references/ subfolder and proper skill structure
- **CLAUDE.md**: Project-level instructions referencing qyweb_editing skill
- **Git .gitignore**: `.codex/` folder added to .gitignore

## Frozen — Do NOT Modify

- `.codex/subtask/001_audit-site-conventions/site-conventions.md` — Authoritative 609-line conventions reference
- `.codex/subtask/002_validate-site-integrity/validation-report.md` — Complete validation report
- `.codex/subtask/002_validate-site-integrity/frontmatter-validation.json` — Structured validation data
- `.codex/subtask/003_create-content-templates/templates/post-template.md` — Verified post template
- `.codex/subtask/003_create-content-templates/templates/blog-template.md` — Verified blog template
- `.codex/subtask/003_create-content-templates/templates/fig-template.md` — Verified fig template
- `.codex/subtask/003_create-content-templates/templates/shot-template.md` — Verified shot template
- `.codex/subtask/003_create-content-templates/templates/vlog-template.md` — Verified vlog template
- `.codex/subtask/003_create-content-templates/templates/quick-reference.md` — Verified quick-reference
- `CLAUDE.md` — Project-level skill reference (may need minor update if skill name changes)
- All site content files (`_posts/`, `_blogs/`, `_figs/`, `_shots/`, `_vlogs/`, static pages) — Do not modify any website content

## Improvement Tasks

### Task 1: Remove .codex files from Git tracking

**What**: Remove all `.codex/` files from Git's index so they are no longer tracked, while keeping them on disk.

**Where**: Git index for the QY-Web repository at `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/QiYuan's Web-github`

**Why**: Human instruction — `.codex/` has been added to `.gitignore` but files already tracked in Git remain tracked. They must be removed from the index.

**How**:
1. Run `git rm -r --cached .codex/` to remove `.codex/` from Git tracking without deleting the files on disk.
2. Verify with `git status` that `.codex/` files show as deleted from index but `.codex/` itself appears in the untracked/ignored section.
3. Do NOT commit this change on its own — only commit if there are other meaningful project changes to include. If `.codex/` removal is the only change, skip the commit (the next real content commit will pick it up naturally).

**Acceptance criteria**:
- `git ls-files .codex/` returns empty (no tracked files)
- `.codex/` folder still exists on disk with all contents intact
- `.gitignore` includes `.codex/` (already done)

### Task 2: Recreate qyweb_editing skill using skill_creator

**What**: Delete the current manually-created qyweb_editing skill and recreate it properly using the `skill_creator` skill. The new skill must follow the standard skill folder structure with YAML frontmatter, examples/templates, and a `references/` subfolder.

**Where**:
- Skill source: use the `skill_creator` skill to generate
- Deploy to all 3 locations:
  1. `/Users/qy/.claude/skills/qyweb_editing/SKILL.md` (Claude Code skills)
  2. `/Users/qy/.codex/skills/qyweb_editing/SKILL.md` (Codex skills)
  3. `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/qyweb_editing/SKILL.md` (workflow backup)

**Why**: Human instruction — "the generated skill is not right, use the skill skill_creator to generate, need to follow the skill format and give example/templates, like the other skill"

**How**:
1. Invoke the `skill_creator` skill to create a new qyweb_editing skill.
2. Use the existing content from `.codex/subtask/004_create-qyweb-skill/qyweb_editing/SKILL.md` (418 lines) as the knowledge base — it contains all the correct procedures, conventions, and validation rules.
3. The new skill MUST follow the same structural pattern as `/Users/qy/.codex/skills/imagegen/SKILL.md`:
   - YAML frontmatter with `name` and `description` fields
   - Clear sections: When to use, Workflow, Do/Don't, etc.
   - Proper trigger description in the `description` field
4. The SKILL.md should include inline examples showing how to create each content type (post, blog, fig, shot, vlog) with sample commands and expected output.
5. Delete the old single-file skill from all 3 locations before deploying the new folder-based skill.

**Reference model**: Study `/Users/qy/.codex/skills/imagegen/SKILL.md` for structure, tone, and level of detail. The imagegen skill has:
- YAML frontmatter with comprehensive trigger description
- Decision tree
- Step-by-step workflow
- Conventions section
- Dependencies section
- References to bundled files

**Acceptance criteria**:
- Skill created via skill_creator (not manually written)
- SKILL.md has YAML frontmatter with `name: "qyweb_editing"` and a comprehensive `description` trigger
- Skill covers all 5 collections + static pages + sidebar navigation
- Includes inline examples/templates for each content type
- Follows the structural pattern of the imagegen skill
- Deployed and byte-identical across all 3 locations
- Skill appears in Claude Code's active skill registry

### Task 3: Create references/ subfolder with template files

**What**: Create a `references/` subfolder inside the qyweb_editing skill folder and populate it with the content templates from subtask 003.

**Where**: Inside each of the 3 skill deployment locations:
- `/Users/qy/.claude/skills/qyweb_editing/references/`
- `/Users/qy/.codex/skills/qyweb_editing/references/`
- `/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/qyweb_editing/references/`

**Why**: Human instruction (repeated twice) — "put your generated template file into the created skill folder with a new subfolder named 'references' like the skill folder: /Users/qy/.codex/skills/imagegen"

**How**:
1. Study the imagegen skill's `references/` folder structure for the pattern:
   ```
   /Users/qy/.codex/skills/imagegen/references/
   ├── cli.md
   ├── codex-network.md
   ├── image-api.md
   ├── prompting.md
   └── sample-prompts.md
   ```
2. Create a `references/` subfolder in each qyweb_editing skill location.
3. Copy the 5 collection templates from `.codex/subtask/003_create-content-templates/templates/` into `references/`:
   - `post-template.md`
   - `blog-template.md`
   - `fig-template.md`
   - `shot-template.md`
   - `vlog-template.md`
4. Also copy the `quick-reference.md` into `references/`.
5. Optionally include the site conventions summary (a condensed version of `001_audit-site-conventions/site-conventions.md`) as `references/site-conventions.md` — keep it under 200 lines.
6. Verify all 3 skill locations have identical `references/` folder contents.

**Acceptance criteria**:
- Each of the 3 skill locations has a `references/` subfolder
- `references/` contains at minimum: 5 collection templates + quick-reference.md
- Templates match the frozen originals from subtask 003
- All 3 `references/` folders are identical (verify with checksums)

## Verification

```bash
# Task 1: Verify .codex removed from git tracking
git ls-files .codex/  # Should return empty

# Task 2: Verify skill structure matches imagegen pattern
ls -la /Users/qy/.claude/skills/qyweb_editing/
ls -la /Users/qy/.codex/skills/qyweb_editing/
# Both should show: SKILL.md, references/

# Task 2: Verify YAML frontmatter
head -5 /Users/qy/.claude/skills/qyweb_editing/SKILL.md
# Should show --- / name: "qyweb_editing" / description: "..." / ---

# Task 2: Verify skill is identical across locations
shasum /Users/qy/.claude/skills/qyweb_editing/SKILL.md
shasum /Users/qy/.codex/skills/qyweb_editing/SKILL.md
shasum "/Users/qy/Library/CloudStorage/OneDrive-Personal/Documents/Interesting Projects/CodexCLI_workflow/workflow/settings/skill/qyweb_editing/SKILL.md"

# Task 3: Verify references folder
ls /Users/qy/.claude/skills/qyweb_editing/references/
# Should list: post-template.md, blog-template.md, fig-template.md, shot-template.md, vlog-template.md, quick-reference.md

# Task 3: Verify references identical across locations
diff -r /Users/qy/.claude/skills/qyweb_editing/references/ /Users/qy/.codex/skills/qyweb_editing/references/
```

## Reviewer Hints

- **Task ordering**: Task 1 (git cleanup) is independent and can run in parallel with Tasks 2–3. Tasks 2 and 3 are sequential — the skill folder must exist before references/ can be populated.
- **skill_creator usage**: Task 2 MUST use the `skill_creator` skill — do not manually write SKILL.md. Feed the skill_creator the existing 418-line skill content as source material.
- **Commit policy**: Since `.codex/` is now gitignored, only commit changes to actual project files (like CLAUDE.md updates). If the only changes are within `.codex/`, skip the commit entirely.
- **Template fidelity**: The templates in `references/` must be exact copies of the frozen originals from subtask 003. Do not modify template content.
- **Three-location sync**: After all tasks, verify byte-identical copies across all 3 deployment locations (Claude skills, Codex skills, workflow backup). Use SHA256 checksums.
