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

Craft websites that **re-interpret and blend** the visual drama, layering, and
JS motion physics recorded from `pos.efisien.id`, `marsrejects.com`, and
`discodungeongame.com`—so every section from Hero to Footer feels original,
cohesive, and alive (never generic AI middle sections and never a 1:1 clone).

## Workflow

### 1. Plan an Original Reference Blend (Before Coding)
Read [Art Direction Reference](./references/art-direction.md):
- **Hero**: Full-bleed atmospheric stage (`100vh`) with `pos.efisien.id`-scale
  display typography or `marsrejects`-style text-behind-subject depth. Never a
  50/50 split box hero.
- **Middle Sections (Crucial — Avoid Dry Text Lists)**: Never leave middle
  sections as plain pill tabs + bare text rows. Pair interactive hairline lists
  with a **sticky live photo/preview card** or interactive customizer that
  reacts on hover/click.
- **Showcase & Closing (Inspired, Not "Plek Ketiplek")**: Re-invent the dark
  showcase & closing trail for the domain—do NOT copy any reference section's
  exact 3-card geometry verbatim.
- **Navigation Hygiene**: Use **either** a clean top navbar **or** a non-blocking
  floating bottom dock—never stack both so they overlap scrolling content.
- **Colors & Real Visuals**: Use any palette requested by the user or fitting
  the domain (no banned colors). Use generated/real photos (`image-generator` if
  available) or rich full-bleed HTML5 `<canvas>`/interactive frames—never tiny
  24–48px inline SVGs inside empty boxes.

### 2. Wire Recorded JS Interactions
Read [JS Interaction Recipes](./references/js-recipes.md) and implement **2–4
recorded mechanics** suited to the domain and stack (Vanilla JS, React, Astro,
Next.js, Vue):
- `initHeroMosaicMorph` (full-bleed hero -> checkerboard morph)
- `initScrollMotion` (650ms reveal, `clip-path` wipe, `easeOutCubic` scrub)
- **Text-Behind-Subject** + non-overlapping navigation
- `initScrollSpine` + `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) & `scale(0.9)` tap
- `initClosingTrail` (8-node pooled cursor trail + 2200ms ambient auto-spawn)
- `initInteractiveTabs` / hover-synced sticky preview / stateful cart or builder

Respect `prefers-reduced-motion: reduce` and keyboard navigation.

### 3. Audit Against Anti-AI-Slop Checklist
Check [Anti-Slop Checklist](./references/anti-slop-checklist.md) before finishing:
- Zero overlap between floating docks/navbars and list content.
- Zero dry text-only middle sections without visual anchors.
- Zero 1:1 literal clones of a reference section.
- Zero dead buttons or placeholder copy.

### 4. Verify Before Finishing
1. Test every interactive control (tabs, hover/click preview, builders, carts)
   for real state updates.
2. Check mobile (`~375px`) and desktop (`~1280px+`) viewports for **zero
   overlapping fixed elements** and zero horizontal overflow.
3. Confirm clean build/launch with zero JS console errors.
