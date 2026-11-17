# UI Keren — Anti-Slop Interactive Web Plugin

Plugin Antigravity modular untuk membangun website & landing page yang
**anti-AI-slop**, memadukan arsitektur penegakan anti-slop (Liveliness Dials,
Written Purpose-Gate, AI Tell Detector, & PASS/FAIL Delivery Gate) dengan
**resep JS & layout hasil rekaman Playwright** dari `marsrejects.com`,
`discodungeongame.com`, dan `pos.efisien.id`.

## Skill di Dalam Plugin (`4` Skill Terintegrasi)
- **`uikeren`** — Core engine, Liveliness Dials (`ENERGY/RHYTHM/MOTION`), kewajiban
  gambar asli (`image-generator`), dan `PASS/FAIL` Delivery Gate.
- **`uikeren-ui`** — Detektor *AI tells* konkret (pill dot di atas H1, kartu 2x3
  kembar, garis grid latar, SVG datar pengganti foto, dock bertabrakan) tanpa
  melarang palet warna apa pun.
- **`uikeren-motion`** — Resep JS/CSS rekaman Playwright dari ketiga situs
  referensi (`initDepthHero`, `initRadialBurst`, `initScreensCarousel`,
  `initScrollSpine`, `initScrollMotion`, `initClosingTrail`).
- **`uikeren-layoutmobile`** — Reflow responsif mobile–tablet–desktop, target
  sentuh `>= 44px`, dan nol overlap.

## Instalasi & Update

```bash
agy plugin install https://github.com/rakamhrdka170803/uikeren
agy plugin list
```

Untuk update ke versi terbaru:

```bash
agy plugin uninstall uikeren
agy plugin install https://github.com/rakamhrdka170803/uikeren
```

## Cara Pakai & Test

Buka folder proyek baru, jalankan `agy`, lalu ketik prompt singkat dalam bahasa
apa pun:
- `"Buatkan web bapau pakai uikeren"`
- `"Buatkan web kedai kopi & slow bar pakai uikeren"`
- `"Build an interactive indie game site using uikeren"`
