# Recorded JS Interaction Recipes

Reusable, framework-agnostic JavaScript + CSS interaction mechanics **recorded
from the real production code of the three reference sites**:
- `pos.efisien.id` (`HeroMosaicMorph`, `ScrollMotion`, `LandingInteractive`,
  `ClosingTrailSection`)
- `marsrejects.com` (snappy `50ms–300ms` curves & `whileTap: scale(0.9)`)
- `discodungeongame.com` (`backOut` overshoot, `{stiffness: 400, damping: 30}`,
  looping emblem rotators)

Always guard animations with `prefers-reduced-motion: reduce`.

---

## Recipe 1: Full-Bleed Hero -> Checkerboard Mosaic Morph (from `pos.efisien.id` `HeroMosaicMorph`)
Starts as a **full-bleed `100vh` hero**, then on scroll smoothly shrinks and
docks into a checkerboard mosaic (`easeOutQuad` + `easeInCirc`) while revealing
a word-by-word rising display headline (`translate3d(0, 160px, 0) -> 0`).

```css
.hero-morph-runway {
  position: relative;
  min-height: 185vh;
}
.hero-morph-sticky {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
  display: grid;
  place-items: center;
}
.hero-primary-stage {
  position: absolute;
  inset: 0;
  z-index: 3;
  transform-origin: center center;
  will-change: transform, border-radius;
  overflow: hidden;
}
.mosaic-checkerboard {
  position: relative;
  z-index: 1;
  width: min(1180px, 94vw);
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 1rem;
  align-items: center;
}
.mosaic-item {
  aspect-ratio: 1 / 1;
  border-radius: 20px;
  overflow: hidden;
  opacity: 0;
  transform: scale(0.25);
  transition: transform 520ms cubic-bezier(0.33, 1.53, 0.69, 0.99), opacity 380ms ease;
}
.mosaic-item.is-shown { opacity: 1; transform: scale(1); }
.mosaic-word {
  display: inline-block;
  opacity: 0;
  transform: translate3d(0, 90px, 0);
  transition: transform 650ms cubic-bezier(0, 0, 0.2, 1), opacity 550ms ease;
}
.mosaic-word.is-shown { opacity: 1; transform: translate3d(0, 0, 0); }
@media (prefers-reduced-motion: reduce) {
  .hero-primary-stage, .mosaic-item, .mosaic-word {
    transform: none !important; opacity: 1 !important; transition: none !important;
  }
}
```

```js
export function initHeroMosaicMorph(runwayEl, stageEl, dockEl) {
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const items = [...runwayEl.querySelectorAll('.mosaic-item')];
  const words = [...runwayEl.querySelectorAll('.mosaic-word')];
  if (reduced) {
    items.forEach((el) => el.classList.add('is-shown'));
    words.forEach((el) => el.classList.add('is-shown'));
    return;
  }

  const clamp01 = (n) => (n < 0 ? 0 : n > 1 ? 1 : n);
  const easeOutQuad = (t) => 1 - (1 - t) * (1 - t);
  let ticking = false;

  const render = () => {
    const rect = runwayEl.getBoundingClientRect();
    const scrollable = Math.max(1, runwayEl.offsetHeight - window.innerHeight);
    const raw = clamp01(-rect.top / scrollable);
    const e = easeOutQuad(raw);

    const targetScale = dockEl ? Math.max(0.18, dockEl.offsetWidth / Math.max(1, window.innerWidth)) : 0.22;
    const scale = 1 - e * (1 - targetScale);
    const radius = e * 24;
    stageEl.style.transform = `scale(${scale.toFixed(4)})`;
    stageEl.style.borderRadius = `${radius.toFixed(1)}px`;

    const showMosaic = raw > 0.38;
    items.forEach((el, i) => {
      el.style.transitionDelay = showMosaic ? `${(i % 5) * 55}ms` : '0ms';
      el.classList.toggle('is-shown', showMosaic);
    });
    const showWords = raw > 0.52;
    words.forEach((el, i) => {
      el.style.transitionDelay = showWords ? `${i * 45}ms` : '0ms';
      el.classList.toggle('is-shown', showWords);
    });
    ticking = false;
  };

  window.addEventListener('scroll', () => {
    if (!ticking) { ticking = true; requestAnimationFrame(render); }
  }, { passive: true });
  render();
}
```

---

