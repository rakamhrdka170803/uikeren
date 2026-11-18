---
name: uikeren-craft
description: >-
  Visual craft, concise copy, SEO hygiene, and anti-AI-template filter for UI
  Keren. Eliminates text-only pastel-pill card grids, wordy AI descriptions,
  cartoonish vector hero illustrations, autopilot palettes, and overlapping
  floating buttons.
---

# UI Keren — Visual Craft, Copy & Pattern Filter

Use with `uikeren/SKILL.md`. Never ban colors—deprioritize AI autopilot
defaults and eliminate AI layout, copy, and asset clichés.

## Visual & Asset Patterns

### 1. Text-Only "Pastel Pill + 3-Line Essay + Stepper" Product Grids
- **AI Pattern:** A 2-column grid of white rounded cards where every card has
  `[PASTEL PILL BADGE]` + `[Title]` + `[15–25 word AI description]` +
  `[Price + (- 2 +) stepper]`, paired with a dark summary card—and **zero
  product images on the cards**.
- **Issue:** Looks 100% like an AI SaaS/ordering template (`Racik Kotak` slop).
- **Replacement:** Show **real food/product photography** (`aspect-[4/3]
  object-cover`) inside every featured card with **only title, price, and a
  4–8 word tasting/spec line** (drop the pastel pill tag), OR use a clean
  hairline list synced to a large live photo preview.

### 2. Flat Cartoon Vector Art Pretending to Be a Hero Photo
- **AI Pattern:** A flat, smooth vector/cartoon illustration (e.g., 3 smooth
  balls on a brown circle) floating on a solid gradient background.
- **Issue:** Immediately reads as synthetic AI clip-art rather than real craft.
- **Replacement:** When calling `image-generator`, explicitly request
  **editorial studio photography, natural textures, directional lighting, and
  shallow depth of field** (or detailed high-craft art direction matching the
  brand)—never generic vector clip-art.

### 3. Wordy AI Prose Everywhere (Hurts UX & Real SEO Clarity)
- **AI Pattern:** 20–35 word hero paragraphs, 15-word menu descriptions, and
  long multi-sentence cards explaining obvious things (*"Cincangan kasar yang
  memberi tekstur kenyal alami, bukan adonan halus yang terasa seperti..."*).
- **Issue:** Bloats mobile height to `9,000px+` and screams AI copywriting.
- **Replacement:** Keep visible UI copy razor-sharp (**`6–12 words`** per card
  line, **`10–18 words`** max for hero subcopy). Put comprehensive business,
  location, menu, and product details cleanly in **JSON-LD schema + `<meta>`
  tags** for SEO.

### 4. Autopilot Color Habits (Deprioritize, Don't Ban)
- **AI Pattern:** Defaulting automatically to `warm cream + dark brown +
  terracotta` on food sites or `dark slate + purple glow` on tech sites when
  the user didn't ask for those colors.
- **Replacement:** Honor any color the user requests; otherwise pick fresher
  domain-authentic palettes first.

### 5. Status-Dot Pills, Background Grids, & `01 · MONO + Serif *Italic*` Rut
- **AI Pattern:** Pulsing status dots above `<h1>`, graph-paper background
  grids, or repeating `01 · SUBTITLE` + `Instrument Serif` + *italic last word*.
- **Replacement:** Clean editorial hierarchy without decorative dots or grids,
  and varied typography pairings (`Syne`, `Bricolage Grotesque`, `Archivo
  Black`, `Fraunces`, `Poppins`, `Space Grotesk`, `DM Sans`).

### 6. Floating Bottom Buttons/Docks Covering Mobile Content
- **AI Pattern:** A fixed `(≡)` circle or wide bottom capsule floating over
  WhatsApp buttons, menu rows, and footer text.
- **Replacement:** Keep navigation cleanly inside a single-row top `<header>`
  (with a slide-down/drawer menu on mobile) so **nothing floats over page
  content**.
