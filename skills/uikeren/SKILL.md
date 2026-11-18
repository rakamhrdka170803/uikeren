---
name: uikeren
description: >-
  Core web craft skill for UI Keren. Activate whenever the user asks—in any
  language—to build, design, or redesign a website, landing page, or interactive
  web UI. Enforces non-SaaS navigation, full-bleed non-boxed layouts, real
  photography, concise SEO copy, modern Node/Vite stack (never Python server),
  and recorded JS mechanics from marsrejects.com, discodungeongame.com, and
  pos.efisien.id.
---

# UI Keren — Core Web Craft Engine

Load `uikeren-craft`, `uikeren-motion`, and `uikeren-responsive` together with
this skill on every web build.

## 1. Tech Stack & Preview Rule
- Build with **modern frontend tooling** (Node + Vite / React / Astro / Vanilla
  ESM) and preview via Vite (`npm run dev`) or `npx serve`. **NEVER** use
  `python -m http.server` or Python scripts unless the user explicitly asks
  for Python.

## 2. Creative Brief & Anti-Template Plan (Before Writing Code)
State one short brief line in the user's language, then choose non-generic
structures for **every** zone:
- **Navigation (NO Boring SaaS Top Bar!)**: **FORBIDDEN**: `[Logo Left | 4
  Centered Links | 1 Pill CTA Right]` on a solid bar! Pick one of:
  1. **No Top Bar / Corner Masthead + Compact Menu Trigger** (`marsrejects.com`
     style): clean brand mark + single `Menu` trigger opening a sleek overlay.
  2. **Transparent Hero-Overlay Nav** (`discodungeongame.com` / `pos.efisien.id`
     style): borderless transparent nav floating cleanly over full-bleed hero
     media, zero bulky pill CTA box.
- **Hero (`100%` Full-Bleed — NEVER 50/50 Split)**: Hero imagery/scene MUST
  span **edge-to-edge full width** (`100%` viewport) with headline layered
  over/behind the subject (`marsrejects` Z-depth or `pos.efisien.id` full-bleed
  backdrop). **FORBIDDEN**: `[Left text + 2 buttons | Right 1 photo card]`.
  Max **2 lines** for `<h1>` (never ultra-wide fonts wrapping to 4 lines).
- **Middle Sections (NO Box-Wrapped Cards Everywhere!)**: **FORBIDDEN**:
  - 4 identical white/dark cards in a row (`[img] + [title] + [2-line desc]`).
  - Vertical line + dot + 4 stacked horizontal white rounded cards (`01..04`).
  - Wrapping every form/FAQ/order summary in `1px` bordered rounded SaaS boxes.
  Instead use **borderless editorial photography**, **open hairline rows**
  (`border-bottom: 1px` with no outer box), **3D radial cluster**, or an
  **interactive split preview** where clicking rows swaps a large photo.
- **Colors**: Never ban colors (honor any user request), but **deprioritize**
  warm cream (`#FAF5EC`) + dark brown/black + amber/terracotta defaults.
- **Real Media (`imgs > 0`) & Short SEO Copy**: Invoke `image-generator` for
  real editorial photos (`object-cover`); keep cards `<= 10 words` and hero
  subcopy `<= 16 words`, while putting full SEO in `<title>`, `<meta>`,
  OpenGraph, semantic HTML, and JSON-LD.

## 3. Pre-Ship Verification (Run Before Answering)
- [ ] **No Python server** used; runs cleanly via Vite / Node.
- [ ] **Non-boring Nav**: Not `[Logo | 4 Links | Pill CTA]` solid header.
- [ ] **Full-Bleed Hero (<= 2-line H1)**: Not `[text left | 1 photo card right]`.
- [ ] **No Card-Box Spam**: No 4-card identical grid rows, no vertical-line
      `01..04` stacked rounded boxes, no boxed SaaS FAQ/form wrappers.
- [ ] **Real Images + Short Copy + SEO**: Real `<img>` assets, concise copy,
      `<meta>` + JSON-LD intact, `375px` mobile & `1440px` desktop verified
      with zero horizontal overflow or floating overlap.
