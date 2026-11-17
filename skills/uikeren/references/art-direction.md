# Art Direction & Reference Architecture

Model the **actual layout drama, contrast, and visual density** of the three
reference sites—never generic boxed templates:

## 1. Choose One of Three High-Craft Structural Archetypes
Adapt the archetype to the user's domain (never copy another brand's content):

### Archetype A — Full-Bleed Scroll-Morph Editorial (`pos.efisien.id` DNA)
- **Above the fold**: Full-bleed atmospheric hero (`100vh`) filled edge-to-edge
  with rich photography, video, or interactive canvas—NO cramped 50/50 boxes.
  Floating minimalist top bar, monumental centered/editorial serif+sans
  display headline, clean pill CTA.
- **Scroll transition**: As the user scrolls, the full-bleed hero shrinks and
  docks cleanly (`HeroMosaicMorph`) into a sparse, airy **checkerboard mosaic**
  of square (`rounded-[20px]`) full-bleed visual tiles & bold typographic
  blocks, while a secondary display headline rises word-by-word.
- **Contrast**: Alternate crisp studio light surfaces (`#FFFFFF` / `#F7F6F5`)
  with deep dark full-bleed spotlight/video bands and tactile tabbed product
  explorers.

### Archetype B — High-Contrast Midnight Editorial (`marsrejects.com` DNA)
- **Palette**: Deep midnight obsidian (`#021120`), bold crimson/electric accent
  (`#F74A53`), crisp off-white paper (`#F5F0F0`), muted slate (`#435365`).
- **Composition**: Full-bleed character/product art panels, dramatic scale
  jumps between oversized display headings and tight technical metadata,
  snappy `50ms–300ms` transitions and tactile `scale(0.9)` press responses.

### Archetype C — Layered Kinetic Showcase (`discodungeongame.com` DNA)
- **Atmosphere**: Rich saturated depth, parallax foreground/midground layers,
  overshoot `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) micro-physics,
  pop-in badges (`scale: 0 -> 1`), and an actually playable/interactive centerpiece
  that fills its stage richly.

## 2. Visual Density & Typography Rules
- **Generate or build real visuals**: If `image-generator` is available in the
  session, generate 2–4 bespoke editorial/product images for the hero and
  mosaic/showcase tiles instead of drawing tiny inline SVG icons! If working
  offline/pure code without image generation, build **full-bleed HTML5 Canvas
  scenes or detailed interactive UI views**—never tiny SVGs floating in white
  cards.
- **Typography Pairing**: Combine a characterful display face (`Fraunces`,
  `Syne`, `Instrument Serif`, `Bricolage Grotesque`, `Space Grotesk`) with a
  clean sans (`Plus Jakarta Sans`, `Inter Tight`, `DM Sans`) and monospace
  (`JetBrains Mono`, `Space Mono`) for prices/specs. Tight display tracking
  (`-0.03em` to `-0.05em`).
- **Strict Restraint**: 1 dominant surface + 1 ink + 1 sharp accent. Let
  generous whitespace and full-bleed media create authority—do not wrap every
  section in thick black borders.
