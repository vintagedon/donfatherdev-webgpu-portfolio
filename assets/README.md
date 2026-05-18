<!--
---
title: "Assets"
description: "Project images, banners, and 3D assets for the portfolio site"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-05-18"
version: "1.1"
status: "Active"
tags:
  - type: directory-readme
  - domain: assets
---
-->

# Assets

Project images, banners, and 3D model assets. Repository-level visual resources (banners, infographics) live at the top level. The `website-assets/` subdirectory holds glTF/GLB models and their textures for the 3D corridor scene.

---

## 1. Contents

```
assets/
├── website-assets/                  # 3D models for the corridor scene
│   └── README.md
├── background-section-infographic.jpg
├── repo-banner.jpg
└── README.md                        # This file
```

---

## 2. Files

| File | Description | Status |
|------|-------------|--------|
| [repo-banner.jpg](repo-banner.jpg) | Repository banner image | ✅ Active |
| [background-section-infographic.jpg](background-section-infographic.jpg) | Background/context infographic | ✅ Active |

---

## 3. Subdirectories

| Directory | Description |
|-----------|-------------|
| [website-assets/](website-assets/README.md) | 3D models (glTF/GLB), textures, and licenses for the corridor scene |

---

## 4. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory |
| [Corridor Scene One-Pager](../internal-files/corridor-scene-concept-one-pager.md) | Asset requirements and manifest |

---

## 5. Conventions

**Naming:** Use descriptive, lowercase, hyphenated filenames: `architecture-diagram.png`, `project-banner.svg`.

**Formats:** Prefer SVG for diagrams and icons, PNG for screenshots and complex images. GLB for production 3D models (single-file binary glTF). Avoid large uncompressed formats.

**References:** Link assets from markdown using relative paths: `![Alt text](assets/filename.png)` from the repo root, or `![Alt text](../assets/filename.png)` from a subdirectory.
