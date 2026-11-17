---
name: uikeren
description: >-
  Core web craft skill for UI Keren. Activate whenever the user asks—in any
  language—to build, design, or redesign a website, landing page, or interactive
  web UI. Combines bespoke visual direction, real image generation, recorded
  JS physics from marsrejects.com, discodungeongame.com, and pos.efisien.id,
  and a pre-ship quality check.
---

# UI Keren — Core Web Craft Engine

Load `uikeren-craft`, `uikeren-motion`, and `uikeren-responsive` together with
this skill on every web build.

## 1. Creative Brief & Intensity Profile (Before Writing Code)
Write one short brief line in the user's language before coding:
> `Brief: <jenis web> untuk <audiens>, memadukan <unsur 3 referensi>, profil Visual <1-3> / Variasi <1-3> / Gerak <1-3>.`

| Dimension | 1 (Subtle) | 2 (Balanced) | 3 (High Craft — Default) |
| :--- | :--- | :--- | :--- |
| **Visual Punch** | Clean minimal | Editorial + accents | Monumental scale, 3D Z-depth, rich imagery |
| **Band Contrast** | Consistent | Occasional shift | Every band changes composition & rhythm |
| **Motion Depth** | Hover states | Reveals + tabs | Depth parallax, radial burst, carousel, trail |

Default target for `uikeren` sites is **3 / 3 / 3** unless the user requests
a calm utility layout.

## 2. Intent Checks (Write a 1-Line Reason Before Coding)
Every major choice must have a concrete purpose, not an AI habit:
- **Color Choice**: Any palette is valid (including any color requested by
  the user); keep active core colors disciplined (2–3 core + 1 accent) with
  strong contrast.
- **Type Voice**: Pick a characterful display + body pairing fit for the topic.
  Never repeat `01 · MONO EYEBROW` + `Instrument Serif` + *italic last word* on
  every heading.
- **Real Media (`imgs > 0`)**: If `image-generator` is available, **generate
  2–4 cohesive images first** (hero scene + product/story shots). Never replace
  real photography/art with flat inline `<svg>` drawings (coffee beans, cups,
  contour lines, boxes).
- **Band Variety**: Sections 2, 3, and 4 must each use **different layouts**—do
  not stack repeated `[Left Text | Right Dark Rounded Card]` or 2x3 card grids.
- **Original Synthesis**: Borrow the *mechanics* from `marsrejects.com`,
  `discodungeongame.com`, and `pos.efisien.id`, re-interpreted for the user's
  brand—never clone any reference section 1:1.
- **Single Navigation**: Choose **either** a top navbar **or** a bottom pill
  (with `padding-bottom: 112px` on `footer`)—never stack both over scrolling
  content.
- **Live Controls**: Every button, tab, carousel, builder, or drawer must
  update real UI state (zero dead controls).
- **Natural Copy**: Write direct, domain-specific prose in the prompt's
  language—no buzzwords (*"Revolutionize"*, *"Seamless"*, *"Elevate"*), no
  invented `10K+` stats, no excessive em dashes (`—`).

## 3. Pre-Ship Verification (Run Before Answering)
Do not deliver until every check passes:
- [ ] **Real Images Present**: At least 2–4 real `<img>` visuals (`object-cover`)
      or rich full-bleed `<canvas>` scenes—no `imgs: 0` with flat SVG doodles.
- [ ] **Visual Filter (`uikeren-craft`)**: Zero pulsing status-dot pills above
      H1, zero 2x3 copy-paste card grids, zero decorative background grid lines,
      zero uniform pill-everything styling.
- [ ] **Distinct Middle Bands**: Hero, Band 2, Band 3, and Closing each look
      structurally distinct.
- [ ] **Active JS Mechanics (`uikeren-motion`)**: At least 3 recorded motion
      or interactive behaviors wired & tested, honoring `prefers-reduced-motion`.
- [ ] **Responsive & Clean (`uikeren-responsive`)**: Verified at desktop
      (`1440px`) and mobile (`375px`) with zero horizontal scroll, zero dock
      or trail overlap on text/buttons, and zero console errors.
