# Recorded JS Interaction Recipes

Reusable, framework-agnostic JavaScript + CSS mechanics **recorded from real
Playwright & source-bundle inspections** of `pos.efisien.id`,
`marsrejects.com`, and `discodungeongame.com`. Always guard motion with
`prefers-reduced-motion: reduce`.

---

## Recipe 1: Full-Bleed Hero -> Checkerboard Mosaic Morph (`pos.efisien.id`)
Starts as a `100vh` full-bleed stage (`1440px+` tall scroll runway), then
shrinks smoothly (`easeOutQuad`) into a checkerboard mosaic of `rounded-[20px]`
full-bleed tiles while a secondary display headline rises word-by-word.

```css
.hero-morph-runway { position: relative; min-height: 175vh; }
.hero-morph-sticky {
  position: sticky; top: 0; height: 100vh; overflow: hidden;
  display: grid; place-items: center;
}
.hero-primary-stage {
  position: absolute; inset: 0; z-index: 3;
  transform-origin: center center; will-change: transform, border-radius; overflow: hidden;
}
.mosaic-checkerboard {
  position: relative; z-index: 1; width: min(1180px, 94vw);
  display: grid; grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 1rem; align-items: center;
}
.mosaic-item {
  aspect-ratio: 1 / 1; border-radius: 20px; overflow: hidden;
  opacity: 0; transform: scale(0.25);
  transition: transform 520ms cubic-bezier(0.33, 1.53, 0.69, 0.99), opacity 380ms ease;
}
.mosaic-item.is-shown { opacity: 1; transform: scale(1); }
.mosaic-word {
  display: inline-block; opacity: 0; transform: translate3d(0, 90px, 0);
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
    stageEl.style.transform = `scale(${(1 - e * (1 - targetScale)).toFixed(4)})`;
    stageEl.style.borderRadius = `${(e * 24).toFixed(1)}px`;

    const showMosaic = raw > 0.36;
    items.forEach((el, i) => {
      el.style.transitionDelay = showMosaic ? `${(i % 5) * 55}ms` : '0ms';
      el.classList.toggle('is-shown', showMosaic);
    });
    const showWords = raw > 0.5;
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

## Recipe 2: Scroll Reveal, Clip-Path Wipe & Scrubbing (`pos.efisien.id`)
Exact recorded timings:
- `translate3d(0, 26px, 0)` -> `0` over `650ms cubic-bezier(0, 0, 0.2, 1)`
- Clip-path wipe (`[data-reveal="clip"]`): `inset(0% -4% 85% -4%)` -> `inset(-18% -4% -24% -4%)` over `700ms`
- Scrub parallax (`[data-scrub]`): `easeOutCubic` (`1 - (1 - t)^3`) mapped to `--scroll-p`.

```css
[data-reveal] {
  opacity: 0; transform: translate3d(0, 26px, 0);
  transition: opacity 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
              transform 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
              clip-path 700ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms);
  will-change: transform, opacity;
}
[data-reveal="clip"] { clip-path: inset(0% -4% 85% -4%); transform: translate3d(0, 22px, 0); }
[data-reveal].is-visible { opacity: 1; transform: translate3d(0, 0, 0); }
[data-reveal="clip"].is-visible { clip-path: inset(-18% -4% -24% -4%); }
[data-scrub] { transform: translate3d(0, calc((var(--scroll-p, 0.5) - 0.5) * -38px), 0); will-change: transform; }
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

## Recipe 3: Layered Text-Behind-Subject & Floating Bottom Dock (`marsrejects.com`)
Places monumental display type **behind** a foreground subject/visual layer
with subtle pointer parallax, paired with a compact floating bottom dock.

```css
.depth-hero {
  position: relative; min-height: 100vh; overflow: hidden;
  display: grid; place-items: end center;
}
.depth-hero-title {
  position: absolute; top: 14%; left: 50%; transform: translateX(-50%);
  z-index: 1; font-size: clamp(3.5rem, 11vw, 8.5rem); line-height: 0.84;
  text-align: center; pointer-events: none; user-select: none;
}
.depth-hero-subject {
  position: relative; z-index: 2; width: min(920px, 94vw);
  transition: transform 240ms cubic-bezier(0.12, 0.23, 0.5, 1);
}
.floating-dock {
  position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
  z-index: 50; display: inline-flex; align-items: center; gap: 0.5rem;
  padding: 0.45rem; border-radius: 999px; backdrop-filter: blur(14px);
}
```

