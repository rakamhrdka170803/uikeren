---
name: uikeren-motion
description: >-
  Playwright-recorded JS and CSS interaction recipes for UI Keren, extracted
  from marsrejects.com, discodungeongame.com, and pos.efisien.id (3D Z-depth
  parallax, collapsible bottom menu trigger, radial burst clusters, screens
  carousel, scroll-spine, clip-path reveals, and safe-zone cursor trail).
---

# UI Keren — Recorded JS Motion Recipes

Use with `uikeren/SKILL.md`. Lead with **`marsrejects.com`** and
**`discodungeongame.com`** mechanics just as often as `pos.efisien.id`, so
builds never look like `pos.efisien.id` clones. Always guard animations with
`prefers-reduced-motion: reduce`.

---

## 1. 3D Z-Depth Sandwiched Hero & Compact Expandable Trigger (`marsrejects.com`)
Recorded from `marsrejects.com` (`perspective: 1200px`, 3 sandwiched Z-layers,
`rotate(±1deg)` caption stickers with `0 10px 16px -4px rgba(0,0,0,0.32)`, and
a compact circular `menu / close` trigger instead of a wide blocking bar):

```css
.depth-stage {
  position: relative; min-height: 92dvh; overflow: hidden;
  perspective: 1200px; display: grid; place-items: center;
}
.depth-layer {
  position: absolute; inset: 0; display: grid; place-items: center;
  will-change: transform; transition: transform 200ms cubic-bezier(0.12, 0.23, 0.5, 1);
}
.depth-rear { z-index: 1; }
.depth-title { z-index: 2; pointer-events: none; text-align: center; }
.depth-front { z-index: 3; pointer-events: none; align-items: end; }
.tilted-sticker {
  transform: rotate(var(--tilt, -1.2deg));
  box-shadow: 0 2px 4px -1px rgba(0,0,0,0.25), 0 10px 16px -4px rgba(0,0,0,0.32);
}
.compact-dock-btn {
  position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
  z-index: 60; width: 54px; height: 54px; border-radius: 999px;
}
```

```js
export function initDepthHero(stageEl) {
  if (!stageEl || window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
  const layers = [...stageEl.querySelectorAll('[data-depth]')];
  stageEl.addEventListener('pointermove', (e) => {
    const r = stageEl.getBoundingClientRect();
    const nx = (e.clientX - r.left) / Math.max(1, r.width) - 0.5;
    const ny = (e.clientY - r.top) / Math.max(1, r.height) - 0.5;
    layers.forEach((el) => {
      const d = Number(el.dataset.depth || 1);
      el.style.transform = `translate3d(${(nx * d * 28).toFixed(1)}px, ${(ny * d * 18).toFixed(1)}px, 0)`;
    });
  });
  stageEl.addEventListener('pointerleave', () => {
    layers.forEach((el) => { el.style.transform = 'translate3d(0,0,0)'; });
  });
}
```

---

## 2. 3D Radial Burst Cluster (`discodungeongame.com`)
Cards/badges burst outward from center in organic staggered positions
(`scale(0.49) -> scale(1)` with `backOut` overshoot) instead of flat 2x3 grids.

```css
.burst-cluster { position: relative; display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 1.25rem; }
.burst-item {
  opacity: 0;
  transform: translate3d(var(--bx, -40px), var(--by, 48px), 0) scale(0.49);
  transition: transform 680ms cubic-bezier(0.33, 1.53, 0.69, 0.99), opacity 420ms ease;
}
.burst-item:nth-child(even) { transform: translateY(24px) translate3d(var(--bx, 40px), var(--by, 48px), 0) scale(0.49); }
.burst-item.is-burst { opacity: 1; transform: translate3d(0, 0, 0) scale(1); }
.burst-item.is-burst:nth-child(even) { transform: translateY(24px) scale(1); }
@media (max-width: 767px) { .burst-item.is-burst:nth-child(even) { transform: scale(1); } }
@media (prefers-reduced-motion: reduce) { .burst-item { opacity: 1; transform: none !important; transition: none; } }
```

