# donfather.dev WebGPU Portfolio: Corridor Scene Concept

**Domain:** Web Development, 3D Portfolio, WebGPU/Three.js
**Status:** Concept validated, ready for technical architecture
**Date:** 2026-05-18
**Version:** 1.0

---

## Vision

A first-person 3D portfolio site styled after the Alien/Isolation aesthetic: the visitor stands in a dimly lit sci-fi corridor, interacting with a wall-mounted CRT monitor and pin pad to navigate portfolio content. The environment sells itself through materials, lighting, and atmosphere rather than geometric complexity. Total scene poly budget under 10k triangles. Desktop-only experience; mobile traffic redirects to a static fallback.

---

## Scene Architecture

### Corridor Layout

Three instances of the same wall panel model arranged end-to-end forming a corridor tube. The visitor's camera is positioned in the center section. Left and right sections provide parallax depth when the camera rotates, fading to darkness at the corridor ends.

**Wall panel asset:** Suushimi's "Sci-fi wall" from Sketchfab (free, CC-BY-like license). ~1.9k triangles per section. Total environment geometry: ~5.7k tris.

- Sketchfab URL: https://sketchfab.com/3d-models/sci-fi-wall-6b80e573801e4316bd89656e6fa51e39
- Format: glTF/GLB via Sketchfab export

### Interactive Props

**Main monitor:** Dreadler's "Control Room Monitor" from Sketchfab (free, CC Attribution). 1.7k triangles, 1k vertices. Mounted to the center wall section, filling most of the forward view. Screen surface gets its material replaced with a dynamic CanvasTexture rendered as a CRT display (green or amber monochrome, scan lines, phosphor bloom, slight curvature distortion, vignette).

- Sketchfab URL: https://sketchfab.com/3d-models/control-room-monitor-75d49d961e06427a9da38b81d341b39f
- Format: glTF/GLB via Sketchfab export

**Pin pad:** Procedurally built in Three.js. ~200-500 tris. Flat housing, 12 extruded button faces, small seven-segment LED readout strip (amber/green digits via CanvasTexture). Mounted to the wall left of the monitor.

**Interaction model:** User clicks navigation items on the monitor screen (Projects, About, Contact, etc). On click, the pin pad buttons physically depress in an automated sequence (translating button meshes inward a few mm on Z axis), digits appear on the readout, and the monitor transitions to the selected content view. The pin pad is reactive set dressing, not a direct input device. Each content section triggers a different key sequence, as though each has its own access code.

### Content Presentation

All content stays in-character with the aesthetic. The monitor isn't showing a web page; it's a ship/station terminal.

| Section | In-universe presentation |
|---------|--------------------------|
| About | Personnel file on the CRT |
| Projects | System status readouts |
| Contact | Communication terminal |

**Screen transitions:** CRT scan-line wipe (content draws top-to-bottom) or brief static burst then resolve. The shader-based transition masks the content swap moment. Hard cuts feel wrong for CRT; the phosphor persistence effect should be visible.

### Camera Constraints

| Axis | Range | Rationale |
|------|-------|-----------|
| Horizontal | ~90 degrees left/right | See corridor depth in both directions |
| Vertical up | ~+60 degrees | Look up at corridor ceiling detail, overhead light |
| Vertical down | ~-10 degrees below horizon | Prevents looking at absent body/feet |

Camera has slight idle drift/sway for life. Mouse controls look direction only (no WASD movement, no orbit). The viewer is stationary at the console.

### Shadow Proxy

An invisible humanoid silhouette mesh (~50 tris) parented to the camera rig. Capsule torso, smaller capsule head, two cylinder legs. Set with `castShadow = true` but `colorWrite = false` and `depthWrite = false` so it renders into shadow maps but not the color buffer. The viewer's shadow falls on the floor and walls from the monitor glow and overhead light, providing subconscious presence cues without rendering a body.

---

## Aesthetic Direction: "Bleak"

The defining reference is the Alien universe, specifically Alien: Isolation. Not harsh or brutal. Indifferent. Spaces designed by someone who calculated minimum acceptable lumens, then half the fixtures failed and nobody filed the repair order.

### Lighting

