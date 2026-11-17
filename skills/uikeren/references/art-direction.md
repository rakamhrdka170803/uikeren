# Recorded Design & Layout DNA (3 Reference Sites)

Recorded via headless Chrome/Playwright inspection of `pos.efisien.id`,
`marsrejects.com`, and `discodungeongame.com`. **Blend and re-interpret their
craft equally and originally**—never default to `pos.efisien.id` alone and
never repeat `[Left List | Right Dark Rounded Card]` across middle sections.

---

## Core Visual Rule: Real Bespoke Imagery Over Flat SVG Placeholders
Every one of the 3 reference sites feels real because it uses **dense real
imagery/artwork** (`65` photos + `9` videos on `pos.efisien.id`, `106` artworks
on `marsrejects.com`, `92` images + `3` videos on `discodungeongame.com`)—NOT
inline `<svg>` doodles inside dark rounded boxes.
- **When `image-generator` is available**: Invoke it early to generate 2–4
  cohesive, art-directed images (1 hero visual + 2–3 product/editorial shots)
  matched to your palette and subject.
- **When no image tool exists**: Use rich multi-layered HTML5 `<canvas>` scenes
  or crisp photographic/editorial UI mockups—never flat SVG drawings of
  cups/boxes/contours.

---

## Balanced Ingredients From All 3 Sites (Mix Across Sections!)

1. **From `marsrejects.com` (`1440x900` 3D Layered Depth)**:
   - **3-Layer Z-Depth Hero**: Rear character/product row -> Monumental wide
     display headline (`clamp(3.5rem, 9vw, 6.5rem)`) **behind** foreground art ->
     Foreground visual layer with subtle pointer parallax.
   - **Tilted Sticker Captions + Hairline Rows**: Rotated stamp badges over
     full-bleed artwork panels + ultra-clean `1px` horizontal dividers.
   - **Expandable Compact Bottom Pill**: Only if there is NO top navbar, with
     generous `padding-bottom: 104px` on `footer` so it never covers text.

2. **From `discodungeongame.com` (`1440px` Kinetic Stage)**:
   - **Horizontal Screens Carousel (`initScreensCarousel`)**: Interactive
     Prev/Next + dot pagination showcase with tall `object-cover` showcase
     cards gliding horizontally.
   - **3D Radial Burst Feature Cluster (`initRadialBurst`)**: Features/icons
     that burst outward in 3D from center when scrolled into view—replacing
     boring 2-column text tables in middle sections!
   - **Scroll-Spine Journey (`initScrollSpine`)** + `backOut` overshoot
     (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`).

3. **From `pos.efisien.id` (`1440px` Editorial Rhythm)**:
   - **Full-Bleed Hero & Alternating Contrast Bands**: Crisp light bands
     (`#FFFFFF` / `#F7F6F5`) alternating with dark sections, `650ms`
     `clip-path` reveals (`ScrollMotion`), and pooled `ClosingTrailSection`
     kept behind/clear of CTA buttons.

---

## Typography Guidance (Avoid the Single-Font AI Rut)
Do **not** default every project to `Instrument Serif` + italic last word +
`01 · MONO EYEBROW`. Pick a fresh pairing per domain:
- **Bold Modern Editorial**: `Bricolage Grotesque` or `Syne` display + `Plus Jakarta Sans` body
- **High-Impact Wide / Arcade / Street**: `Archivo Black` or `Space Grotesk` display + `Inter Tight` body
- **Warm Craft Serif (without italic-last-word cliché)**: `Fraunces` or `Playfair Display` + `DM Sans` body
- Use **any color palette** requested by the user or suited to the domain.
