<!--
---
title: "Repository Hydration Pass: Interior READMEs, Licenses, and Writing Standards"
description: "Complete remaining scaffolding hydration before initial commit"
author: "https://github.com/vintagedon/"
date: "2026-05-18"
version: "1.0"
status: "Ready"
tags:
  - type: specification
  - domain: documentation
  - tech: [markdown]
related_documents:
  - "[AGENTS.md](../AGENTS.md)"
  - "[Tagging Strategy](../docs/documentation-standards/tagging-strategy.md)"
  - "[Writing Style Guide](../docs/documentation-standards/writing-style-guide.md)"
  - "[Interior README Template](../docs/documentation-standards/interior-readme-template.md)"
  - "[Corridor Scene One-Pager](../internal-files/corridor-scene-concept-one-pager.md)"
---
-->

## Task: Repository Hydration Pass

Mode: Documentation

---

### Objective

All remaining template-era placeholder content in the repository is replaced with project-specific content. Interior READMEs reflect the actual purpose of each directory within a WebGPU portfolio project. License files carry the correct year and author. Every Markdown file in the repository passes the writing style guide (no em dashes, no negation parallelism, no inflated significance, no editorializing prefaces, no superficial analysis clauses, no bold-keyword-colon bullet lists). The repository is ready for initial commit to GitHub at `https://github.com/vintagedon/donfatherdev-webgpu-portfolio`.

---

### Execution Environment

| Field | Value |
|-------|-------|
| Host | GitHub (Codex cloud sandbox) |
| OS | N/A (file-only task) |
| Agent Runtime | Codex |

---

### Scope

**Pre-existing (do not create):**

- Repository structure (all directories already exist)
- `AGENTS.md` (already hydrated)
- `README.md` (already hydrated)
- `assets/README.md` (already hydrated)
- `assets/website-assets/README.md` (already hydrated)
- `docs/documentation-standards/tagging-strategy.md` (already hydrated)
- `docs/documentation-standards/` template files (already updated with correct repo URLs)

**Modify:**

- `docs/README.md` (update from generic template content to project-specific)
- `work-logs/README.md` (update domain tag from `documentation` to match project vocabulary)
- `staging/README.md` (update if still template-generic)
- `recycle/README.md` (update if still template-generic)
- `spec/README.md` (update if still template-generic)
- `internal-files/` (create interior README; currently has none)
- `LICENSE` (fill `[Year]` and `[Author/Organization]` placeholders)
- `LICENSE-DATA` (fill `[Year]` and `[Author/Organization]` placeholders)
- All `.md` files in the repository (writing style compliance pass)

**Reference:**

- `AGENTS.md` for project identity and constraints
- `README.md` for project overview
- `docs/documentation-standards/writing-style-guide.md` for prose rules
- `docs/documentation-standards/interior-readme-template.md` for README structure
- `docs/documentation-standards/tagging-strategy.md` for allowed tag values
- `internal-files/corridor-scene-concept-one-pager.md` for project context

**Do not touch:**

- `AGENTS.md` (already hydrated by orchestrator)
- `README.md` (already hydrated by orchestrator)
- `assets/README.md` and `assets/website-assets/README.md` (already hydrated)
- `docs/documentation-standards/tagging-strategy.md` (already hydrated)
- Template files in `docs/documentation-standards/` (already correct)
- Any files in `assets/website-assets/` subdirectories (model files, textures, licenses)
- `.gitignore`, `.markdownlint.json`, `cspell.json`, `.vscode/`
- `CLAUDE.md` (intentionally minimal, pointer only)

---

### Deliverables & Validation

#### Deliverable 1: Interior READMEs

Update the following interior READMEs to reflect this project's actual content and purpose. Use the interior README template as the structural guide. Domain tags must come from the tagging strategy.

**`docs/README.md`:** Currently references the template repo. Update the description to reflect that this is documentation for a WebGPU portfolio project. The tree in Contents should match the actual directory contents.

**`work-logs/README.md`:** Functional as-is, but update the domain tag from `documentation` to whichever project domain tag is most appropriate (likely keep `documentation` since work logs are meta-content). Remove the `README-pending.md` file if it still exists in `work-logs/` (it was a placeholder marker).

**`staging/README.md`:** Check if still template-generic. Update to project context if needed.

**`recycle/README.md`:** Check if still template-generic. Update to project context if needed.

**`spec/README.md`:** Check if still template-generic. Update to project context if needed.

