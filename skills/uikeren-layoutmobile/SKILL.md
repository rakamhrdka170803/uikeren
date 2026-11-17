---
name: uikeren-layoutmobile
description: >-
  Mobile and responsive layout skill for UI Keren. Prevents horizontal overflow,
  overlapping fixed bottom docks, desktop-only 100vh slabs, hover-only menus,
  and undersized tap targets across mobile, tablet, and desktop.
---

# UI Keren — Mobile & Responsive Reflow

Use alongside `uikeren/SKILL.md`. Mobile is a **deliberately reflowed layout**,
not a shrunk desktop page.

## Required Reflow Rules
- **3-State Fluidity**: Never jump straight from 1-col mobile to 4-col desktop
  without an intermediate tablet step (`minmax()` / `auto-fit`). Always put
  `min-width: 0` on grid/flex children so text or carousels never push wider
  than `100vw`.
- **Fluid Type (`clamp()`)**: Never keep fixed `74px–88px` desktop display font
  sizes on `375px` viewports.
- **No `100vh` Mobile Slabs**: Use `min-height: 85dvh` or `auto` on narrow
  screens so browser chrome never clips CTAs.
- **Zero Bottom-Dock Content Collision**: If using a fixed bottom pill dock,
  reserve at least `padding-bottom: 112px` on `footer` and `scroll-padding-bottom: 96px`
  on `html` so anchor links and footer copy are never covered.
- **Touch & Tap Targets**: Minimum `44x44px` hit target on buttons, tabs,
  carousel arrows, and pagination dots. Every hover preview must also activate
  on click/tap for touchscreens.
- **Zero Horizontal Overflow**: Verify `document.documentElement.scrollWidth <= window.innerWidth`
  at `375px` and `1440px`.
