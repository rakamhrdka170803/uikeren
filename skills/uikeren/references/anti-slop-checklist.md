# Anti-AI-Slop Checklist (Layout & Visual Craft)

**Note on Colors:** Never ban any color palette. Cream + orange, neon purple,
pastel, monochrome, or dark crimson are all valid—especially if the user asks
for them or the domain fits. What makes a site look like "AI slop" is **generic
layout structure and empty placeholder visuals**, NOT the color palette.

Reject and rebuild immediately if your design falls into these structural traps:

## 1. Banned Generic AI Layout Patterns
- [ ] **BAN the Default 50/50 AI Split Hero**: Do NOT build:
      Left = `[pill badge] + [3-line H1 with underlined word] + [2-line grey desc] + [2 buttons] + [3-number stat row]`
      Right = `[1 rounded-rectangle box holding a 2x3 or 3x2 grid of mini cards]`.
- [ ] **BAN Box-Inside-Box Card Grid Repetition**: Do NOT wrap every feature,
      menu item, or benefit in thick `2px` bordered boxes with hard drop
      shadows everywhere. Mix full-bleed visual panels, overlapping editorial
      layers, and clean hairline-divided list rows (`border-bottom: 1px solid`)
      like `marsrejects.com` and `pos.efisien.id`.
- [ ] **BAN Generic 3-Column Symmetric Icon Cards**: No identical 3 cards with
      small centered icons + heading + 2 lines of filler text.

## 2. Banned Empty "Tiny SVG Icon" Visuals
- [ ] **NEVER put 24px–48px inline SVG icons inside big empty cards** as a
      substitute for real imagery. That is the #1 reason generated sites look
      like AI slop.
- [ ] Instead, every hero and showcase frame MUST be filled edge-to-edge using:
      1. **Bespoke generated images** (call `image-generator` if available in
         the session to create real editorial photos/illustrations rendered
         with `object-fit: cover`), OR
      2. **Full-bleed interactive HTML5 `<canvas>` / detailed layered scene**
         that fills 100% of its container with lighting, depth, and motion, OR
      3. **Realistic framed UI/device showcase** with high-density interactive
         controls (like `discodungeongame.com`'s live game frame).

## 3. Copy & JS Interaction Guardrails
- [ ] **No cliché AI filler copy** (*"Revolutionize"*, *"Seamless"*,
      *"Unleash"*, *"Elevate"*). Write concrete, domain-authentic copy in the
      user's language.
- [ ] **No dead buttons**: Every nav item, CTA, tab, card, or dock icon must
      scroll/navigate meaningfully or mutate live JS state.
- [ ] **Smooth GPU motion**: Animate `transform`, `opacity`, and `clip-path`,
      and always support `prefers-reduced-motion: reduce`.
