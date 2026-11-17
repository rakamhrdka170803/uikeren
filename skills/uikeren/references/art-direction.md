# Recorded Design & Layout DNA (3 Reference Sites)

Recorded via headless Chrome/Playwright inspection of `pos.efisien.id`,
`marsrejects.com`, and `discodungeongame.com`. **Blend the best ingredients from
all three** and adapt the theme, copy, and colors (including any user-requested
colors) authentically to the prompt's domain.

---

## Reference 1: `pos.efisien.id` — Full-Bleed Photo/Video + Editorial Rhythm
Observed layout & metrics (`1440px` desktop):
- **Hero (`1440x1440` scroll runway)**: Full-bleed atmospheric photograph/video
  filling 100% of the viewport, transparent top nav (`64px`), centered `74px`
  serif display headline (`Exact Block` style, `line-height: 1.02`,
  `letter-spacing: -0.02em`), crisp pill CTA buttons, and a subtle bottom
  category strip. On scroll, the hero shrinks into a staggered **checkerboard
  photo mosaic** (`HeroMosaicMorph`).
- **Band Rhythm**: Alternates crisp clean light bands (`#FFFFFF` / `#F7F6F5`)
  with deep dark bands (`#000000`). Uses large full-bleed `object-cover` photo
  cards with clean overlay typography (no thick cartoon borders) and an
  interactive tabbed explorer.
- **Closing Band**: Dark full-width CTA section (`~520px` tall) with a pooled
  cursor-following + idle ambient trail (`ClosingTrailSection`).

## Reference 2: `marsrejects.com` — Layered Depth, Text-Behind-Subject & Hairline Rows
Observed layout & metrics (`1440px` desktop):
- **Hero (`1440x900`)**: Monumental wide display typography (`88px`, `line-height: 0.8`)
  **layered BEHIND** foreground illustrated subjects (`z-index` depth), flanked
  by subtle vertical micro-telemetry marks on the outer screen edges.
- **Floating Bottom Dock**: Compact centered pill/circle action dock pinned
  near the bottom (`position: fixed; bottom: 20px`) instead of bulky top/footer
  clutter.
- **Story Cards + Tilted Stickers**: Full-bleed vertical artwork panels with
  slightly rotated editorial/comic caption stickers (`transform: rotate(-2deg)`)
  overlapping the frame edges.
- **Hairline Editorial List**: Clean benefits/menu/specs rows separated by thin
  `1px` horizontal rules (`border-bottom: 1px solid`) with generous breathing
  room—zero boxy card borders.

## Reference 3: `discodungeongame.com` — Scroll-Spine Journey & Tactile Showcase
Observed layout & metrics (`1440px` desktop):
- **Atmospheric Stage (`765px` hero)**: Centered custom emblem/title over a
  deep atmospheric scene (`92` images + `3` videos across the page), clean
  minimalist top nav (`5` links + `1` accent CTA).
- **Vertical Scroll Spine**: A central glowing column/motif (`ScrollSpine`)
  runs continuously down the dark sections so scrolling feels like descending
  through a cohesive world.
- **Asymmetric Device/UI Showcase**: Clean `55px` headline + short paragraph on
  one side paired with a tall interactive device/frame mockup + dot carousel on
  the other, powered by Framer `backOut` overshoot physics.

---

## How to Blend Them for Any Prompt (e.g., Bakpao, Coffee Shop, SaaS, Game)
Pick **one hero style** + **2–3 section patterns** from above:
- **Example Blend A (Culinary / Bakpao / Coffee Shop)**:
  - Full-bleed `100vh` atmospheric hero (generated/real food photography or rich
    full-bleed interactive canvas) with `pos.efisien.id`-style `74px` serif
    headline + `marsrejects`-style **floating bottom action/cart dock**.
  - `HeroMosaicMorph` scroll transition into flavor/story photo tiles.
  - Interactive menu/box builder inside an editorial **hairline list** +
    clean `discodungeongame`-style live preview frame + `ClosingTrailSection`.
- **Example Blend B (Creative / Game / Collectible)**:
  - `marsrejects`-style **text-behind-subject hero** (`88px` wide display
    behind foreground artwork/canvas) + floating bottom dock.
  - `discodungeongame`-style **vertical scroll-spine** connecting dark
    atmospheric feature bands + interactive device/playable showcase.
- **Color Rule**: Use whatever palette fits the domain or whatever colors the
  user explicitly asks for—let typography scale, full-bleed visuals, layering,
  and whitespace carry the craft.