**`internal-files/README.md`:** This directory currently has no README. Create one following the interior README template. It contains the corridor scene one-pager and will hold future charters and reference materials. Domain tag: `documentation`.

Validation:

- [ ] `docs/README.md` does not reference "template repository," "RadioAstronomy.io," or other template-era content
- [ ] `internal-files/README.md` exists and follows the interior README template structure
- [ ] All interior READMEs have valid YAML frontmatter with tags from the tagging strategy
- [ ] All interior READMEs have accurate Contents trees matching actual directory contents
- [ ] `work-logs/README-pending.md` is removed (if it exists)

---

#### Deliverable 2: License Files

Update both license files with the correct year and author.

**`LICENSE` (MIT):** Replace `[Year]` with `2026`. Replace `[Author/Organization]` with `VintageDon (https://github.com/vintagedon/)`.

**`LICENSE-DATA` (CC-BY-4.0):** Replace `[Year]` with `2026`. Replace `[Author/Organization]` with `VintageDon (https://github.com/vintagedon/)`.

Do not change any other content in these files.

Validation:

- [ ] `LICENSE` contains `Copyright (c) 2026 VintageDon`
- [ ] `LICENSE-DATA` contains `Copyright (c) 2026 VintageDon`
- [ ] No `[Year]` or `[Author/Organization]` placeholders remain in either file

---

#### Deliverable 3: Writing Style Compliance Pass

Read `docs/documentation-standards/writing-style-guide.md` in full. Then review every `.md` file in the repository (excluding files in `docs/documentation-standards/` since those are templates with intentional placeholder patterns, and excluding files in `assets/website-assets/` subdirectories since those are third-party license files).

For each file, check for and fix:

- Em dashes (replace with commas, colons, semicolons, parentheses, or restructure)
- "Not just X, but Y" / "not X, it's Y" negation parallelism (state the point directly)
- Inflated significance terms listed in the writing guide
- Editorializing prefaces listed in the writing guide
- Superficial analysis clauses: trailing -ing clauses that restate what the main clause implies
- Transition word crutches listed in the writing guide
- Bold-keyword-colon bullet lists (the AI pattern where every bullet starts with a bolded keyword followed by a colon restating the keyword)

This is a light pass. If existing prose is clean, leave it alone. Only fix clear violations.

Validation:

- [ ] No em dash characters (Unicode U+2014) appear in any `.md` file outside of `docs/documentation-standards/` template files
- [ ] No negation-parallelism constructions appear in project-authored content
- [ ] No inflated significance words from the writing guide's avoid list appear in project-authored content

---

#### Deliverable 4: Worklog

Write a worklog following the template at `docs/documentation-standards/worklog-readme-template.md`. Filename: `work-logs/worklog-2026-05-18-repo-hydration-pass.md`. This is the first worklog in the repository.

Validation:

- [ ] Worklog exists at `work-logs/worklog-2026-05-18-repo-hydration-pass.md`
- [ ] Worklog frontmatter has all required fields populated
- [ ] Worklog lists all files modified in this spec execution

---

### Constraints

- Do not modify any file listed in the "Do not touch" scope section
- Do not change the structure or section numbering of any existing document; only update content within existing sections
- Tag values must come exclusively from `docs/documentation-standards/tagging-strategy.md`
- Writing style fixes must not change the meaning or technical accuracy of existing content
- Keep interior READMEs lean; do not add sections for completeness

---

### Execution Order

1. Deliverable 2: License Files (quick, no dependencies)
2. Deliverable 1: Interior READMEs (requires reading project context)
3. Deliverable 3: Writing Style Compliance Pass (requires all content to be in final form)
4. Deliverable 4: Worklog (captures all changes from deliverables 1-3)

---

### Notes

This spec covers the standard "last mile" of repository hydration: the work that happens after the orchestrator (Claude.ai) has handled the strategic documents (AGENTS.md, primary README, tagging strategy, one-pager) and before the initial commit. It is a repeatable pattern across repos: fill license placeholders, write any missing interior READMEs, run a writing style compliance pass, and log the work. Future repos will use a similar spec structure for this phase.

The `CONTRIBUTING.md`, `SECURITY.md`, and `CODE_OF_CONDUCT.md` files are standard repo furniture carried from the project template. They are functional as-is and do not need project-specific hydration. They are exempt from YAML frontmatter requirements per the convention in AGENTS.md.
