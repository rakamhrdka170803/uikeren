---
name: uikeren
description: >-
  Use this skill whenever the user asks—in any language—to build, design,
  create, or redesign a website, landing page, web UI, or interactive frontend
  (e.g. "buatkan web bapau", "bikinin landing page", "build a product website",
  "create an interactive site"). Enforces bespoke art direction, full-bleed
  visual richness, recorded high-craft JavaScript interactions, and strict
  anti-AI-slop guardrails adapted to the user's domain.
---

# UI Keren — Reference-Driven Anti-Slop Web Builder

Blend the **layout drama, visual richness, and JS interaction physics**
recorded equally from `pos.efisien.id`, `marsrejects.com`, and
`discodungeongame.com`—adapted originally to the user's topic and color
preferences. Never default to `pos.efisien.id` alone, and never clone any
reference section 1:1.

## Workflow

### 1. Generate Real Visuals First (MANDATORY When Tool Available)
Never fake photography or hero/card visuals with flat inline `<svg>` drawings
(no SVG coffee pots, SVG contour lines, or tiny icons inside dark rounded
boxes).
- If the `image-generator` subagent is available, **invoke it first** to
  generate **2–4 cohesive bespoke images** (e.g., 1 full-bleed hero scene,
  2–3 product/editorial shots) matching the domain and palette.

### 2. Plan a Balanced 3-Reference Blend (Before Coding)
Read [Art Direction Reference](./references/art-direction.md) and mix across
all 3 references:
- **Hero**: Pick either `marsrejects` **3D Perspective Depth Hero** (`initDepthHero`
  with rear/title/front layers), `discodungeon` **Atmospheric Stage**, or
  `pos.efisien.id` full-bleed hero.
- **Middle Sections (Vary Every Band!)**: Never repeat `[left list | right dark
  rounded card]` down the page. Use `discodungeon`'s **Screens Carousel**
  (`initScreensCarousel`) and **3D Radial Burst Cluster** (`initRadialBurst`),
  `marsrejects`'s **Tilted Stickers + Hairline Rows**, and 1 signature
  interactive builder/customizer.
- **Typography & Colors**: Use **any colors** the user asks for or that fit the
  domain. Do NOT repeat the cliché `01 · MONO EYEBROW + Instrument Serif +
  italic last word` header pattern on every section.
- **Single Clean Nav**: Use **either** a top bar **or** a compact bottom pill
  (with `padding-bottom: 104px` on `footer` so it never overlaps text).

### 3. Wire Recorded JS Interactions
Read [JS Interaction Recipes](./references/js-recipes.md) and implement **3–4
recorded mechanics**:
- `initDepthHero` (`marsrejects.com` 3D Z-layer parallax)
- `initScreensCarousel` & `initRadialBurst` (`discodungeongame.com`)
- `initScrollSpine` + `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) & `scale(0.9)` tap
- `initScrollMotion` & `initClosingTrail` (`pos.efisien.id` — keep CTA at higher `z-index` than trail stamps)

Respect `prefers-reduced-motion: reduce` and keyboard navigation.

### 4. Audit & Verify
Check [Anti-Slop Checklist](./references/anti-slop-checklist.md) and verify in
browser/build:
1. Real images/rich scenes present (no flat SVG diagram placeholders).
2. Middle sections have distinct layouts (not repeated 2-col dark cards).
3. Zero fixed-dock/trail overlap on buttons, rows, or footer text.
4. Zero JS console errors and clean mobile + desktop responsiveness.
