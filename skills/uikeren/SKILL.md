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
| **Motion Depth** | Hover states | Reveals + tabs | Depth parallax, radial burst, carousel, spine |

Default target for `uikeren` sites is **3 / 3 / 3** unless the user requests
a calm utility layout.

## 2. Intent Checks (Write a 1-Line Reason Before Coding)
Every major choice must have a concrete purpose, not an AI autopilot habit:
- **Color Choice (Deprioritize AI Autopilot Palettes)**: Any color is allowed
  (never ban colors, and always honor colors requested by the user). However,
  **DO NOT default on autopilot** to `warm cream (#FAF5EC/#F6F3EC) + dark brown +
  terracotta/orange-red (#D83A22/#FF5A36)` or `dark slate + purple/indigo glow`!
  Explore fresher, domain-fit palettes first (e.g., celadon jade + porcelain +
  chili, midnight navy + electric coral + bone white, cobalt + cream + brass,
  charcoal + olive + butter, obsidian + cyan/magenta).
- **Type Voice**: Pick a characterful display + body pairing fit for the topic.
  Never repeat `01 · MONO EYEBROW` + `Instrument Serif` + *italic last word* on
  every heading.
- **Real Media (`imgs > 0`)**: If `image-generator` is available, **generate
  2–4 cohesive images first** (hero scene + product/story shots). Never replace
  real photography/art with flat inline `<svg>` drawings.
- **Equal 3-Reference Balance (Stop Leaning Toward `pos.efisien.id`!)**:
  Do NOT default to `pos.efisien.id`'s centered dark-photo hero + red/orange
  cursor-trail closing band every time. Actively lead with `marsrejects.com`
  (3D text-behind-subject hero, tilted story stickers, hairline rows, dark
  horizon footer) and `discodungeongame.com` (scroll-spine journey, 3D radial
  burst cluster, horizontal screens carousel, framed live stage), blending
  `pos.efisien.id` subtly rather than copying it.
- **Band Variety**: Sections 2, 3, and 4 must each use **different layouts**—do
  not stack repeated `[Left Text | Right Card]` or 2x3 identical boxes.
- **Zero-Collision Navigation**: Use **either** a clean top navbar **or** a
  compact collapsible bottom trigger (`<= 56px` circle when collapsed, never a
  wide 400px bar floating over scrolling buttons/text).
- **Live Controls & Natural Copy**: Every interactive control must mutate real
  state; zero buzzwords (*"Revolutionize"*, *"Seamless"*, *"Elevate"*), zero
  fake stats, zero excessive em dashes (`—`).

## 3. Pre-Ship Verification (Run Before Answering)
Do not deliver until every check passes:
- [ ] **Real Images Present**: At least 2–4 real `<img>` visuals (`object-cover`)
      or rich full-bleed `<canvas>` scenes—no `imgs: 0` with flat SVG doodles.
- [ ] **Palette & Reference Independence**: Did not fall back on autopilot to
      cream+terracotta or `pos.efisien.id`'s exact hero/closing-trail clone.
- [ ] **Visual Filter (`uikeren-craft`)**: Zero pulsing status-dot pills above
      H1, zero 2x3 copy-paste card grids, zero decorative background grid lines.
- [ ] **Active JS Mechanics (`uikeren-motion`)**: At least 3 recorded mechanics
      wired & tested, honoring `prefers-reduced-motion`.
- [ ] **Responsive & Overlap Check (`uikeren-responsive`)**: Tested at desktop
      (`1440px`) and mobile (`375px`) with zero horizontal scroll, **zero
      floating bar/trail overlapping buttons or text**, and zero console errors.