---

## Recipe 4: Scroll-Spine Progress & `backOut` Micro-Physics (`discodungeongame.com`)
- Continuous central scroll-progress spine/indicator across sections
- `backOut` overshoot: `cubic-bezier(0.33, 1.53, 0.69, 0.99)` (`300ms`)
- Press feedback (`whileTap`): `scale(0.9)`

```css
.tactile-btn, .tactile-card {
  transition: transform 300ms cubic-bezier(0.33, 1.53, 0.69, 0.99),
              opacity 150ms cubic-bezier(0.12, 0.23, 0.5, 1);
}
.tactile-card:hover { transform: translateY(-4px); }
.tactile-btn:hover { opacity: 0.85; transform: translateY(-2px); }
.tactile-btn:active, .tactile-card:active { transform: scale(0.9); }
```

```js
export function initScrollSpine(spineEl, trackerEl) {
  if (!spineEl || !trackerEl) return;
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if (reduced) return;
  let ticking = false;
  const update = () => {
    const r = spineEl.getBoundingClientRect();
    const total = Math.max(1, spineEl.offsetHeight - window.innerHeight);
    const p = Math.min(1, Math.max(0, -r.top / total));
    trackerEl.style.transform = `translate3d(-50%, ${(p * (spineEl.offsetHeight - trackerEl.offsetHeight)).toFixed(1)}px, 0)`;
    ticking = false;
  };
  window.addEventListener('scroll', () => {
    if (!ticking) { ticking = true; requestAnimationFrame(update); }
  }, { passive: true });
  update();
}
```

---

## Recipe 5: Closing Cursor & Ambient Trail (`pos.efisien.id` `ClosingTrailSection`)
Pooled `8` nodes, `100ms ease-out` spawn, `1000ms cubic-bezier(0.16, 1, 0.3, 1)`
exit scaling to `0.2`, plus **ambient auto-spawn** after `2200ms` idle on desktop.

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
    const el = nodes[idx], { x, y } = coords[idx];
    el.style.transition = 'opacity 1000ms cubic-bezier(0.16, 1, 0.3, 1), transform 1000ms cubic-bezier(0.16, 1, 0.3, 1)';
    el.style.opacity = '0';
    el.style.transform = `translate3d(${x.toFixed(1)}px, ${y.toFixed(1)}px, 0) scale(0.2)`;
  };

  const spawn = (x, y) => {
    const idx = seq % POOL, el = nodes[idx];
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

## Recipe 6: Interactive Content Explorer & Full-Bleed Canvas Atmosphere
Use `initInteractiveTabs` for real product/menu/feature switchers, and
`initAmbientCanvas` whenever external photography is unavailable so every hero
or backdrop stays richly alive instead of blank.

```js
export function initInteractiveTabs({ tabSelector, panelSelector, onSwitch }) {
  const tabs = [...document.querySelectorAll(tabSelector)];
  const panels = [...document.querySelectorAll(panelSelector)];
  if (!tabs.length) return;
  const select = (targetId) => {
    tabs.forEach((t) => {
      const active = t.dataset.tab === targetId;
      t.classList.toggle('is-active', active);
      t.setAttribute('aria-selected', String(active));
    });
    panels.forEach((p) => {
      const active = p.dataset.panel === targetId;
      p.hidden = !active;
      p.classList.toggle('is-active', active);
    });
    if (onSwitch) onSwitch(targetId);
  };
  tabs.forEach((t) => t.addEventListener('click', () => select(t.dataset.tab)));
  select(tabs[0].dataset.tab);
}

export function initAmbientCanvas(canvas, colors = ['#0b1021', '#1b264f', '#ff5a36']) {
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
    grad.addColorStop(0, colors[2] + '66');
    grad.addColorStop(0.45, colors[1] + 'cc');
    grad.addColorStop(1, colors[0]);
    ctx.fillStyle = grad;
    ctx.fillRect(0, 0, w, h);
    if (!reduced) requestAnimationFrame(draw);
  };
  draw(0);
}
```
