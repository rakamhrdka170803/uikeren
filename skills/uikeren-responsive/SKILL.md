---
name: uikeren-responsive
description: >-
  Responsive layout and touch hygiene skill for UI Keren. Prevents horizontal
  overflow, overlapping fixed bottom docks, desktop-only 100vh slabs,
  hover-only interactions, and undersized tap targets across viewports.
---

# UI Keren — Responsive Reflow & Safe Spacing

Use with `uikeren/SKILL.md`. Mobile and tablet layouts must reflow with
intent, never just shrink desktop proportions.

## Reflow Rules
- **3-State Fluidity**: Support single-column phone, 2-column tablet, and
  multi-column desktop (`minmax()` / `auto-fit`), with `min-width: 0` on grid
  and flex children so carousels or long headlines never push wider than `100vw`.
- **Fluid Display Scale (`clamp()`)**: Never leave `74px–88px` fixed desktop
  sizes on narrow `375px` viewports.
- **Dynamic Viewport Heights**: Prefer `min-height: 85dvh` or `auto` on mobile
  so browser address bars do not clip hero CTAs.
- **Safe Bottom Dock Clearance**: When using a fixed bottom pill, reserve
  `padding-bottom: 112px` on `footer` and `scroll-padding-bottom: 96px` on
  `html` so fixed navigation never covers links or list rows.
- **Touch & Tap Parity**: Minimum `44x44px` hit target on controls; every hover
  preview must also work on click/tap.
- **Zero Horizontal Scroll**: Verify `scrollWidth <= innerWidth` at `375px` and
  `1440px`.
