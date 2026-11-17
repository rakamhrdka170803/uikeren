# UI Keren — Anti-Slop Interactive Web Plugin

Plugin Antigravity untuk membangun website dan landing page yang **anti-AI-slop**—memadukan *art direction* yang berkarakter dengan **elemen JS interaktif** yang direkam menjadi resep modular bersih (terinspirasi kualitas interaksi situs seperti `pos.efisien.id`, `marsrejects.com`, dan `discodungeongame.com`).

Berfungsi lintas bahasa prompt (Indonesia, Inggris, santai, formal) dan lintas tech stack (HTML/Vanilla JS, React, Next.js, Astro, Vue).

## Apa Itu "Anti-Slop"?
**AI Slop** adalah ciri khas website buatan AI yang terasa generik dan templated (misal: gradient ungu-biru neon di mana-mana, 3 kartu fitur simetris membosankan, hero standar tanpa karakter, copywriting klise, dan tombol mati).
**Anti-Slop** memastikan setiap web punya konsep visual sesuai topiknya, copywriting natural, dan elemen JS interaktif yang benar-benar bekerja.

## Instalasi

```bash
git clone https://github.com/rakamhrdka170803/uikeren.git
agy plugin validate --strict ./uikeren
agy plugin install ./uikeren
agy plugin list
```

Atau langsung taruh folder `uikeren/` ke dalam `.agents/plugins/uikeren/` di proyek kamu (atau `~/.gemini/config/plugins/uikeren/` untuk global).

## Cara Menguji (Testing)

Setelah plugin aktif, coba uji dengan beberapa prompt yang kontras:

1. **Kuliner / UMKM**: `"Buatkan web bapau kekinian dengan builder paket isi box dan keranjang pesan"`
2. **SaaS / Utility**: `"Buatkan landing page aplikasi POS kasir dengan simulator fitur interaktif"`
3. **Game / Kreatif**: `"Build an interactive retro puzzle RPG landing page with tactile cards"`

Pastikan hasilnya:
- Mengadaptasi tema sesuai domain (tidak menyalin tema situs referensi mentah-mentah).
- Memiliki minimal 2–4 elemen JS aktif dari `js-recipes.md` (mosaic morph, scroll motion, live switcher/builder, spring tactile cards, closing cursor trail, atau kinetic marquee).
- Responsif di mobile & desktop tanpa error di console.
