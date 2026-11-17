---
name: uikeren-ui
description: >-
  Visual anti-slop diagnostic skill for UI Keren. Lists exact AI-slop tells
  (pill eyebrow dots, 2x3 copy-paste cards, background grids, fake SVG charts,
  repeated dark rounded boxes) and their concrete fixes without restricting any
  color palette.
---

# UI Keren — Visual & Anti-Slop Tells

Use alongside `uikeren/SKILL.md`. **Never ban colors**—any palette requested
by the user or suited to the brand is welcome. What this skill kills is
**structural and visual AI tells**.

## Visual & Asset Tells

### Flat SVG Doodles Replacing Real Photography (`imgs: 0` Slop)
- **Tell:** Inline `<svg>` drawings of coffee beans, cups, contour lines,
  clocks, or boxes sitting inside dark rounded rectangles across every section.
- **Why:** Instantly reads as "AI had no real images so it drew vector charts".
- **Fix:** Invoke `image-generator` (2–4 cohesive images) and render full-bleed
  `object-cover` visuals, or build rich procedural HTML5 `<canvas>` scenes.

### Eyebrow Pill + Decorative Status Dot Above H1
- **Tell:** A small pill (`• Batch #48 · Fresh Today`) with a glowing/pulsing dot
  parked directly above the main `H1` or floating in the hero corner.
- **Why:** Textbook AI template ornament borrowing "live status" UI for static
  marketing text.
- **Fix:** Cut decorative status dots. Put location/context cleanly in the
  minimal top/edge metadata or weave it directly into the headline copy.

### Background Grid / Graph Paper Lines
- **Tell:** Repeating faint grid squares (`background-image: linear-gradient(...)`)
  behind charts, cards, or hero sections without a true CAD/technical reason.
- **Why:** Cheap AI shortcut to make flat boxes feel "engineered".
- **Fix:** Use clean solid contrast surfaces, subtle film grain, or real
  photography/layered artwork instead.

### `01 · MONO EYEBROW` + `Instrument Serif` + *Italic Last Word* Rut
- **Tell:** Every section header repeating `01 · SUBTITLE` in uppercase monospace
  above `Instrument Serif` with the last 1–2 words italicized in accent color.
- **Why:** Even though serif+mono looks "editorial" once, repeating the exact
  formula on every H2 screams AI template.
- **Fix:** Vary type voice deliberately across domains (`Syne`, `Bricolage
  Grotesque`, `Archivo Black`, `Fraunces`, `Poppins`, `Space Grotesk`, `DM Sans`).

### Excessive Pill Shapes (`border-radius: 9999px` Everything)
- **Tell:** Buttons, filter tabs, tags, inputs, cards, and docks all rounded to
  identical pills.
- **Why:** Erases visual hierarchy between a primary CTA, a tab, and a tag.
- **Fix:** Establish 2–3 intentional radii in your system (e.g., `0px–4px`
  editorial hairline, `16px–20px` media frames, pill reserved strictly for one
  primary CTA or dock).

## Layout & Rhythm Tells

### Copy-Paste 2x3 or 3-Column Feature Cards
- **Tell:** Six identical bordered boxes (`AIR · 75 PPM`, `BURR · 64 MM`, ...)
  all sharing the same mono eyebrow, bold title, and 2-line description.
- **Why:** Flattens hierarchy and screams template filler.
- **Fix:** Replace with `discodungeon`-style **3D Radial Burst Cluster**
  (`initRadialBurst`), `marsrejects`-style **Hairline Rows** (`border-bottom: 1px`),
  or a **Horizontal Screens Carousel** (`initScreensCarousel`).

### Back-to-Back `[Left Controls | Right Dark Rounded Card]`
- **Tell:** Section 2, Section 3, and Section 4 all structured as a 2-column
  split with a dark rounded box on one side.
- **Why:** Middle sections blur together and feel AI-assembled.
- **Fix:** Force `RHYTHM 3`: alternate full-bleed media bands, horizontal
  carousels, asymmetric overlapped stickers, and one signature interactive tool.

### Overlapping Fixed Docks & Trail Stamps
- **Tell:** A fixed floating bottom dock sitting on top of menu rows or footer
  links, or `ClosingTrail` stickers rendering over CTA button text.
- **Why:** Broken layout collision.
- **Fix:** Pick **one** navigation anchor (top bar OR bottom pill with
  `padding-bottom: 112px` on `footer`), and keep CTA text/buttons at `z-index: 5`
  above trail stamps (`z-index: 1`).
