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

Specifically craft websites that **combine the layout drama, visual richness,
and JS interaction craft** recorded from `pos.efisien.id`, `marsrejects.com`,
and `discodungeongame.com`—adapted to any topic and any color palette the user
wants.

## Workflow

### 1. Plan the Reference Blend & Visual Assets (Before Coding)
Read [Art Direction Reference](./references/art-direction.md) and choose how to
**blend** the three recorded reference styles for the user's domain:
- **Hero Architecture**: Pick either `pos.efisien.id` full-bleed `100vh` hero
  -> checkerboard mosaic morph, `marsrejects.com` **text-behind-subject**
  layered hero, or `discodungeongame.com` atmospheric stage + floating central
  anchor. Never default to a cramped 50/50 split box hero.
- **Section Blending**: Mix full-bleed visual cards, tilted sticker captions,
  clean **hairline-divided editorial lists** (`border-bottom: 1px solid`),
  asymmetric framed UI/device showcases, and a dark closing band.
- **Colors**: Follow any color palette the user asks for, or pick a palette
  suited to the domain—there are **no banned colors**.
- **Real Visuals (MANDATORY)**: Never use tiny 24–48px SVG icons inside empty
  boxes as hero/card art! If `image-generator` is available, generate real
  bespoke hero & card images (`object-cover`); otherwise build rich full-bleed
  HTML5 `<canvas>` scenes or detailed interactive UI mockups.

### 2. Wire Recorded JS Interactions
Read [JS Interaction Recipes](./references/js-recipes.md) and implement **2–4
recorded mechanics** suited to the site and stack (Vanilla JS, React, Astro,
Next.js, Vue):
- `initHeroMosaicMorph` (full-bleed hero shrinking into checkerboard mosaic)
- `initScrollMotion` (650ms reveal, `clip-path` wipe, `easeOutCubic` scrub)
- **Text-Behind-Subject + Floating Bottom Dock** (`marsrejects.com` layout)
- `initScrollSpine` + `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) & `scale(0.9)` tap
- `initClosingTrail` (8-node pooled cursor trail + 2200ms ambient auto-spawn)
- `initInteractiveTabs` / stateful builder + `initAmbientCanvas`

Respect `prefers-reduced-motion: reduce` and keyboard navigation.

### 3. Audit Against Anti-AI-Slop Checklist
Check [Anti-Slop Checklist](./references/anti-slop-checklist.md) before finishing:
- Reject 50/50 split box heroes (`left text + 3 stats | right 2x3 mini-cards`).
- Reject tiny SVG sprites pretending to be product photography/illustration.
- Reject dead buttons or boilerplate AI copy.

### 4. Verify Before Finishing
1. Test every interactive control (tabs, builders, carts, dock, canvas) for
   real state updates.
2. Check mobile (`~375px`) and desktop (`~1280px+`) responsiveness with zero
   horizontal overflow.
3. Confirm clean build/launch with zero JS console errors.
