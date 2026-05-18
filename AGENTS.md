# Agent Instructions

## Repository Identity

This is the donfather.dev WebGPU portfolio site: a first-person 3D experience built with Three.js where the visitor stands in a sci-fi corridor and interacts with a wall-mounted CRT terminal to navigate portfolio content. The aesthetic reference is the Alien universe, specifically Alien: Isolation. The environment is dark, damp, industrial, and indifferent.

## Context Loading

Agents working on this repository should load context in this order:

1. This file (`AGENTS.md`), which covers repository identity, constraints, and conventions
2. `README.md` for project overview and current state
3. `docs/documentation-standards/` for templates and standards to follow
4. `internal-files/corridor-scene-concept-one-pager.md` for the full scene concept, asset manifest, and technical decisions
5. Any domain-specific docs referenced below

## Architectural Constraints

- All 3D rendering uses Three.js with WebGPURenderer, falling back to WebGLRenderer transparently. No raw WebGPU API usage.
- Total scene poly budget stays under 10k triangles. Performance on integrated graphics at 60fps is a hard requirement.
- Mobile traffic redirects to a static fallback. The 3D experience is desktop-only and uncompromised.
- External 3D assets are CC-BY-4.0 from Sketchfab. Attribution for each author must appear in the site credits. See `assets/website-assets/README.md` for the full manifest.
- Monitor content renders via CanvasTexture with a CRT shader (scan lines, phosphor bloom, curvature distortion). No DOM overlay for primary content display.
- The pin pad is reactive set dressing, not a direct input device. It animates in response to monitor navigation clicks.
- Camera vertical range is clamped: approximately -10 degrees (floor limit) to +60 degrees (ceiling). No view of where feet would be.
- No character model, hands, or body. Viewer presence is conveyed through a shadow proxy (~50 tris, invisible to camera, casts shadows).
- Audio uses Web Audio API with layered ambient loops. No heavy audio libraries.
- The corridor environment uses three instances of a single wall panel model. Room construction is composition, not modeling.

## Documentation Conventions

- All Markdown files require YAML frontmatter (see `docs/documentation-standards/tagging-strategy.md`)
  - Exempt: standard repo furniture (CONTRIBUTING.md, SECURITY.md, CODE_OF_CONDUCT.md, licenses) and source materials in `internal-files/`
- New directories require an interior README (see `docs/documentation-standards/interior-readme-template.md`)
- Script files require language-appropriate headers (see `docs/documentation-standards/script-header-*.md`)
- Follow dual-audience commenting (see `docs/documentation-standards/code-commenting-dual-audience.md`)
- Follow writing style conventions (see `docs/documentation-standards/writing-style-guide.md`)
- Agents never delete files; move unnecessary files to `recycle/` with documented justification

## Commit Messages

- Present tense, imperative mood
- 72-character first line limit
- Reference issues after first line

## Session Pattern

1. Load context (this file + README)
2. Work within defined scope
3. Document changes appropriately
4. Update work-logs if significant work completed
