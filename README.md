# karashi — HTML / CSS / JavaScript portfolio

Portfolio satu-halaman dengan tema terminal + live hex-dump, dibangun murni
dengan HTML, CSS, dan JavaScript (tanpa TypeScript, tanpa build step, tanpa
framework). Tinggal buka `index.html` di browser — selesai.

## Struktur

- `index.html` — shell halaman utama, cuma memuat `style.css` dan `script.js`.
- `style.css` — semua styling: tema terminal + hex-dump di homepage, dan
  styling khusus halaman writeup (prefix class `.wr-*`) di bagian bawah file.
- `script.js` — semua data + logika render homepage dalam satu file, dibagi
  jadi 5 bagian yang ditandai komentar:
  1. **DATA** — edit di sini untuk ganti nama, bio, daftar writeup, tools, timeline.
  2. **DOM HELPERS** — fungsi bantu kecil.
  3. **TYPEWRITER** — efek mengetik di terminal hero.
  4. **HEX DUMP** — panel hex-dump animasi (elemen signature halaman).
  5. **SECTION RENDERERS** — fungsi yang mengubah data jadi HTML per section.
- `writeups/itechnocup2026.html` — halaman writeup lengkap, ditulis manual
  jadi HTML statis (bukan link ke PDF). Card writeup di homepage sudah
  diarahkan ke file ini lewat `href` di `script.js`.

## Menjalankan

Cukup buka `index.html` langsung di browser. Kalau browser memblokir
`fetch`/font loading dari file lokal, serve saja dengan server statis apa pun:

```bash
npx serve .
# atau
python3 -m http.server 8080
```

## Kustomisasi cepat

1. Buka `script.js`, edit bagian **DATA** di paling atas (`profile`, `writeups`,
   `tools`, `timeline`).
2. Tiap entri di `writeups` otomatis jadi satu card. `level` (`"info"` /
   `"warn"` / `"crit"`) mengatur warna badge di title bar card.
3. Set `href` tiap writeup ke halaman writeup asli (lihat bagian di bawah)
   atau ke link eksternal begitu sudah online.
4. Mau ganti warna aksen? Edit variabel di `:root` pada `style.css`
   (`--mint`, `--amber`, `--red`, `--bg`).
5. Simpan, refresh browser — tidak perlu compile apa pun.

## Menambah writeup baru sebagai halaman (bukan PDF)

1. Copy `writeups/itechnocup2026.html` jadi file baru, misal `writeups/nama-ctf.html`.
2. Ganti isi `<title>`, header (`wr-title`, `wr-meta`), daftar isi (`wr-toc`),
   dan tiap section `<article class="wr-chal">` sesuai writeup baru.
3. Blok terminal output pakai `<div class="wr-term">...<pre>...</pre></div>`,
   blok kode pakai `<div class="wr-code">...<pre>...</pre></div>`, dan flag
   pakai `<div class="wr-flag">...</div>` — semua style-nya sudah ada di
   `style.css`, tinggal isi kontennya.
4. Di `script.js`, tambah satu entri baru di array `writeups` dengan
   `href: "writeups/nama-ctf.html"`.

## Deploy

Karena tidak ada build step, folder ini bisa langsung di-upload ke GitHub
Pages, Netlify, Vercel, atau hosting statis mana pun apa adanya.
