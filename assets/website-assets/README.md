<!--
---
title: "Website Assets"
description: "3D models, textures, and licenses for the corridor scene"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-05-18"
version: "1.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: assets
  - tech: gltf
---
-->

# Website Assets

3D models sourced from Sketchfab for the corridor scene on donfather.dev. Each subdirectory contains the Sketchfab download package: GLB (binary glTF, production use), separated glTF + BIN (scene graph + geometry), source files (original author format), textures (PBR maps), and a license file with attribution requirements.

All models are licensed CC-BY-4.0. Attribution for each author must appear in the site credits.

---

## 1. Contents

```
website-assets/
├── control-room-monitor/       # Wall-mounted monitor (hero interactive element)
│   ├── control_room_monitor.glb
│   ├── scene.gltf + scene.bin
│   ├── source/
│   ├── textures/
│   └── license.txt
├── scfi-wall/                  # Corridor wall section (primary environment)
│   ├── sci-fi_wall.glb
│   ├── scene.gltf + scene.bin
│   ├── source/
│   ├── textures/
│   └── license.txt
├── simple-scifi-wall-panel/    # Alternate wall panel with emission maps
│   ├── simple_sci-fi_wall_panel.glb
│   ├── scene.gltf + scene.bin
│   ├── source/
│   ├── textures/
│   └── license.txt
└── README.md                   # This file
```

---

## 2. Asset Inventory

| Asset | Author | License | Triangles | Role |
|-------|--------|---------|-----------|------|
| [Control Room Monitor](control-room-monitor/) | [Dreadler](https://sketchfab.com/Dreadler) | CC-BY-4.0 | ~1,700 | Wall-mounted CRT display, primary interaction surface |
| [Sci-fi Wall](scfi-wall/) | [Suushimi](https://sketchfab.com/Suushimi) | CC-BY-4.0 | ~1,900 | Corridor wall section (x3 for environment) |
| [Simple Sci-Fi Wall Panel](simple-scifi-wall-panel/) | [Mizuchi Sensei](https://sketchfab.com/FatFreeBeefCake) | CC-BY-4.0 | TBD | Alternate panel option with built-in emission mapping |

---

## 3. Usage Notes

### Production Format

Use the `.glb` files for Three.js loading via `GLTFLoader`. GLB is the binary glTF container: single file, no external dependencies, fastest load. The separated `.gltf` + `.bin` + `/textures/` structure is the unpacked equivalent, useful for inspecting the scene graph or selectively replacing textures.

### Texture Maps

Each model includes PBR texture sets. Key maps by model:

**control-room-monitor:** Base color, normal, metallic/roughness for monitor housing. The screen surface mesh material will be replaced at runtime with a dynamic CanvasTexture (CRT shader).

**scfi-wall:** Base color, normal, metallic/roughness, and emissive maps. The emissive textures provide built-in glowing accent lines on the wall panels.

**simple-scifi-wall-panel:** Base color, normal, and emissive maps. The emission map (`WallpanelEmission.png`) provides edge-lit panel accents.

### Scene Graph

After loading, traverse the glTF scene to identify named meshes for interaction targets (screen surface on the monitor) and material replacement. Mesh names will be documented during the prototyping phase.

---

## 4. Attribution Requirements

All three models require author credit per CC-BY-4.0. Each `license.txt` contains the exact attribution text. These credits must appear in the site (either in a dedicated credits section on the CRT terminal or in page metadata).

| Author | Model | Sketchfab Profile |
|--------|-------|-------------------|
| Dreadler | Control Room Monitor | https://sketchfab.com/Dreadler |
| Suushimi | Sci-fi Wall | https://sketchfab.com/Suushimi |
| Mizuchi Sensei | Simple Sci-Fi Wall Panel | https://sketchfab.com/FatFreeBeefCake |

---

## 5. Related

| Document | Relationship |
|----------|--------------|
| [Assets](../README.md) | Parent directory |
| [Corridor Scene One-Pager](../../internal-files/corridor-scene-concept-one-pager.md) | Scene concept with asset manifest and poly budget |
