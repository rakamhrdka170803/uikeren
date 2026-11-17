---
name: uikeren
description: >-
  Core anti-slop web builder skill. Activate whenever the user asks—in any
  language—to build, design, or redesign a website, landing page, or interactive
  web UI. Enforces Liveliness Dials, Purpose-Gate checks, real image generation,
  Playwright-recorded JS motion from marsrejects.com, discodungeongame.com, and
  pos.efisien.id, plus a mandatory PASS/FAIL Delivery Gate.
---

# UI Keren — Core Anti-Slop Engine

> Filter + Direction combined. Removing AI slop leaves a sterile void unless
> you inject real visual craft and Playwright-recorded interaction physics.

Load `uikeren-ui`, `uikeren-motion`, and `uikeren-layoutmobile` together with
this core skill on every web build.

## Step 1: Declare Design Read & Liveliness Dials (Before Coding)
Write one concise Design Read line in the user's language before writing code:
> `Reading this as: <page kind> for <audience>, blending <reference ingredients>, dial ENERGY <1-3> / RHYTHM <1-3> / MOTION <1-3>.`

| Dial | 1 (Calm) | 2 (Balanced) | 3 (Bold — Default Target) |
| :--- | :--- | :--- | :--- |
| **ENERGY** | Clean editorial | Editorial + tactile accents | Monumental typography, 3D Z-depth, rich imagery |
| **RHYTHM** | Predictable | Occasional layout break | Asymmetric, every section changes composition |
| **MOTION** | Hover only | Scroll-reveal + tabs | Scroll-morph / 3D parallax / carousel / cursor trail |

Default target for `uikeren` websites is **ENERGY 3 / RHYTHM 3 / MOTION 3**
(unless the user asks for a minimal/calm utility).

## Step 2: Written Purpose-Gate (`R-01` to `R-08`)
Before finalizing your architecture, write a **1-line reason** for each choice
(no "because AI usually puts it here"):
- **R-01 Colors**: Any palette is allowed (including user-requested colors); cap
  active core colors at 2–3 + 1 accent with clear contrast.
- **R-02 Typography**: Why this display + body font? **FORBIDDEN**: repeating
  `01 · MONO EYEBROW` + `Instrument Serif` + *italic last word* on every H2.
- **R-03 Visual Assets (NO `imgs: 0`!)**: If `image-generator` is available,
  **invoke it first** to generate 2–4 bespoke domain images (hero scene,
  product/editorial photos). **FORBIDDEN**: replacing real photography/art with
  flat inline `<svg>` doodles (beans, cups, contour graphs, tiny boxes).
- **R-04 Section Rhythm (No Repeated Middle Boxes)**: When `RHYTHM = 3`,
  Sections 2, 3, and 4 MUST use **visibly different compositions**—never stack
  repeated `[Left Text | Right Dark Rounded Box]` or 2x3 identical card grids.
- **R-05 Original Blend (Never Clone 1:1)**: Borrow mechanics from all 3
  references (`marsrejects.com`, `discodungeongame.com`, `pos.efisien.id`),
  never copying any single site's layout verbatim.
- **R-06 Single Non-Overlapping Navigation**: Use **either** a top navbar **or**
  a compact bottom pill (`padding-bottom: 112px` on `footer`)—never stack both
  and never let a fixed dock cover list rows, buttons, or footer text.
- **R-07 Real Interactive State**: Every button, tab, carousel, builder, or
  drawer must work end-to-end (zero dead `href="#"` controls).
- **R-08 Natural Human Copy**: Zero em-dash (`—`) overuse, zero AI buzzwords
  (*"Revolutionize"*, *"Seamless"*, *"Elevate"*), zero fake `10K+ Users` stats.

## Step 3: Mandatory Delivery Gate (Run BEFORE Delivering)
Verify every item below; if ANY item fails, fix it first before answering:
- [ ] **Real Visuals Check**: At least 2–4 real images (`<img>` with
      `object-cover`) or rich full-bleed `<canvas>` scenes—NOT `imgs: 0` with
      only flat SVG diagrams.
- [ ] **AI Tell Scan (`uikeren-ui`)**: No pill eyebrow with pulsing dot above H1,
      no 2x3 copy-paste feature cards, no decorative background grid lines, no
      pill-shaped everything.
- [ ] **Section Variety Check**: Section 1, 2, 3, and 4 each have distinct
      structure (e.g., 3D Z-depth hero -> horizontal Screens Carousel -> 3D
      Radial Cluster / interactive builder -> closing trail).
- [ ] **Motion Check (`uikeren-motion`)**: At least 3 recorded JS interactions
      active & tested, with `prefers-reduced-motion: reduce` support.
- [ ] **Mobile & Overlap Check (`uikeren-layoutmobile`)**: Tested at desktop
      (`1440px`) and mobile (`375px`), zero horizontal overflow, zero fixed dock
      or trail stamp covering text/buttons, zero console errors.
