<!--
---
title: "Tagging Strategy Guide"
description: "Controlled vocabulary for document classification"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-05-18"
version: "1.0"
tags:
  - type: guide
  - domain: documentation
related_documents:
  - "[Primary README Template](primary-readme-template.md)"
  - "[Interior README Template](interior-readme-template.md)"
  - "[General KB Template](general-kb-template.md)"
  - "[Worklog README Template](worklog-readme-template.md)"
  - "[One-Pager Template](one-pager-template.md)"
  - "[Project Charter Template](project-charter-template.md)"
---
-->

# Tagging Strategy Guide

## 1. Purpose

This guide defines the controlled tag vocabulary for the donfatherdev-webgpu-portfolio repository. Consistent tagging enables human navigation and RAG system retrieval. All Markdown files use YAML frontmatter with tags drawn exclusively from this vocabulary.

---

## 2. Why Controlled Vocabulary

Uncontrolled tagging leads to synonyms fragmenting search (`shader` vs `shaders` vs `glsl`), inconsistent granularity (`threejs` vs `3d-rendering`), and tag proliferation that reduces signal. A controlled vocabulary defines allowed values upfront, ensuring consistency across contributors and time.

---

## 3. Tag Categories

Each category answers a different question about the document. Keep categories orthogonal; each captures a distinct dimension.

| Category | Question Answered | Required |
|----------|-------------------|----------|
| `type` | What kind of document is this? | Yes |
| `domain` | What subject area? | Yes |
| `status` | What's the lifecycle state? | Recommended |
| `tech` | What technologies involved? | When applicable |

---

## 4. Domain Tags

```yaml
domain:
  - scene           # 3D scene composition, corridor layout, camera, lighting, fog, particles
  - assets          # Model sourcing, textures, audio files, fonts, glTF pipeline
  - shaders         # CRT shader, material authoring, post-processing effects
  - interaction     # Monitor content system, pin pad, raycasting, hover/click behavior
  - content         # Portfolio sections (Projects, About, Contact), in-universe presentation
  - build           # Build tooling, bundling, deployment, hosting, CI/CD
  - design          # Aesthetic direction, visual references, UX decisions, mood/tone
  - documentation   # Templates, standards, meta-content about the repo itself
```

### Boundary Rules

- `scene` covers the spatial environment: geometry placement, camera rig, lighting setup, atmospheric effects. If it lives in the Three.js scene graph, it's scene.
- `shaders` covers GPU-side material and post-processing work. The CRT effect, custom materials, and any GLSL/TSL authoring. Distinct from `scene` because shader work is reusable across scene elements.
- `assets` covers sourcing, licensing, format conversion, and optimization of external files (models, textures, audio). Once an asset is placed in the scene, further work on it falls under `scene` or `shaders`.
- `interaction` covers the user-facing behavior: what happens when you click, hover, or look at something. The content system that drives the monitor display lives here too.
- `content` covers the actual portfolio information presented on the CRT. The words, data, and section structure, not the rendering technique (that's `shaders` or `interaction`).
- `design` covers aesthetic decisions, mood boards, reference material (Alien/Isolation), and UX choices. Design informs scene and shaders but captures the reasoning separately.
- `build` covers everything from `npm install` to production deployment. Vite config, hosting, mobile redirect logic, performance optimization.
- If a document spans two domains, use the primary one. Multi-value only when genuinely split.

---

## 5. Type Tags

| Tag | Use For |
|-----|---------|
| `project-root` | Repository root README |
| `directory-readme` | Interior README for any directory |
| `worklog` | Work log entries and milestone documentation |
| `charter` | Project charter (frozen scope and architectural commitments) |
| `one-pager` | Ideation capture (portable context unit for AI handoffs) |
| `guide` | Step-by-step procedures and how-to documents |
| `reference` | Lookup information: inventories, schemas, asset manifests |
| `specification` | Service specs, deployment definitions, formal requirements |
| `report` | Analysis, findings, audit results, summaries |

---

## 6. Status Tags

| Tag | Description |
|-----|-------------|
| `draft` | In development, not yet complete |
| `active` | Current, maintained, approved |
| `under-review` | Scheduled or triggered review in progress |
| `deprecated` | Superseded, avoid for new work |
| `archived` | Historical reference only |

---

## 7. Tech Tags

```yaml
tech:
  - three-js        # Three.js renderer, scene graph, loaders, controls
  - webgpu          # WebGPU API, WebGPURenderer
  - webgl           # WebGL fallback path
  - javascript      # Vanilla JS or general JS
  - typescript      # TypeScript (if adopted)
  - glsl            # GLSL shader code
  - tsl             # Three.js Shading Language (TSL/node materials)
  - gltf            # glTF/GLB model format, GLTFLoader
  - vite            # Vite build tooling
  - web-audio       # Web Audio API for ambient sound
  - css             # Styling for HTML overlay elements
  - html            # HTML structure, mobile fallback
```

---

## 8. Implementation

### Standard Frontmatter

```yaml
<!--
---
title: "Document Title"
description: "What this document covers"
author: "VintageDon (https://github.com/vintagedon/)"
date: "YYYY-MM-DD"
version: "1.0"
status: "Active"
tags:
  - type: guide
  - domain: scene
  - tech: three-js
related_documents:
  - "[Related Doc](path/to/doc.md)"
---
-->
```

### Conventions

- Use lowercase, hyphenated values (`web-audio` not `WebAudio` or `webaudio`)
- Tech tags use canonical names from the list above
- One value per line for readability, or array syntax for multi-value
- `related_documents` links use relative paths within the repo

---

## 9. Maintaining the Vocabulary

### Adding New Tags

1. Check if an existing tag covers the concept
2. If not, add the new tag with a boundary definition to this document
3. Backfill existing documents if the new tag applies retroactively

### Governance

- This document is the authoritative source for allowed tag values
- Prefer broader tags over proliferating specific ones
- Review additions for overlap with existing tags

---

## 10. References

| Resource | Description |
|----------|-------------|
| [Primary README Template](primary-readme-template.md) | Shows tag usage in repository root READMEs |
| [Interior README Template](interior-readme-template.md) | Shows tag usage in directory READMEs |
| [General KB Template](general-kb-template.md) | Shows tag usage for standalone docs |
| [Worklog README Template](worklog-readme-template.md) | Shows tag usage for work log entries |
| [One-Pager Template](one-pager-template.md) | Shows tag usage for ideation documents |
| [Project Charter Template](project-charter-template.md) | Shows tag usage for project charters |
