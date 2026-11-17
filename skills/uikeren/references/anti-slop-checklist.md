# Anti-AI-Slop Checklist

Reject and rebuild immediately if your design contains ANY of these 2025/2026
AI-slop defaults:

## 1. Banned "AI Template" Hero & Palette Clichés
- [ ] **BAN the 50/50 Split Box Hero**: Do NOT default to:
      Left = `[pill badge] + [3-line H1 with 1 underlined accent word] + [2-line grey paragraph] + [2 buttons] + [3-stat row (e.g. 93°C | 4 | 15%)]`,
      Right = `[1 big rounded card containing a 2x3 or 3x2 grid of tiny cards]`.
- [ ] **BAN Neo-Brutalist Cream/Orange Slop**: Do NOT default to warm cream
      (`#F6F3EC`) + orange-red (`#FF5A36`) + `2px solid black` borders +
      `4px 4px 0 #000` hard shadows + black ticker bar under the hero, unless
      the user explicitly asks for neo-brutalism.
- [ ] **BAN Purple/Blue SaaS Gradient Blobs**: Do NOT default to generic
      purple/indigo radial blurs over white or `#0F172A` cards.
- [ ] **BAN 3-Column Symmetric Icon Cards**: No identical cards with small
      centered icons + title + 2 lines of filler text.

## 2. Banned "Tiny SVG Icon Placeholder" Visuals
- [ ] **NEVER use tiny 24px–48px inline SVG sprites inside big empty cards**
      as your hero or showcase visual. That immediately looks like cheap AI
      placeholder art.
- [ ] Instead, fill visual frames richly using one of:
      1. **Real generated/sourced artwork & photography** (use the
         `image-generator` tool if available, or high-craft assets) rendered
         `object-cover` full-bleed.
      2. **Rich HTML5 Canvas / interactive visual scenes** (procedural
         lighting, particles, playable/interactive viewport, or fluid motion).
      3. **High-density interactive product/UI mockups** with real typography,
         controls, live numbers, and layered depth.

## 3. Copy & Interaction Slop
- [ ] **No cliché AI buzzwords** (*"Revolutionize"*, *"Seamless"*, *"Unleash"*,
      *"Next-gen"*, *"Elevate"*, or stiff Indonesian translations).
- [ ] **No dead buttons or fake links**: Every CTA, nav item, tab, card, or
      builder control must navigate or update real interactive JS state.
- [ ] **No layout-thrashing animations**: Animate `transform`, `opacity`, and
      `clip-path` only; always guard with `prefers-reduced-motion: reduce`.
