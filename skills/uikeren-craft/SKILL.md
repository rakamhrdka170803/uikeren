---
name: uikeren-craft
description: >-
  Visual craft and anti-generic-template filter for UI Keren. Spots common
  AI-generated patterns (eyebrow dot pills, 2x3 identical cards, background
  grids, flat SVG doodles, repeated dark cards) and replaces them with rich
  visuals—without restricting any color palette.
---

# UI Keren — Visual Craft & Pattern Filter

Use with `uikeren/SKILL.md`. **Never restrict colors**—any palette requested
by the user or suited to the topic is welcome. Focus strictly on eliminating
lazy structural and visual clichés.

## Visual & Asset Patterns

### 1. Flat SVG Doodles Instead of Real Media (`imgs: 0`)
- **AI Pattern:** Inline `<svg>` sketches (beans, cups, contour graphs, boxes)
  inside dark rounded boxes taking the place of photography or artwork.
- **Issue:** Immediately signals that the page has zero real visual assets.
- **Replacement:** Generate 2–4 tailored images via `image-generator` and
  display them edge-to-edge (`object-cover`), or build rich full-frame HTML5
  `<canvas>` scenes.

### 2. Status-Dot Pill Parked Above the Headline
- **AI Pattern:** A rounded pill (`• Batch #48 · Fresh`) with a glowing or
  pulsing dot floating directly above the main `H1`.
- **Issue:** Overused AI template badge imitating a live indicator when nothing
  is actually live.
- **Replacement:** Drop the decorative dot pill. Fold essential context into
  subtle top/edge metadata or directly into the hero copy.

### 3. Decorative Graph-Paper / Background Grids
- **AI Pattern:** Repeating faint square grids (`linear-gradient`) behind
  sections or charts with no functional purpose.
- **Issue:** Cheap visual filler trying to make empty boxes look technical.
- **Replacement:** Use clean contrast planes, subtle grain, or real imagery.

### 4. Repetitive `01 · MONO` + `Instrument Serif` + *Italic Accent* Headings
- **AI Pattern:** Repeating `01 · SUBTITLE` above `Instrument Serif` with the
  last word italicized on every single section heading.
- **Issue:** Repeating one typographic gimmick across 4–5 sections turns an
  editorial style into an obvious template.
- **Replacement:** Vary heading treatments and select font pairings matched to
  the domain (`Syne`, `Bricolage Grotesque`, `Archivo Black`, `Fraunces`,
  `Poppins`, `Space Grotesk`, `DM Sans`).

### 5. Uniform Pill Radii Everywhere
- **AI Pattern:** Making every button, filter tab, tag, badge, and dock a
  `9999px` capsule.
- **Issue:** Destroys visual distinction between primary CTAs, tabs, and tags.
- **Replacement:** Use 2–3 deliberate radius steps (e.g., `0–4px` editorial
  lines, `16–20px` media frames, and capsule reserved for primary actions).

## Layout & Rhythm Patterns

### 6. Copy-Paste 2x3 / 3-Column Feature Cards
- **AI Pattern:** Six identical bordered cards (`AIR · 75 PPM`, `BURR · 64 MM`,
  etc.) all using the same mono tag + bold title + 2-line blurb.
- **Issue:** Flattens content hierarchy into template filler.
- **Replacement:** Use a staggered **3D Radial Burst Cluster** (`initRadialBurst`),
  a **Horizontal Screens Carousel** (`initScreensCarousel`), or clean
  **Hairline Editorial Rows** (`border-bottom: 1px`).

### 7. Stacked `[Left Text | Right Dark Rounded Card]` Bands
- **AI Pattern:** Sections 2, 3, and 4 all structured as a 2-column split with
  a dark rounded widget box on the right.
- **Issue:** Middle sections feel monotonous and mechanically generated.
- **Replacement:** Alternate full-bleed bands, horizontal carousels, tilted
  editorial stickers, and one dedicated interactive workspace.

### 8. Fixed Dock & Trail Overlap
- **AI Pattern:** A floating bottom dock covering rows or footer text, or
  cursor trail stickers spawning on top of CTA button labels.
- **Issue:** Broken interactive layering.
- **Replacement:** Keep one navigation system only (reserve `padding-bottom: 112px`
  on `footer` if using a bottom dock), and keep CTA text/buttons at `z-index: 5`
  above trail elements (`z-index: 1`).