```js
export function initRadialBurst(containerEl) {
  if (!containerEl) return;
  const items = [...containerEl.querySelectorAll('.burst-item')];
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    items.forEach((el) => el.classList.add('is-burst'));
    return;
  }
  const io = new IntersectionObserver(([entry]) => {
    if (!entry.isIntersecting) return;
    items.forEach((el, i) => {
      el.style.transitionDelay = `${i * 75}ms`;
      el.classList.add('is-burst');
    });
    io.disconnect();
  }, { threshold: 0.18 });
  io.observe(containerEl);
}
```

---

## 3. Horizontal Screens Carousel (`discodungeongame.com`)
Interactive Prev/Next + pagination dot slider with `backOut` spring glide.

```js
export function initScreensCarousel(rootEl) {
  if (!rootEl) return;
  const track = rootEl.querySelector('.screens-track');
  const slides = [...rootEl.querySelectorAll('.screen-slide')];
  const prev = rootEl.querySelector('[data-prev]');
  const next = rootEl.querySelector('[data-next]');
  const dots = [...rootEl.querySelectorAll('[data-dot]')];
  if (!track || !slides.length) return;

  let index = 0;
  const go = (i) => {
    index = (i + slides.length) % slides.length;
    const gap = parseFloat(getComputedStyle(track).gap || '20') || 20;
    const step = slides[0].getBoundingClientRect().width + gap;
    track.style.transform = `translate3d(${-(index * step).toFixed(1)}px, 0, 0)`;
    dots.forEach((d, di) => {
      d.classList.toggle('is-active', di === index);
      d.setAttribute('aria-current', di === index ? 'true' : 'false');
    });
  };
  prev?.addEventListener('click', () => go(index - 1));
  next?.addEventListener('click', () => go(index + 1));
  dots.forEach((d, di) => d.addEventListener('click', () => go(di)));
  window.addEventListener('resize', () => go(index));
  go(0);
}
```

---

## 4. Scroll-Spine & `backOut` Micro-Physics (`discodungeongame.com`)
```css
.tactile-btn, .tactile-card {
  transition: transform 300ms cubic-bezier(0.33, 1.53, 0.69, 0.99),
              opacity 150ms cubic-bezier(0.12, 0.23, 0.5, 1);
}
.tactile-btn:hover { opacity: 0.86; transform: translateY(-2px); }
.tactile-btn:active, .tactile-card:active { transform: scale(0.9); }
```

```js
export function initScrollSpine(spineEl, trackerEl) {
  if (!spineEl || !trackerEl) return;
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
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

## 5. Clip-Path Reveals & Optional Safe-Zone Trail (`pos.efisien.id`)
Use `initScrollMotion` across bands, and use `initClosingTrail` **only as one
optional closing choice** (never default to it on every site). When used,
keep a safe-zone clear around the central `h2`/paragraph/buttons so stamps
never overlap readable copy!

```css
[data-reveal] {
  opacity: 0; transform: translate3d(0, 26px, 0);
  transition: opacity 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
              transform 650ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms),
              clip-path 700ms cubic-bezier(0, 0, 0.2, 1) var(--stagger, 0ms);
}
[data-reveal="clip"] { clip-path: inset(0% -4% 85% -4%); transform: translate3d(0, 22px, 0); }
[data-reveal].is-visible { opacity: 1; transform: translate3d(0, 0, 0); }
[data-reveal="clip"].is-visible { clip-path: inset(-18% -4% -24% -4%); }
@media (prefers-reduced-motion: reduce) {
  [data-reveal] { opacity: 1 !important; transform: none !important; clip-path: none !important; transition: none !important; }
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
}

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
    // Skip central text/CTA safe-zone so trail stamps stay on the flanks
    if (x > r.width * 0.24 && x < r.width * 0.76 && y > r.height * 0.18 && y < r.height * 0.82) return;
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
    const leftSide = Math.random() < 0.5;
    const x = leftSide ? r.width * (0.08 + Math.random() * 0.14) : r.width * (0.78 + Math.random() * 0.14);
    spawn(x, r.height * (0.2 + Math.random() * 0.6));
  }, 950);
}
```
