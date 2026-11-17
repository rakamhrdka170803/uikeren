# Recorded JS Interaction Recipes

Reusable, framework-agnostic JavaScript + CSS interaction mechanics distilled
from high-craft interactive websites (`pos.efisien.id` Astro Islands,
`marsrejects.com`, and `discodungeongame.com` Framer-style tactile motion).

Adapt colors, copy, and assets to the user's domain—keep the motion physics
and state quality intact. Always wrap scroll/pointer animations with a
`prefers-reduced-motion: reduce` guard.

---

## Recipe 1: Hero Mosaic Morph (`HeroMosaicMorph` pattern)
Use when a hero needs dynamic visual energy: a grid/mosaic of tiles (products,
cards, scenes, or badges) that smoothly morphs/cycles active states and reacts
to pointer tilt.

```css
.mosaic-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.75rem;
}
.mosaic-tile {
  position: relative;
  border-radius: 1rem;
  overflow: hidden;
  transition: transform 650ms cubic-bezier(0.22, 1.4, 0.36, 1),
              opacity 450ms ease;
  will-change: transform;
}
.mosaic-tile.is-featured {
  transform: scale(1.04) translateY(-4px);
  z-index: 2;
}
@media (prefers-reduced-motion: reduce) {
  .mosaic-tile { transition: none; transform: none !important; }
}
```

```js
export function initHeroMosaic(container, intervalMs = 2600) {
  const tiles = [...container.querySelectorAll('.mosaic-tile')];
  if (!tiles.length) return;
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  let active = 0;

  const activate = (idx) => {
    tiles.forEach((t, i) => t.classList.toggle('is-featured', i === idx));
  };
  activate(0);

  if (reduced) return;
  let timer = setInterval(() => {
    active = (active + 1) % tiles.length;
    activate(active);
  }, intervalMs);

  tiles.forEach((tile, idx) => {
    tile.addEventListener('mouseenter', () => {
      clearInterval(timer);
      active = idx;
      activate(idx);
    });
  });
}
```

---

## Recipe 2: Scroll Choreography & Progress Scrubbing (`ScrollMotion` pattern)
Combines `IntersectionObserver` staggered reveals with a lightweight
`requestAnimationFrame` scroll progress CSS variable (`--scroll-p` from `0` to
`1`) for parallax/rotation without layout thrashing.

```css
[data-reveal] {
  opacity: 0;
  transform: translateY(22px) scale(0.98);
  transition: opacity 600ms ease,
              transform 700ms cubic-bezier(0.22, 1, 0.36, 1);
  transition-delay: var(--stagger, 0ms);
}
[data-reveal].is-visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}
[data-scrub] {
  transform: translate3d(0, calc((var(--scroll-p, 0.5) - 0.5) * -36px), 0);
  will-change: transform;
}
@media (prefers-reduced-motion: reduce) {
  [data-reveal] { opacity: 1; transform: none; transition: none; }
  [data-scrub] { transform: none !important; }
}
```

```js
export function initScrollMotion() {
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const reveals = document.querySelectorAll('[data-reveal]');

  if (reduced) {
    reveals.forEach((el) => el.classList.add('is-visible'));
    return;
  }

  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        io.unobserve(entry.target);
      }
    });
  }, { threshold: 0.14, rootMargin: '0px 0px -40px 0px' });

  reveals.forEach((el, idx) => {
    if (!el.style.getPropertyValue('--stagger')) {
      el.style.setProperty('--stagger', `${(idx % 4) * 75}ms`);
    }
    io.observe(el);
  });

  const scrubs = [...document.querySelectorAll('[data-scrub]')];
  if (!scrubs.length) return;

  let ticking = false;
  const updateScrub = () => {
    const vh = window.innerHeight || 1;
    scrubs.forEach((el) => {
      const rect = el.getBoundingClientRect();
      const p = Math.min(1, Math.max(0, (vh - rect.top) / (vh + rect.height)));
      el.style.setProperty('--scroll-p', p.toFixed(4));
    });
    ticking = false;
  };

  window.addEventListener('scroll', () => {
    if (!ticking) {
      ticking = true;
      requestAnimationFrame(updateScrub);
    }
  }, { passive: true });
  updateScrub();
}
```

---

## Recipe 3: Interactive Feature / Product Switcher & Live State (`LandingInteractive` pattern)
Replaces dead static cards with a live switcher, filter, or builder (e.g., POS
module switcher, bakpao box/flavor customizer, or game character/skill tab)
that updates both preview UI and state counters smoothly.