## Recipe 2: Scroll Reveal, Clip-Path Wipe & Scrubbing (from `pos.efisien.id` `ScrollMotion`)
Exact recorded timings:
- Standard reveal: `translate3d(0, 26px, 0)` -> `0` over `650ms cubic-bezier(0, 0, 0.2, 1)`
- Clip-path wipe (`[data-reveal="clip"]`): `clip-path: inset(0% -4% 85% -4%)` -> `inset(-18% -4% -24% -4%)` over `700ms`
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
[data-reveal].is-visible { opacity: 1; transform: translate3d(0, 0, 0); }
[data-reveal="clip"].is-visible { clip-path: inset(-18% -4% -24% -4%); }
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
  if (reduced) { reveals.forEach((el) => el.classList.add('is-visible')); return; }

  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) { entry.target.classList.add('is-visible'); io.unobserve(entry.target); }
    });
  }, { threshold: 0, rootMargin: '0px 0px -24px 0px' });

  reveals.forEach((el, idx) => {
    if (!el.style.getPropertyValue('--stagger')) el.style.setProperty('--stagger', `${(idx % 4) * 75}ms`);
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
Pooled `8` recycled nodes, `100ms ease-out` spawn, `1000ms cubic-bezier(0.16, 1, 0.3, 1)` exit scaling to `0.2`, plus **ambient auto-spawn** after `2200ms` idle when in view on desktop (`>= 768px`). Use crisp photo thumbnails or custom badge elements (not plain tiny text only).

```js
export function initClosingTrail(sectionEl, renderItem) {
  if (!sectionEl || typeof renderItem !== 'function') return;
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;

  const POOL = 8;
  const nodes = Array.from({ length: POOL }, (_, i) => {
    const el = renderItem(i);
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
    el.style.transition = 'none';
    el.style.zIndex = String(10 + (seq % 100));
    el.style.opacity = '0';
    el.style.transform = `translate3d(${x.toFixed(1)}px, ${y.toFixed(1)}px, 0) scale(1)`;
    el.offsetWidth;
    el.style.transition = 'opacity 100ms ease-out';
    el.style.opacity = '1';
    if (seq >= 4) retire((seq - 4 + POOL) % POOL);
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

## Recipe 4: Framer `backOut` Overshoot & `whileTap` Physics (from `marsrejects.com` & `discodungeongame.com`)
- `backOut` overshoot: `cubic-bezier(0.33, 1.53, 0.69, 0.99)` (`300ms`)
- Fast snap ease: `cubic-bezier(0.12, 0.23, 0.5, 1)` (`150ms`)
- Press feedback (`whileTap`): `scale(0.9)`
- Continuous emblem spin: `2s linear infinite`

```css
.tactile-btn,
.tactile-card {
  transition: transform 300ms cubic-bezier(0.33, 1.53, 0.69, 0.99),
              opacity 150ms cubic-bezier(0.12, 0.23, 0.5, 1),
              box-shadow 200ms ease;
}
.tactile-card:hover { transform: translateY(-4px); }
.tactile-btn:hover { opacity: 0.85; transform: translateY(-2px); }
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
Stateful switcher/builder/drawer with live DOM updates and `aria-selected` accessibility.

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

## Recipe 6: Full-Bleed Canvas Atmosphere (Fallback when No External Images Exist)
When building a standalone site without photographic assets, render a rich
pointer-reactive HTML5 `<canvas>` backdrop (ambient light fields, floating
particles, CRT/grid depth, or fluid color washes) instead of leaving blank
surfaces or relying on tiny inline SVG icons.

```js
export function initAmbientCanvas(canvas, colors = ['#0f172a', '#1e293b', '#f97316']) {
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  let w = 0, h = 0, mx = 0.5, my = 0.5;

  const resize = () => {
    const dpr = Math.min(2, window.devicePixelRatio || 1);
    w = canvas.clientWidth; h = canvas.clientHeight;
    canvas.width = w * dpr; canvas.height = h * dpr;
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
  };
  resize();
  window.addEventListener('resize', resize);
  canvas.addEventListener('pointermove', (e) => {
    const r = canvas.getBoundingClientRect();
    mx = (e.clientX - r.left) / Math.max(1, r.width);
    my = (e.clientY - r.top) / Math.max(1, r.height);
  });

  const draw = (t = 0) => {
    ctx.fillStyle = colors[0];
    ctx.fillRect(0, 0, w, h);
    const gx = w * (0.35 + mx * 0.3 + Math.sin(t * 0.0007) * 0.08);
    const gy = h * (0.35 + my * 0.3 + Math.cos(t * 0.0005) * 0.08);
    const grad = ctx.createRadialGradient(gx, gy, 20, gx, gy, Math.max(w, h) * 0.72);
    grad.addColorStop(0, colors[2] + '55');
    grad.addColorStop(0.45, colors[1] + 'cc');
    grad.addColorStop(1, colors[0]);
    ctx.fillStyle = grad;
    ctx.fillRect(0, 0, w, h);
    if (!reduced) requestAnimationFrame(draw);
  };
  draw(0);
}
```
