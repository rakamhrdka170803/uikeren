---
name: uikeren-responsive
description: >-
  Mobile-first responsive reflow and touch hygiene skill for UI Keren. Prevents
  bloated mobile stacks, cramped multi-row mobile headers, overlapping floating
  buttons, horizontal overflow, and undersized tap targets.
---

# UI Keren — Mobile-First Reflow & Safe Spacing

Use with `uikeren/SKILL.md`. Always verify the **`375px` mobile view** so it
never collapses into a giant vertical pile of boxes.

## Mandatory Mobile (`< 768px`) Rules
- **Single-Row Minimal Header (`<= 64px`)**: Keep mobile masthead on **one
  clean row** (`Brand left | 1 Menu drawer button right`). Never stack address,
  hours, and links vertically inside `<header>`.
- **Zero Floating Overlap**: Do NOT float a fixed bottom button/bar over
  interactive controls, cards, or footer copy. Mobile menus belong inside a
  clean top-triggered drawer/overlay.
- **No 9,000px Stacked Card Tunnels**: On mobile (`< 768px`), convert multi-item
  showcases (`4+` items) into a **horizontal snap-scroll strip** (`overflow-x:
  auto; scroll-snap-type: x mandatory; gap: 12px`) or compact **open hairline
  rows**—never 6–10 tall boxed cards stacked vertically.
- **Fluid Scale & Tight Padding**: Use `clamp()` for headings so `<h1>` fits
  cleanly in 2–3 lines on `375px`, and tighten vertical section padding to
  `40px–56px` on mobile.
- **Touch Parity & Zero Overflow**: `>= 44x44px` tap targets; every hover
  preview works on tap; `scrollWidth <= innerWidth` across `375px`, `768px`,
  and `1440px`.