**Key light (overhead fluorescent):** Insufficient. A single tube light illuminating a patch of ceiling and upper third of walls. Slightly too yellow/warm. Optional intermittent flicker. Falls off fast; everything below waist height is lit by bounce and monitor emission.

**Monitor emission:** The brightest element in the scene by default (because everything else is so dim). Green or amber glow washes across surrounding wall panels via a point light or rect area light at the screen surface, colored to match current display content. When screen content transitions, this ambient light color shifts with it.

**Corridor ends:** Not uniform black. Enough ambient to barely make out wall geometry continuing into darkness. One or two distant indicator lights (steady amber, slow-blinking red) implying infrastructure running beyond the visible area. These also anchor parallax when the camera rotates.

**Double shadows:** Two shadow-casting light sources (monitor + overhead) producing the slightly uncanny overlapping shadow look of real institutional spaces with mixed lighting.

### Materials

**Wall panels:** High roughness overall. Subtle albedo variation (discoloration, water staining). Darkened seam lines suggesting accumulated grime. Applied as a detail texture layer over the base model textures. Not uniformly rough (reads as concrete), not smooth (reads as new/maintained).

**Moisture/damp effect:** Roughness map with vertical streak patterns at ~20% contrast where condensation has run down surfaces. When monitor light catches these at glancing angles, it reads as damp metal. Zero geometry cost.

**Floor:** Basic plane with a PBR material. Moderate metalness and roughness with a grime/wear roughness map. Small patches of near-zero roughness acting as imperfect puddle reflections that catch distorted monitor glow. Standing water, not mirror.

**Emissive accents:** Very dim emissive strips along corridor panel seam lines or edges (blue, amber, or red). Tiny glowing dots on walls suggesting background systems. Status indicators, not decoration.

### Atmosphere

**Depth fog:** Subtle, mostly visible where it catches monitor light or the overhead. Slight density variation (not uniform). Motivated by "the lighting doesn't reach" rather than artificial fadeout.

**Floating particulates:** Dozens of tiny sprites drifting slowly through the light cone from the monitor. Not dust motes in sunlight (too warm/pleasant); moisture droplets or fiber particulates in poorly filtered recycled air. Slow drift, slight random motion. Soft additive blend.

**No animated water/caustics needed.** The damp look comes entirely from the roughness map treatment.

### Audio

Ambient sound design via Web Audio API. Layered approach at low volume:

| Layer | Content | Behavior |
|-------|---------|----------|
| Base | Electrical hum, low drone | Continuous loop |
| Mid | Air circulation, ventilation | Continuous loop |
| Incidental | Distant metallic clanks, pressure releases | Randomized intervals |
| CRT | Faint high-frequency whine | Continuous, tied to monitor |

Source: freesound.org CC0 spaceship/industrial ambience loops.

---

## Technical Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| Renderer | Three.js with WebGPURenderer | Falls back to WebGLRenderer transparently |
| Model format | glTF/GLB | Three.js preferred format, Sketchfab standard export |
| Screen content | CanvasTexture with CRT shader | Render text/graphics to canvas, apply as emissiveMap |
| Audio | Web Audio API | Lightweight, built-in, handles layered ambient loops |
| Build tool | TBD (Vite likely) | Fast dev server, good Three.js ecosystem support |
| Mobile detection | UA string or viewport width check | Redirect to static fallback site |

### Poly Budget

| Element | Triangles |
|---------|-----------|
| Corridor sections (3x) | ~5,700 |
| Control Room Monitor | ~1,700 |
| Pin pad (procedural) | ~200-500 |
| Shadow proxy | ~50 |
| Floor plane | 2 |
| Overhead light fixture | ~50-100 |
| **Total** | **~7,700-8,050** |

### Screen Content Pipeline

1. Render section content (text, data, graphics) to an offscreen HTML Canvas
2. Apply CRT post-processing to the canvas (scan lines, bloom, curvature, vignette)
3. Use canvas as a `CanvasTexture` on the monitor's screen mesh material (emissiveMap)
4. Set `texture.needsUpdate = true` each frame (or on content change)
5. Sync the rect area light color to the dominant screen color for glow bleed

### Key Three.js Techniques

