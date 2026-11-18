---
name: uikeren-responsive
description: >-
  Mobile-first responsive reflow and touch hygiene skill for UI Keren. Prevents
  bloated 9000px mobile stacks, multi-row cramped mobile headers, overlapping
  floating buttons, horizontal overflow, and undersized tap targets.
---

# UI Keren — Mobile-First Reflow & Safe Spacing

Use with `uikeren/SKILL.md`. Always inspect and design the **`375px` mobile
view** as a first-class layout—never a giant vertical pile of desktop cards.

## Mandatory Mobile (`< 768px`) Rules
- **Single-Row Compact Header (`<= 64px`)**: Keep mobile `<header>` on **one
  horizontal row** (`Brand left | 1 CTA or Menu button right`). NEVER stack
  address, opening hours, logo, and CTA into 3–4 vertical rows in the mobile
  header—move secondary metadata into the mobile menu drawer and footer.
- **Zero Floating Overlap**: Do NOT float a fixed `(≡)` circle or bottom bar
  over buttons, cards, or footer text on mobile. If a bottom bar is ever
  explicitly requested, hide it cleanly on scroll or reserve `padding-bottom:
  112px` so zero text or CTA is ever covered.
- **Kill the 9,000px Mobile Card Tunnel**: Never stack 6+ tall bordered cards
  one-by-one down a `375px` screen. On mobile (`< 768px`), turn multi-item
  card sets into either:
  1. A **horizontal snap-scroll strip** (`display: flex; overflow-x: auto;
     scroll-snap-type: x mandatory; gap: 12px`), OR
  2. A **compact 2-column visual grid** / **clean hairline list**.
- **Tight Mobile Rhythm**: Scale section padding down to `40px–56px` on
  mobile (instead of `96px–128px`), use fluid `clamp()` display typography, and
  avoid `100vh` slabs that push content below the fold.
- **Touch Parity & Zero Overflow**: `>= 44x44px` tap targets; every hover state
  must also work on tap; `document.documentElement.scrollWidth <= window.innerWidth`
  across `375px`, `768px`, and `1440px`.
