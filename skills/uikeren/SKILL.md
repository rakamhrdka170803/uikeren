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

# UI Keren — Anti-Slop Interactive Web Builder

Build websites that feel genuinely art-directed, visually rich, and alive—like
hand-crafted editorial and interactive product sites—never falling back to
cookie-cutter AI split-hero templates or tiny placeholder SVG boxes.

## Workflow

### 1. Choose Structural Archetype & Art Direction (Before Coding)
Read [Art Direction Reference](./references/art-direction.md) and define a
brief tailored to the prompt's domain (written in the user's language):
- **Pick an Archetype**: Choose Full-Bleed Scroll-Morph Editorial
  (`pos.efisien.id` DNA), High-Contrast Midnight Editorial (`marsrejects.com`
  DNA), or Layered Kinetic Showcase (`discodungeongame.com` DNA)—adapted
  authentically to the user's topic.
- **Visual Media Plan (CRITICAL)**: Never leave hero/showcase sections with
  tiny 24px–48px SVG icons inside bordered boxes! If `image-generator` is
  available, generate 2–4 bespoke images; otherwise render rich full-bleed
  HTML5 Canvas scenes or high-density interactive product previews.
- **Typography & Palette**: Expressive display font + clean body font + mono
  micro-labels; 1 dominant surface + 1 high-contrast ink + 1 sharp accent.

### 2. Assemble Recorded JS Interactions (Mandatory)
Read [JS Interaction Recipes](./references/js-recipes.md) and implement **2–4
recorded mechanics** suited to the domain and stack (Vanilla JS, React, Astro,
Next.js, Vue):
- **Full-Bleed Hero -> Mosaic Morph** (`initHeroMosaicMorph`)
- **Scroll Reveal, Clip-Path Wipe & Scrubbing** (`initScrollMotion`)
- **Closing Cursor & Ambient Trail** (`initClosingTrail`)
- **Framer `backOut` Overshoot & `whileTap: scale(0.9)`**
- **Interactive Content Explorer / Live Builder / Drawer**
- **Full-Bleed Canvas Atmosphere** (`initAmbientCanvas` when no image assets exist)

Ensure all motion respects `prefers-reduced-motion: reduce` and keyboard focus.

### 3. Enforce Anti-AI-Slop Guardrails (Hard Reject Gate)
Audit against [Anti-Slop Checklist](./references/anti-slop-checklist.md) BEFORE
finalizing. Specifically reject:
- 50/50 split hero (`left text + 3 stats | right 2x3 box of tiny SVGs`)
- Default neo-brutalist cream (`#F6F3EC`) + orange (`#FF5A36`) + `2px black`
  borders unless requested
- Tiny inline SVG icons pretending to be product photography or illustration

### 4. Verify Before Finishing
1. Test all interactive controls (tabs, builders, carts, drawers, canvas/demos)
   and verify real state updates.
2. Verify responsive layout at mobile (`~375px`) and desktop (`~1280px+`)
   with zero horizontal overflow.
3. Confirm clean build/launch with zero JS console errors.
