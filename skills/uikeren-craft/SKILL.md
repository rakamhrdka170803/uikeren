---
name: uikeren-craft
description: >-
  Visual craft and anti-generic-template filter for UI Keren. Spots common
  AI-generated patterns (autopilot cream+terracotta defaults, eyebrow dot pills,
  2x3 identical cards, background grids, flat SVG doodles, overlapping wide
  bottom docks) and replaces them with rich visuals—without banning any color.
---

# UI Keren — Visual Craft & Pattern Filter

Use with `uikeren/SKILL.md`. **Never ban any color**—if the user asks for
cream, orange, purple, or anything else, honor it. What we reject is **lazy AI
autopilot defaults** and **layout collisions**.

## Visual, Color & Asset Patterns

### 1. Autopilot "AI Culinary/SaaS" Color Habits (Deprioritize, Don't Ban)
- **AI Pattern:** Reaching on autopilot for `warm cream (#FAF5EC) + dark brown
  + terracotta/crimson (#D83A22)` on every food/cafe site, or `dark slate +
  purple/blue glow` on every tech site, even when the user didn't ask for it.
- **Issue:** Makes completely different projects look like the same AI model
  template.
- **Replacement:** Unless the user requests those colors, deliberately pick a
  fresher palette first (e.g., deep tea-jade + porcelain + chili, midnight navy
  + electric coral + off-white, cobalt + bone + brass, charcoal + sage + cream,
  obsidian + cyan/pink).

### 2. Flat SVG Doodles Instead of Real Media (`imgs: 0`)
- **AI Pattern:** Inline `<svg>` sketches (beans, cups, contour graphs, boxes)
  inside dark rounded boxes taking the place of photography or artwork.
- **Issue:** Immediately signals zero real visual assets.
- **Replacement:** Generate 2–4 tailored images via `image-generator` and
  display them edge-to-edge (`object-cover`), or build rich full-frame `<canvas>`
  scenes.

### 3. Status-Dot Pill & Eyebrow Above the Headline
- **AI Pattern:** A rounded pill (`• Batch #48 · Fresh`) or uppercase eyebrow
  parked directly above a centered H1.
- **Issue:** Textbook AI template ornament.
- **Replacement:** Drop the decorative dot pill. Fold context cleanly into
  top/edge metadata or directly into the copy.

### 4. Repetitive `01 · MONO` + `Instrument Serif` + *Italic Accent* Headings
- **AI Pattern:** Repeating `01 · SUBTITLE` above serif headings with the last
  word italicized on every single band.
- **Issue:** Turns an editorial look into an obvious mechanical pattern.
- **Replacement:** Vary heading treatments and select font pairings matched to
  the domain (`Syne`, `Bricolage Grotesque`, `Archivo Black`, `Fraunces`,
  `Poppins`, `Space Grotesk`, `DM Sans`).

## Layout, Reference Balance & Collision Patterns

### 5. Over-Leaning on `pos.efisien.id` Closing Trail & Hero
- **AI Pattern:** Always building a centered dark-photo hero + 2 bottom-corner
  floating cards + a bright red/orange full-width closing band with floating
  photo stamps (`ClosingTrail`).
- **Issue:** Makes every site look like a clone of `pos.efisien.id` instead of
  blending `marsrejects.com` and `discodungeongame.com`.
- **Replacement:** Alternate hero and closing patterns across builds: use
  `marsrejects.com`'s **3D Text-Behind-Subject hero** and **full-bleed artwork
  + clean dark horizon footer**, or `discodungeongame.com`'s **Scroll-Spine
  stage** + **subscribe/action horizon footer**. If using `ClosingTrail`, keep
  trail stamps strictly outside the centered text/CTA safe zone so they never
  overlap paragraph copy.

### 6. Wide Fixed Bottom Dock Eating Middle Content
- **AI Pattern:** A `400px`-wide `position: fixed; bottom: 20px` dark capsule
  bar sitting over tabs, calculators, menu rows, and footer links as you scroll.
- **Issue:** Actively blocks interactive buttons and text in middle bands.
- **Replacement:** Use a clean top navbar **OR** a compact circular floating
  menu trigger (`<= 56px`, `marsrejects`-style) that expands only on click—never
  a wide floating pill bar blocking middle-section controls.

### 7. Copy-Paste 2x3 Cards & Repeated Dark Split Boxes
- **AI Pattern:** Six identical bordered cards or repeated `[Left Text | Right
  Dark Card]` sections.
- **Issue:** Monotonous middle sections.
- **Replacement:** Mix a staggered **3D Radial Burst Cluster** (`initRadialBurst`),
  a **Horizontal Screens Carousel** (`initScreensCarousel`), **Tilted Story
  Stickers**, and **Hairline Rows** (`border-bottom: 1px`).
