# Recorded JS Interaction Recipes

Reusable, framework-agnostic JavaScript + CSS interaction mechanics **recorded
and distilled from the real production JS/CSS of the three reference sites**:
- `pos.efisien.id` (Astro Islands: `HeroMosaicMorph`, `ScrollMotion`,
  `LandingInteractive`, `ClosingTrailSection`)
- `marsrejects.com` (Framer motion curves & `whileTap` tactile states)
- `discodungeongame.com` (Framer spring physics, `backOut` overshoot, loop rotators)

Adapt colors, copy, and assets to the user's domain—keep the extracted motion
physics, timing curves, and real JS state intact. Always guard animations with
`prefers-reduced-motion: reduce`.

---

## Recipe 1: Scroll-Linked Hero Mosaic Morph (from `pos.efisien.id` `HeroMosaicMorph`)
Scroll-driven hero-to-mosaic scale/translate morph using `easeOutQuad`
(`1 - (1 - t)^2`) and `easeInCirc` (`1 - Math.sqrt(1 - t * t)`), plus
`IntersectionObserver` pausing offscreen background video (`saveData`-aware).

```css
.hero-morph-stage {
  position: relative;
  min-height: 92vh;
  overflow: hidden;
}
.hero-morph-frame {
  transform-origin: center top;
  will-change: transform;
}
.mosaic-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.75rem;
}
.mosaic-tile {
  border-radius: 1rem;
  overflow: hidden;
  transition: transform 420ms cubic-bezier(0.33, 1.53, 0.69, 0.99), opacity 300ms ease;
}
.mosaic-tile.is-featured { transform: scale(1.04) translateY(-4px); z-index: 2; }
@media (prefers-reduced-motion: reduce) {
  .hero-morph-frame, .mosaic-tile { transform: none !important; transition: none; }
}
```

```js
export function initHeroMosaicMorph(stageEl, frameEl, tilesSelector = '.mosaic-tile') {
  const tiles = [...stageEl.querySelectorAll(tilesSelector)];
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const clamp01 = (n) => (n < 0 ? 0 : n > 1 ? 1 : n);
  const easeOutQuad = (t) => 1 - (1 - t) * (1 - t);

  if (!reduced && frameEl) {
    const scrollEnd = 342;
    let ticking = false;
    const render = () => {
      const p = clamp01((window.scrollY || 0) / scrollEnd);
      const e = easeOutQuad(p);
      const scale = 1 - e * 0.14;
      const ty = e * 28;
      frameEl.style.transform = `translate3d(0, ${ty.toFixed(2)}px, 0) scale(${scale.toFixed(4)})`;
      ticking = false;
    };
    window.addEventListener('scroll', () => {
      if (!ticking) { ticking = true; requestAnimationFrame(render); }
    }, { passive: true });
    render();
  }

  if (!tiles.length) return;
  let active = 0;
  const setActive = (i) => tiles.forEach((t, idx) => t.classList.toggle('is-featured', idx === i));
  setActive(0);
  if (reduced) return;

  let timer = setInterval(() => { active = (active + 1) % tiles.length; setActive(active); }, 2600);
  tiles.forEach((tile, idx) => {
    tile.addEventListener('mouseenter', () => {
      clearInterval(timer);
      active = idx;
      setActive(idx);
    });
  });
}
```

---

## Recipe 2: Scroll Reveal, Clip-Path Wipe & Scrubbing (from `pos.efisien.id` `ScrollMotion`)
Exact recorded timings:
- Standard reveal: `translate3d(0, 26px, 0)` -> `0` over `650ms cubic-bezier(0, 0, 0.2, 1)`
- Clip-path wipe (`[data-reveal="clip"]`): `inset(0% -4% 85% -4%)` + `translate3d(0, 22px, 0)` -> `inset(-18% -4% -24% -4%)` over `700ms cubic-bezier(0, 0, 0.2, 1)`
- Scrub parallax (`[data-scrub]`): `easeOutCubic` (`1 - (1 - t)^3`) mapped to `--scroll-p`.

