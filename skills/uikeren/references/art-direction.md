# Recorded Design & Layout DNA (3 Reference Sites)

Recorded via headless Chrome/Playwright inspection of `pos.efisien.id`,
`marsrejects.com`, and `discodungeongame.com`. **Re-interpret and blend their
principles originally**—never clone any single section 1:1 ("plek ketiplek").

---

## What to Take from Each Reference (Principle, Not Literal Clone)

1. **From `pos.efisien.id` — Full-Bleed Cinema & Scroll Transitions**:
   - **Principle**: Full-bleed `100vh` atmospheric opening with bold serif+sans
     scale contrast (`~74px` display vs `16px` body), alternating clean light
     and deep dark bands, scroll-triggered morphing/clip-path reveals, and a
     pooled closing cursor trail.
   - **Original Re-interpretation**: Do NOT copy the exact centered 1-landscape
     + 2-flanking-square photo trio in a dark void. Instead, build domain-native
     compositions (e.g., asymmetric staggered photo stack + interactive story
     tabs, or full-bleed split showcase with live tasting/product controls).

2. **From `marsrejects.com` — Z-Index Depth, Stickers & Hairline Editorial**:
   - **Principle**: Oversized display typography layered **behind** a
     foreground subject (`z-index`), tilted caption stickers overlapping visual
     frames, and crisp `1px` hairline-divided rows.
   - **Original Re-interpretation**: Never drop bare hairline rows alone across
     a whole viewport (that looks like an empty text list). Pair hairline rows
     with a **sticky live visual preview card** (photo + live specs + add/build
     action) on the opposite column, and if using a floating dock, do **not**
     also clutter the page with a competing sticky top bar that traps text.

3. **From `discodungeongame.com` — Continuous Journey & Interactive Stage**:
   - **Principle**: A persistent visual thread/scroll-spine connecting sections,
     plus a realistic framed interactive device/builder alongside concise copy
     with `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) micro-physics.
   - **Original Re-interpretation**: Turn the framed UI into something real for
     the user's topic (a live bakpao box builder, live pour-over/brew timer,
     live POS simulator, or mini playable canvas).

---

## Visual Balance Rule Across ALL Sections (Top -> Middle -> Bottom)
- **Section 1 (Hero)**: Full-bleed visual drama (`100vh` photo/art/canvas +
  monumental type).
- **Sections 2 & 3 (Middle — Where AI Usually Gets Boring!)**:
  - Never just pill tabs + plain text rows!
  - Combine **interactive controls + visual preview** in an asymmetric layout
    (e.g., `55%` interactive hairline menu/builder + `45%` sticky photo/live
    preview card that swaps image & details on hover/click), or bento visual
    storytelling with overlapping stickers.
- **Section 4+ (Showcase & Closing)**: Deep contrast band with an **original**
  interactive gallery/showcase (not a 1:1 copy of a reference) + `ClosingTrail`
  finale.
- **Colors**: Use any palette the user requests or that fits the domain—never
  ban colors.
