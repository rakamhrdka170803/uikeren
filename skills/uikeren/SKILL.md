---
name: uikeren
description: >-
  Core web craft skill for UI Keren. Activate whenever the user asks—in any
  language—to build, design, or redesign a website, landing page, or interactive
  web UI. Combines bespoke visual direction, photorealistic/editorial image
  generation, technical SEO without bloated copy, mobile-first reflow, and
  recorded JS physics from marsrejects.com, discodungeongame.com, and
  pos.efisien.id.
---

# UI Keren — Core Web Craft Engine

Load `uikeren-craft`, `uikeren-motion`, and `uikeren-responsive` together with
this skill on every web build.

## 1. Creative Brief & Intensity Profile (Before Writing Code)
Write one short brief line in the user's language before coding:
> `Brief: <jenis web> untuk <audiens>, memadukan <unsur 3 referensi>, profil Visual <1-3> / Variasi <1-3> / Gerak <1-3>.`

| Dimension | 1 (Subtle) | 2 (Balanced) | 3 (High Craft — Default) |
| :--- | :--- | :--- | :--- |
| **Visual Punch** | Clean minimal | Editorial + accents | Monumental scale, 3D Z-depth, rich real imagery |
| **Band Contrast** | Consistent | Occasional shift | Every band changes composition & rhythm |
| **Motion Depth** | Hover states | Reveals + tabs | Depth parallax, radial burst, carousel, spine |

Default target is **3 / 3 / 3**.

## 2. Intent Checks (Write a 1-Line Reason Before Coding)
- **Color Choice**: Any color is allowed (never ban colors, and always honor
  user-requested colors), but **deprioritize** autopilot AI combos (`warm cream
  + dark brown + terracotta` or `slate + purple glow`) unless requested.
- **Type Voice**: Characterful display + body pairing. Never repeat
  `01 · MONO EYEBROW` + `Instrument Serif` + *italic last word* on every heading.
- **Real Photorealistic / Editorial Media (`imgs > 0`)**: If `image-generator`
  is available, generate **3–5 real editorial photographs or detailed
  illustrations** (hero + showcase/product cards)—explicitly requesting rich
  lighting, texture, and realism, **NEVER flat cartoon/vector clip-art**.
- **Equal 3-Reference Balance**: Actively lead with `marsrejects.com` (3D
  text-behind-subject, tilted caption stickers, hairline rows) and
  `discodungeongame.com` (scroll-spine, 3D radial burst, horizontal screens
  carousel), using `pos.efisien.id` motion selectively rather than cloning it.
- **Concise Human Copy (Strict Word Budgets)**:
  - Hero `<h1>`: **3–7 words**.
  - Hero subheadline: **10–18 words** max (1–2 short lines).
  - Card / feature description: **6–12 words** max (1 crisp line—NEVER 2–3
    sentence AI essays inside cards!).
- **Technical SEO Without Visible Bloat**:
  - Put rich SEO into `<head>` and semantics—not bloated on-screen paragraphs!
  - Include `<title>` (50–60 chars), `<meta name="description">` (135–155 chars),
    OpenGraph (`og:title`, `og:description`, `og:image`, `og:type`), single
    `<h1>` + proper `<h2>`/`<h3>` hierarchy, semantic `<header>/<main>/<section>/
    <article>/<footer>`, descriptive `alt` on every `<img>`, and a domain-matched
    **JSON-LD** `<script type="application/ld+json">` (`LocalBusiness`,
    `Product`, `SoftwareApplication`, etc.).
- **Clean Single Navigation (Zero Floating Overlap)**: Use **one** clean single-row
  top bar (collapses to a clean header drawer on mobile—NO floating bottom
  circular `(≡)` or wide bottom capsule overlapping buttons, cards, or footer!).

## 3. Pre-Ship Verification (Run Before Answering)
Do not deliver until every check passes:
- [ ] **Real Photography/Art**: Hero & product cards use real rich imagery
      (`object-cover`, `naturalWidth > 0`), NOT flat cartoon vectors or text-only
      pastel-pill white boxes.
- [ ] **Copy & SEO Check**: Card descriptions are `<= 12 words`; `<title>`,
      `<meta name="description">`, OG tags, semantic landmarks, and JSON-LD
      present.
- [ ] **Mobile Inspect Check (`375px`)**: Single-row header (`<= 64px`), zero
      floating button overlapping text/buttons/footer, grids reflow into
      horizontal snap strips or compact stacks (no 9,000px mobile bloat),
      `scrollWidth <= 375`.
- [ ] **Active JS Mechanics (`uikeren-motion`)**: At least 3 recorded mechanics
      active & tested, honoring `prefers-reduced-motion`.