- `GLTFLoader` for model import
- Scene graph traversal to find named meshes (screen surface, buttons)
- `CanvasTexture` for dynamic screen and pin pad readout
- `RectAreaLight` or `PointLight` for monitor glow bleed
- Raycasting for mouse hover/click detection on monitor content
- Fog (linear or exponential) for corridor fade
- Sprite-based particle system for atmospheric particulates
- Shadow maps with proxy mesh for viewer shadow
- `OrbitControls` or custom camera controls with clamped rotation ranges

---

## Asset Manifest

| Asset | Source | License | Cost | Status |
|-------|--------|---------|------|--------|
| Sci-fi wall (corridor) | Sketchfab / Suushimi | Free, contact requested | $0 | Needs download |
| Control Room Monitor | Sketchfab / Dreadler | CC Attribution | $0 | Needs download |
| PBR metal/industrial textures | ambientCG or Polyhaven | CC0 | $0 | Needs selection |
| Ambient audio loops | freesound.org | CC0 | $0 | Needs selection |
| Monospace CRT font | Google Fonts or similar | Open license | $0 | Needs selection |
| Pin pad model | Procedural (Three.js) | N/A | N/A | To be built |
| Shadow proxy | Procedural (Three.js) | N/A | N/A | To be built |

**Attribution requirements:** Dreadler (CC-BY) must be credited. Suushimi requested to be shown the usage. Both should appear in site credits/footer or a credits section on the CRT itself.

---

## Scope

**In scope:**
- Single corridor scene as full-page 3D experience
- Monitor with CRT shader displaying portfolio content sections
- Pin pad with reactive animation (button depression, digit readout)
- Materials-driven atmosphere (damp industrial metal, insufficient lighting, particulates)
- Ambient audio layer
- Shadow proxy for viewer presence
- Mobile redirect to static fallback
- WebGPU with WebGL fallback

**Out of scope (for now):**
- Multiple rooms or explorable areas
- Animated doors or transitions between spaces
- Character model or hands
- VR/AR support
- Mobile-native 3D experience
- Backend/CMS for content (content is static in code initially)
- Analytics integration

**Future considerations:**
- Additional corridor sections as the site grows (walk to a new terminal)
- Interactive elements beyond monitor and pin pad (wall panels that open, etc.)
- Dynamic content loading from a CMS
- Easter eggs (hidden codes on the pin pad, flickering lights revealing messages)

---

## Open Questions

1. **Exact content sections:** Projects, About, Contact confirmed? Others? Resume/CV as a terminal readout?
2. **Monitor content detail level:** How much actual text/data on screen vs. aesthetic filler (scrolling logs, status bars)?
3. **Color palette:** Green phosphor CRT (classic Alien) vs. amber (warmer, more Isolation-era)? Could vary per section.
4. **Static fallback site:** Separate build, or same codebase with a 2D rendering path?
5. **Domain/hosting:** donfather.dev confirmed. Hosting platform? (Vercel, Cloudflare Pages, self-hosted on cluster?)
6. **Build tooling:** Vite assumed. Any preference?
7. **Font selection:** Need a monospace font that reads well at CRT resolution and has the right period feel. IBM Plex Mono, Space Mono, or something more retro?

---

## Next Steps

1. Download and test-load both Sketchfab models (wall + monitor) in a bare Three.js scene
2. Verify mesh names in the glTF scene graph (identify screen surface mesh for texture swap)
3. Prototype the CRT shader on a canvas texture
4. Build the corridor layout (three wall sections + floor plane + camera rig)
5. Implement basic lighting (overhead + monitor emission)
6. Add camera controls with rotation clamping

---

## Document Info

| | |
|---|---|
| Author | Claude (Anthropic) |
| Collaborator | User |
| Created | 2026-05-18 |
| Updated | 2026-05-18 |
| Version | 1.0 |
| Status | Concept validated |

---

## Sources

- Conversation in Claude.ai donfather.dev WebGPU portfolio project, 2026-05-18
- Sketchfab model pages (URLs inline above)
- Alien (1979) and Alien: Isolation (2014) as primary aesthetic references
- WebGPU showcase examples: webgpu.com (weisdevice, shader-se, joseph-santamaria portfolios)
