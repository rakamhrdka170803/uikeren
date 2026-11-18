---
name: uikeren-craft
description: >-
  Visual craft and anti-generic-template filter for UI Keren. Eliminates the
  boring SaaS top bar, 50/50 split hero with 1 photo card, 4-card identical
  grids, vertical-line 01..04 timeline boxes, SaaS rounded-box wrappers, and
  wordy AI prose.
---

# UI Keren — Visual Craft & Pattern Filter

Use with `uikeren/SKILL.md`. Never ban colors—deprioritize autopilot defaults
and eliminate the exact layout patterns that make generated sites look like AI.

## Banned Generic AI Patterns (Must Replace)

### 1. Boring SaaS Top Navbar (`[Logo | 4 Links | Pill CTA]`)
- **AI Pattern:** Solid dark/light bar with `[Square Icon + BRAND]` left, `4`
  evenly spaced anchor links centered, and `1` bright rounded pill CTA right.
- **Replacement:** Use a **borderless transparent overlay nav** on full-bleed
  hero media (`discodungeongame.com` / `pos.efisien.id`), **OR** a minimal
  **corner masthead + compact `Menu` trigger** (`marsrejects.com`) with no
  horizontal link strip at all.

### 2. 50/50 Split Hero With 1 Tilted Photo Card on the Right
- **AI Pattern:** Left = `[UPPERCASE EYEBROW] + [4-line H1] + [2-line desc] +
  [2 pill buttons]`; Right = `[1 rounded photo card with tilted price badges]`.
- **Replacement:** Make hero visuals **full-bleed (`100vw`)**—either
  `marsrejects`-style **3D text-behind-subject** layered across the full width,
  `discodungeon`-style centered stage, or `pos.efisien.id` edge-to-edge hero
  photography. Keep `<h1>` to **1–2 crisp lines** (never stretched ultra-wide
  fonts breaking into 4 awkward lines).

### 3. Vertical Line + Dot + 4 Stacked Horizontal Rounded Cards (`01..04`)
- **AI Pattern:** A thin vertical grey line + orange dot on the left next to
  4 wide white `rounded-xl` boxes (`01`, `02`, `03`, `04`) stacked down a cream
  page.
- **Replacement:** Turn process/storytelling into **open hairline rows**
  (`border-bottom: 1px`, zero outer card background/border) synced to a live
  changing full-bleed photo, OR horizontal editorial panels with tilted
  stickers.

### 4. Identical 4-Column Photo+Title+Text Card Rows & Rounded Box Wrappers
- **AI Pattern:** Four identical bordered/filled cards in a row (`[photo] +
  [title] + [2-line text] + [+ Tambah]`), plus wrapping FAQ/orders/forms in
  rounded `1px` SaaS border cards.
- **Replacement:** Use borderless `object-cover` photo tiles (`marsrejects` /
  `pos.efisien.id`), open hairline tables (`border-bottom: 1px`) for menus and
  FAQs, or a staggered **3D Radial Burst Cluster** (`initRadialBurst`).

### 5. Flat Vector Art, Pastel Pill Tags, & Wordy Copy
- **AI Pattern:** Cartoon vector hero art, pastel pill badges inside cards,
  or `15–30` word descriptions inside menu items.
- **Replacement:** Real editorial photography via `image-generator`, max **`6–10
  words`** per card/row description, and full SEO metadata placed cleanly in
  `<head>` + JSON-LD.

### 6. Autopilot Warm Cream / Amber-Terracotta Defaults
- **AI Pattern:** Defaulting to `#FAF5EC` cream + `#12110F` black + `#FF5A36`
  / `#F59E0B` yellow-amber unless asked.
- **Replacement:** Honor any color requested by the user; otherwise pick fresher
  editorial palettes (celadon/porcelain, midnight navy/coral, cobalt/bone,
  forest/butter, obsidian/magenta-cyan) first.
