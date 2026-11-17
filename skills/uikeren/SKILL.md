---
name: uikeren
description: >-
  Use this skill whenever the user asks—in any language—to build, design,
  create, or redesign a website, landing page, web UI, or interactive frontend
  (e.g. "buatkan web bapau", "bikinin landing page", "build a product website",
  "create an interactive site"). Enforces bespoke art direction, recorded
  high-craft JavaScript interactions, tactile motion, and anti-AI-slop design
  standards adapted to the user's domain.
---

# UI Keren — Anti-Slop Interactive Web Builder

Build websites that feel hand-crafted, memorable, and alive—combining strong
art direction with real JavaScript interactivity—while adapting the aesthetic
authentically to whatever topic the user requests.

## Workflow

### 1. Define the Creative Direction Brief (Before Coding)
Never start with generic boilerplate. Establish a brief tailored to the
prompt's domain and written in the user's requested language:
- **Domain Persona & Mood**: Match the subject authentically (e.g., warm
  tactile street-food craft for a bakpao shop; sharp high-contrast utility for
  a POS/SaaS; kinetic arcade energy for a game). Never copy another brand's
  content or literal theme.
- **Typography Pairing**: Pick an expressive display font + a clean body font
  + a monospace font for micro-labels/prices/specs. Load real fonts (e.g.,
  Google Fonts) with strong hierarchy and tight display tracking.
- **Color System**: Choose 1 dominant background/surface, 1 high-contrast ink,
  and 1 intentional accent color (plus subtle surface tints).
- **Signature Visual Motif**: Pick 1–2 unifying motifs (e.g., editorial border
  grids, tactile sticker badges, halftone/paper grain, asymmetric bento cards).

Read [Art Direction Reference](./references/art-direction.md) when designing
the visual system and layout rhythm.

### 2. Assemble Recorded JS Interactions (Mandatory)
Treat JavaScript and motion as core user experience, not static decoration.
Read [JS Interaction Recipes](./references/js-recipes.md) and select **2–4
recorded mechanics** that fit the user's domain (and work cleanly in the
project's stack—Vanilla JS, React, Astro, Next.js, Vue, etc.):
- **Hero Mosaic / Bento Morph** or **Kinetic Marquee** for immediate above-the-fold
  energy.
- **Scroll Choreography & Progress Scrubbing** (`IntersectionObserver` +
  `requestAnimationFrame` CSS variable `--scroll-p`) for smooth section pacing.
- **Interactive Feature/Product Switcher, Live Simulator, or Builder + Drawer**
  so the user can actually click, filter, customize, or add items with live
  state updates.
- **Spring Tactile Cards / Magnetic Hover** and/or **Closing Cursor Trail** for
  memorable micro-feedback.

Ensure all motion respects `prefers-reduced-motion: reduce` and all interactive
controls support keyboard focus.

### 3. Enforce Anti-AI-Slop Guardrails
Before and during implementation, audit your layout, copy, and components
against [Anti-Slop Checklist](./references/anti-slop-checklist.md) so the result
never looks like a cookie-cutter AI template.

### 4. Verify Before Finishing
1. Check that all interactive JS widgets (tabs, filters, customizers, cart/menu
   drawers, modals, forms) actually mutate state and respond smoothly.
2. Verify responsive layout at mobile (`~375px`) and desktop (`~1280px+`)
   widths with zero horizontal overflow or clipped typography.
3. Confirm the project builds/opens cleanly with zero JavaScript console errors.