```css
[data-reveal] {
  opacity: 0;
  transform: translate3d(0, 26px, 0);
  transition:
    opacity 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
    transform 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
    clip-path 700ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms);
  will-change: transform, opacity;
}
[data-reveal="clip"] {
  clip-path: inset(0% -4% 85% -4%);
  transform: translate3d(0, 22px, 0);
}
[data-reveal].is-visible {
  opacity: 1;
  transform: translate3d(0, 0, 0);
}
[data-reveal="clip"].is-visible {
  clip-path: inset(-18% -4% -24% -4%);
}
[data-scrub] {
  transform: translate3d(0, calc((var(--scroll-p, 0.5) - 0.5) * -38px), 0);
  will-change: transform;
}
@media (prefers-reduced-motion: reduce) {
  [data-reveal] { opacity: 1 !important; transform: none !important; clip-path: none !important; transition: none !important; }
  [data-scrub] { transform: none !important; }
}
```

```js
export function initScrollMotion() {
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const reveals = [...document.querySelectorAll('[data-reveal]')];
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
  }, { threshold: 0, rootMargin: '0px 0px -24px 0px' });

  reveals.forEach((el, idx) => {
    if (!el.style.getPropertyValue('--stagger')) {
      el.style.setProperty('--stagger', `${(idx % 4) * 75}ms`);
    }
    io.observe(el);
  });

  const scrubs = [...document.querySelectorAll('[data-scrub]')];
  if (!scrubs.length) return;
  const easeOutCubic = (t) => 1 - Math.pow(1 - t, 3);
  let ticking = false;
  const update = () => {
    const vh = window.innerHeight || 800;
    scrubs.forEach((el) => {
      const r = el.getBoundingClientRect();
      const raw = Math.min(1, Math.max(0, (vh - r.top) / (vh + r.height)));
      el.style.setProperty('--scroll-p', easeOutCubic(raw).toFixed(4));
    });
    ticking = false;
  };
  window.addEventListener('scroll', () => {
    if (!ticking) { ticking = true; requestAnimationFrame(update); }
  }, { passive: true });
  update();
}
```

---

## Recipe 3: Closing Cursor & Ambient Trail (from `pos.efisien.id` `ClosingTrailSection`)
Exact recorded pool & timing mechanics:
- Pooled `8` recycled nodes (`O = 8`)
- Spawn fade-in `100ms ease-out`, exit fade-out `1000ms cubic-bezier(0.16, 1, 0.3, 1)` scaling down to `scale(0.2)`
- **Ambient auto-spawn** after `2200ms` of pointer idle while section is in view on desktop (`>= 768px`).

