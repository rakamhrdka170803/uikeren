# Recorded JS Interaction Recipes (All 3 Reference Sites Balanced)

Reusable, framework-agnostic JavaScript + CSS recipes **recorded via
Playwright + source inspection** across ALL THREE reference sites equally—so
designs blend all three instead of copying `pos.efisien.id` every time.
Always guard motion with `prefers-reduced-motion: reduce`.

---

## Recipe 1: 3D Perspective Depth Hero & Expandable Bottom Pill (`marsrejects.com`)
Recorded `marsrejects.com` layout (`perspective: 1200px` -> `matrix3d` depth):
- **3 sandwiched Z-layers**: Rear subjects (`translateZ(-120px)`) -> Monumental
  Display Title (`translateZ(-40px)`) -> Foreground subjects (`translateZ(40px)`),
  reacting smoothly to pointer & scroll!
- **Expandable Bottom Menu Pill (`350x78` compact dock)**: Replaces bulky top
  headers with a sleek bottom pill that toggles open/closed.

```css
.depth-stage {
  position: relative; min-height: 100vh; overflow: hidden;
  perspective: 1200px; display: grid; place-items: center;
}
.depth-layer {
  position: absolute; inset: 0; display: grid; place-items: center;
  will-change: transform; transition: transform 180ms ease-out;
}
.depth-rear { z-index: 1; }
.depth-title { z-index: 2; pointer-events: none; text-align: center; }
.depth-front { z-index: 3; pointer-events: none; align-items: end; }
.bottom-pill-nav {
  position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
  z-index: 60; display: flex; align-items: center; gap: 0.45rem;
  padding: 0.45rem 0.65rem; border-radius: 999px;
  backdrop-filter: blur(14px);
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
      const tx = (nx * d * 28).toFixed(1);
      const ty = (ny * d * 18).toFixed(1);
      el.style.transform = `translate3d(${tx}px, ${ty}px, 0) scale(${1 + Math.abs(d) * 0.01})`;
    });
  });
  stageEl.addEventListener('pointerleave', () => {
    layers.forEach((el) => { el.style.transform = 'translate3d(0,0,0)'; });
  });
}
```

---

## Recipe 2: Screens Carousel + Radial Burst Features (`discodungeongame.com`)
Recorded directly from `discodungeongame.com`'s middle sections (so middle
sections are **visual & kinetic**, never dry `[text left | dark box right]`):
- **Horizontal Screens Carousel** (`Previous` / `Next` + dot pagination) with
  spring slide transitions and full-bleed `object-cover` showcase cards.
- **3D Radial Burst Cluster (`Power Section`)**: Feature cards/badges burst out
  from center (`scale(0.49) translate3d(...) -> scale(1) translate3d(0,0,0)`)
  when scrolled into view!

```css
.screens-viewport { overflow: hidden; width: 100%; }
.screens-track {
  display: flex; gap: 1.25rem;
  transition: transform 520ms cubic-bezier(0.33, 1.53, 0.69, 0.99);
}
.burst-item {
  opacity: 0;
  transform: translate3d(var(--bx, 0px), var(--by, 40px), 0) scale(0.49);
  transition: transform 680ms cubic-bezier(0.33, 1.53, 0.69, 0.99), opacity 420ms ease;
}
.burst-item.is-burst {
  opacity: 1;
  transform: translate3d(0, 0, 0) scale(1);
}
@media (prefers-reduced-motion: reduce) {
  .screens-track { transition: none; }
  .burst-item { opacity: 1; transform: none; transition: none; }
}
```

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
    const step = slides[0].getBoundingClientRect().width + 20;
    track.style.transform = `translate3d(${-(index * step)}px, 0, 0)`;
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
      el.style.transitionDelay = `${i * 70}ms`;
      el.classList.add('is-burst');
    });
    io.disconnect();
  }, { threshold: 0.2 });
  io.observe(containerEl);
}
```

---

## Recipe 3: Scroll-Spine Journey & `backOut` Micro-Physics (`discodungeongame.com`)
Continuous vertical guide/emblem moving down the page as you scroll, paired
with `backOut` (`cubic-bezier(0.33, 1.53, 0.69, 0.99)`) & `scale(0.9)` tap.

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

## Recipe 4: Full-Bleed Scroll-Morph & Clip-Path Reveal (`pos.efisien.id`)
Use when choosing the editorial photo-morph opening (`HeroMosaicMorph`) +
`650ms cubic-bezier(0, 0, 0.2, 1)` / `clip-path` wipe reveals (`ScrollMotion`).

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
```

---

## Recipe 5: Closing Cursor & Ambient Trail (`pos.efisien.id`)
Pooled `8` nodes (`100ms` spawn, `1000ms cubic-bezier(0.16, 1, 0.3, 1)` exit,
`2200ms` ambient auto-spawn). Always keep closing `h2` & CTA buttons at higher
`z-index` than trail stamps so stamps never cover button text.

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