```js
export function initInteractiveTabs({ tabSelector, panelSelector, onSwitch }) {
  const tabs = [...document.querySelectorAll(tabSelector)];
  const panels = [...document.querySelectorAll(panelSelector)];
  if (!tabs.length) return;

  const select = (targetId) => {
    tabs.forEach((tab) => {
      const active = tab.dataset.tab === targetId;
      tab.classList.toggle('is-active', active);
      tab.setAttribute('aria-selected', String(active));
    });
    panels.forEach((panel) => {
      const active = panel.dataset.panel === targetId;
      panel.hidden = !active;
      panel.classList.toggle('is-active', active);
    });
    if (onSwitch) onSwitch(targetId);
  };

  tabs.forEach((tab) => {
    tab.addEventListener('click', () => select(tab.dataset.tab));
  });
  select(tabs[0].dataset.tab);
}
```

---

## Recipe 4: Spring Tactile Cards & Magnetic Hover (Framer-style micro-physics)
Gives buttons, stickers, and cards a physical spring feel on hover and press.

```css
.tactile-card {
  transition: transform 420ms cubic-bezier(0.22, 1.4, 0.36, 1),
              box-shadow 300ms ease;
}
.tactile-card:hover {
  transform: translateY(-4px) rotate(var(--tilt, -0.8deg));
}
.tactile-card:active {
  transform: translateY(1px) scale(0.985);
}
```

```js
export function initMagneticButtons(selector = '[data-magnetic]') {
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
  document.querySelectorAll(selector).forEach((btn) => {
    btn.addEventListener('pointermove', (e) => {
      const r = btn.getBoundingClientRect();
      const dx = (e.clientX - (r.left + r.width / 2)) * 0.18;
      const dy = (e.clientY - (r.top + r.height / 2)) * 0.18;
      btn.style.transform = `translate3d(${dx.toFixed(1)}px, ${dy.toFixed(1)}px, 0)`;
    });
    btn.addEventListener('pointerleave', () => {
      btn.style.transform = '';
    });
  });
}
```

---

## Recipe 5: Closing Interactive Cursor Trail (`ClosingTrailSection` pattern)
Spawns throttled, gently rotated floating stickers/badges/thumbnails as the
pointer moves across a closing CTA band, then fades them out cleanly.

```js
export function initClosingTrail(section, items = []) {
  if (!section || !items.length) return;
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
  if (window.matchMedia('(pointer: coarse)').matches) return;

  let lastX = 0;
  let lastY = 0;
  let idx = 0;

  section.style.position = 'relative';
  section.style.overflow = 'hidden';

  section.addEventListener('pointermove', (e) => {
    const rect = section.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    if (Math.hypot(x - lastX, y - lastY) < 75) return;
    lastX = x;
    lastY = y;

    const badge = document.createElement('span');
    badge.className = 'trail-stamp';
    badge.textContent = items[idx % items.length];
    idx++;

    const rot = (Math.random() * 18 - 9).toFixed(1);
    Object.assign(badge.style, {
      position: 'absolute',
      left: `${x}px`,
      top: `${y}px`,
      pointerEvents: 'none',
      transform: `translate(-50%, -50%) rotate(${rot}deg) scale(0.85)`,
      opacity: '1',
      transition: 'transform 650ms cubic-bezier(0.22, 1, 0.36, 1), opacity 650ms ease',
      zIndex: '1'
    });

    section.appendChild(badge);
    requestAnimationFrame(() => {
      badge.style.transform = `translate(-50%, -65%) rotate(${rot}deg) scale(1.05)`;
      badge.style.opacity = '0';
    });
    setTimeout(() => badge.remove(), 680);
  });
}
```

---

## Recipe 6: Kinetic Marquee / Ticker
Seamless infinite horizontal strip for slogans, flavors, features, or community
tags—pauses on hover and stops automatically under `prefers-reduced-motion`.

```css
.marquee-wrap { overflow: hidden; display: flex; }
.marquee-track {
  display: flex;
  gap: 1.5rem;
  flex-shrink: 0;
  animation: uikeren-marquee 24s linear infinite;
}
.marquee-wrap:hover .marquee-track { animation-play-state: paused; }
@keyframes uikeren-marquee {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}
@media (prefers-reduced-motion: reduce) {
  .marquee-track { animation: none; }
}
```
