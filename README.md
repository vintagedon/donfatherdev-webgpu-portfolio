<!--
---
title: "donfather.dev WebGPU Portfolio"
description: "First-person 3D portfolio site built with Three.js and WebGPU"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-05-18"
version: "1.0"
status: "Active"
tags:
  - type: project-root
  - domain: scene
  - tech: [three-js, webgpu, javascript, gltf]
related_documents:
  - "[Corridor Scene One-Pager](internal-files/corridor-scene-concept-one-pager.md)"
---
-->

# donfather.dev WebGPU Portfolio

[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

> A first-person 3D portfolio experience where visitors navigate content through a CRT terminal inside a sci-fi corridor.

The portfolio at donfather.dev puts the visitor inside a dimly lit corridor segment, facing a wall-mounted monitor rendered as a retro CRT display. Navigation happens on the screen itself: clicking sections triggers pin pad animations and transitions the terminal content. The environment is built from free CC-BY-4.0 Sketchfab assets, and the atmosphere is sold entirely through materials, lighting, and audio rather than geometric complexity. Total scene weight is under 10k triangles.

---

## Overview

Most developer portfolios are flat pages with cards and gradients. This project takes a different approach: the portfolio is a place you stand in. The aesthetic draws from the Alien universe (particularly Alien: Isolation), where spaces are industrial, insufficiently lit, and quietly neglected. The monitor glows because everything else is too dim. The corridor extends into darkness because nobody maintains the lights past this section.

The site targets desktop browsers exclusively. Mobile traffic redirects to a static fallback. The 3D scene uses Three.js with WebGPURenderer where supported, falling back to WebGL transparently. The poly budget is deliberately minimal so the experience runs at 60fps on integrated graphics; the visual quality comes from PBR materials, emissive textures, CRT shader effects, atmospheric particles, and layered ambient audio.

---

## Project Status

| Area | Status | Description |
|------|--------|-------------|
| Concept | ✅ Complete | Scene layout, aesthetic direction, interaction model defined |
| Assets | ✅ Complete | Three Sketchfab models downloaded (corridor wall, monitor, alt panel) |
| Documentation Standards | ✅ Complete | Tagging strategy, templates, writing guide hydrated |
| Project Charter | ⬜ Planned | Freeze scope and architecture from one-pager |
| Scene Prototype | ⬜ Planned | Three.js scene with corridor, lighting, camera rig |
| CRT Shader | ⬜ Planned | Scan lines, phosphor bloom, curvature, vignette |
| Content System | ⬜ Planned | CanvasTexture pipeline for monitor display |
| Interaction | ⬜ Planned | Raycasting, pin pad animation, screen transitions |
| Audio | ⬜ Planned | Ambient layers via Web Audio API |
| Deployment | ⬜ Planned | Build, hosting, mobile redirect |

---

## Architecture

The scene is composed from a small number of lightweight elements. Visual depth comes from materials and lighting, not geometry.

| Component | Implementation | Purpose |
|-----------|----------------|---------|
| Corridor | 3x Suushimi sci-fi wall sections (~5.7k tris) | Environment enclosure |
| Monitor | Dreadler Control Room Monitor (~1.7k tris) | Primary interaction surface |
| Pin pad | Procedural Three.js geometry (~200-500 tris) | Reactive navigation feedback |
| Shadow proxy | Invisible capsule mesh (~50 tris) | Viewer presence via cast shadows |
| Floor | Plane with PBR material | Reflective puddles catch monitor glow |
| CRT display | CanvasTexture with shader post-processing | Portfolio content rendered as retro terminal |
| Lighting | Overhead fluorescent + monitor emission | Insufficient warmth vs cool screen glow |
| Atmosphere | Depth fog + sprite particles | Recycled-air haze catching light |
| Audio | Web Audio API, layered loops | Electrical hum, ventilation, incidental clanks |

---

## Repository Structure

```markdown
donfatherdev-webgpu-portfolio/
├── assets/                       # Project images and 3D models
│   └── website-assets/           # glTF models for the corridor scene
├── docs/                         # Documentation
│   └── documentation-standards/  # Template library and guidelines
├── internal-files/               # One-pagers, charters, reference docs
├── recycle/                      # Removed files (never delete, always move)
├── spec/                         # Agent task specifications
├── staging/                      # Pre-commit staging area
├── work-logs/                    # Development history
├── AGENTS.md                     # Agent context loading instructions
├── CLAUDE.md                     # Pointer to AGENTS.md for Claude Code
├── LICENSE                       # MIT License (code)
├── LICENSE-DATA                  # CC-BY-4.0 (data/content)
└── README.md                     # This file
```

---

## Getting Started

Project is in the concept/planning phase. Development environment setup will be documented when the build tooling is selected (Vite is the likely choice).

```bash
# Planned setup (not yet implemented)
git clone https://github.com/vintagedon/donfatherdev-webgpu-portfolio.git
cd donfatherdev-webgpu-portfolio
npm install
npm run dev
```

---

## Asset Credits

All 3D models are sourced from Sketchfab under CC-BY-4.0 licenses.

| Model | Author | Source |
|-------|--------|--------|
| Sci-fi Wall | [Suushimi](https://sketchfab.com/Suushimi) | [Sketchfab](https://sketchfab.com/3d-models/sci-fi-wall-6b80e573801e4316bd89656e6fa51e39) |
| Control Room Monitor | [Dreadler](https://sketchfab.com/Dreadler) | [Sketchfab](https://sketchfab.com/3d-models/control-room-monitor-75d49d961e06427a9da38b81d341b39f) |
| Simple Sci-Fi Wall Panel | [Mizuchi Sensei](https://sketchfab.com/FatFreeBeefCake) | [Sketchfab](https://sketchfab.com/3d-models/simple-sci-fi-wall-panel-651ea9453d614cf6abfa7b0c09b57417) |

---

## License

- **Code**: [MIT License](LICENSE)
- **Data/Content**: [CC-BY-4.0](LICENSE-DATA)

---

Last Updated: 2026-05-18 | Status: Concept Complete, Development Planned