```js
export function initClosingTrail(sectionEl, labels = []) {
  if (!sectionEl || !labels.length) return;
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;

  const POOL = 8;
  const nodes = Array.from({ length: POOL }, (_, i) => {
    const el = document.createElement('span');
    el.className = 'trail-item';
    el.textContent = labels[i % labels.length];
    Object.assign(el.style, {
      position: 'absolute', left: '0', top: '0', opacity: '0',
      pointerEvents: 'none', willChange: 'transform, opacity', zIndex: '1'
    });
    sectionEl.appendChild(el);
    return el;
  });

  sectionEl.style.position = 'relative';
  sectionEl.style.overflow = 'hidden';

  let seq = 0, lastX = 0, lastY = 0, hasPoint = false, lastMoveAt = Date.now(), inView = false;
  const coords = Array.from({ length: POOL }, () => ({ x: 0, y: 0 }));

  const retire = (idx) => {
    const el = nodes[idx];
    const { x, y } = coords[idx];
    el.style.transition = 'opacity 1000ms cubic-bezier(0.16, 1, 0.3, 1), transform 1000ms cubic-bezier(0.16, 1, 0.3, 1)';
    el.style.opacity = '0';
    el.style.transform = `translate3d(${x.toFixed(1)}px, ${y.toFixed(1)}px, 0) scale(0.2)`;
  };

  const spawn = (x, y) => {
    const idx = seq % POOL;
    const el = nodes[idx];
    coords[idx] = { x, y };
    el.textContent = labels[seq % labels.length];
    el.style.transition = 'none';
    el.style.zIndex = String(10 + (seq % 100));
    el.style.opacity = '0';
    el.style.transform = `translate3d(${x.toFixed(1)}px, ${y.toFixed(1)}px, 0) scale(1)`;
    el.offsetWidth;
    el.style.transition = 'opacity 100ms ease-out';
    el.style.opacity = '1';
    const oldIdx = (seq - 4 + POOL) % POOL;
    if (seq >= 4) retire(oldIdx);
    seq++;
  };

  sectionEl.addEventListener('pointermove', (e) => {
    const r = sectionEl.getBoundingClientRect();
    const x = e.clientX - r.left, y = e.clientY - r.top;
    lastMoveAt = Date.now();
    if (!hasPoint || Math.hypot(x - lastX, y - lastY) >= 72) {
      hasPoint = true; lastX = x; lastY = y;
      spawn(x, y);
    }
  });

  const io = new IntersectionObserver(([entry]) => { inView = entry.isIntersecting; }, { threshold: 0.2 });
  io.observe(sectionEl);

  setInterval(() => {
    if (!inView || window.innerWidth < 768 || Date.now() - lastMoveAt < 2200) return;
    const r = sectionEl.getBoundingClientRect();
    spawn(r.width * (0.18 + Math.random() * 0.64), r.height * (0.22 + Math.random() * 0.56));
  }, 950);
}
```

---

## Recipe 4: Framer Spring Tactile Press & `backOut` Overshoot (from `marsrejects.com` & `discodungeongame.com`)
Exact recorded Framer curves and tap/hover responses:
- `backOut` overshoot: `cubic-bezier(0.33, 1.53, 0.69, 0.99)` (`300ms`)
- Fast snap ease: `cubic-bezier(0.12, 0.23, 0.5, 1)` (`150ms–200ms`)
- Press feedback (`whileTap`): `scale(0.9)`
- Continuous kinetic badge/emblem spin: `2s linear infinite` (pauses under reduced motion)

```css
.tactile-btn,
.tactile-card {
  transition: transform 300ms cubic-bezier(0.33, 1.53, 0.69, 0.99),
              opacity 150ms cubic-bezier(0.12, 0.23, 0.5, 1),
              box-shadow 200ms ease;
}
.tactile-card:hover { transform: translateY(-4px) rotate(var(--tilt, -0.8deg)); }
.tactile-btn:hover { opacity: 0.88; transform: translateY(-2px); }
.tactile-btn:active,
.tactile-card:active { transform: scale(0.9); }

.spin-badge { animation: uikeren-spin 2s linear infinite; }
@keyframes uikeren-spin { to { transform: rotate(360deg); } }
@media (prefers-reduced-motion: reduce) {
  .tactile-btn, .tactile-card { transition: none; transform: none !important; }
  .spin-badge { animation: none; }
}
```

---

## Recipe 5: Interactive Content Explorer & Live Builder (`LandingInteractive` pattern)
Replaces static feature grids with a stateful switcher/customizer (e.g., POS
module tabs, bakpao flavor box builder + slide-over cart drawer, or game unit
inspector) with real DOM state and `aria-selected` accessibility.

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

  tabs.forEach((tab) => tab.addEventListener('click', () => select(tab.dataset.tab)));
  select(tabs[0].dataset.tab);
}
```

---

## Recipe 6: Kinetic Dual-Track Marquee
GPU-accelerated infinite horizontal strip for slogans, flavors, or tags—pauses
on hover and disables automatically under `prefers-reduced-motion`.

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
