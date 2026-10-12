# Plan Proyek: Clone W3Schools "How To"

Tugas Pemrograman Web: tiru tampilan https://www.w3schools.com/howto/default.asp semirip mungkin.
Kelompok 2 orang: **Anggota A = kamu (partner)**, **Anggota B = Zaki**.

---

## 1. Yang Wajib Ada
1. Navigasi atas (2 bar: bar putih + bar topik gelap)
2. Sidebar kiri
3. Iklan: **gambar** dan **video**
4. Semua demo konten (slideshow, accordion, dst) di dalam **iframe**. Pengecualian (keputusan Zaki): 6 demo popup (Login Form, Hover/Click Dropdowns, Side Navigation, Modal Box, Fullscreen Navigation) ditulis langsung di `index.html` + `css/howto-inline.css` agar popup menutupi seluruh halaman seperti asli
5. Section **Learn in Adventure Mode** dengan animasi buatan sendiri
6. Footer

## 2. Aturan Main (penting, jangan dilanggar)
1. **Hanya HTML + CSS.** Tidak boleh ada `<script>`, tidak boleh `onclick`/`onload`/dll.
2. **Link tidak pindah halaman.** Semua `<a>` di nav, sidebar, footer pakai `href="#!"`.
   Dropdown, menu, modal tetap harus bisa dibuka/ditutup pakai trik CSS (lihat bagian 6).
3. **Aset buatan sendiri** (logo, gambar iklan, video iklan, pixel-art). Jangan unduh aset asli W3Schools. Pengecualian atas permintaan Zaki: foto dan avatar di `assets/img/demos/` adalah screenshot gambar dari situs asli. Adventure Mode dan iklan tetap buatan sendiri.
4. Font **Source Sans Pro** (Google Fonts). Warna utama:

   | Nama | Hex | Dipakai di |
   |---|---|---|
   | Hijau | `#04AA6D` | logo, tombol Sign In, item aktif, pagination aktif |
   | Gelap | `#282A35` | bar topik, footer |
   | Sidebar | `#E7E9EB` | latar sidebar |
   | Abu konten | `#F1F1F1` | latar kotak demo |
   | Ungu | `#9763F6` | tombol Paid Courses |
   | Kuning footer | `#FFF4A3` | link baris atas footer |

## 3. Peta Halaman (hasil inspeksi DOM halaman asli)
```
header#top-nav-bar     putih, ±46px, sticky
  logo | Tutorials▾ References▾ Exercises▾ Certificates▾ | [Search...] ⋮ | Spaces Upgrade App(NEW) [Paid Courses] [Sign In]
nav#subtopnav          gelap, ±28px: HTML CSS JAVASCRIPT SQL PYTHON ... HOW TO(aktif) ... NODEJS
div.layout             grid 3 kolom
  aside#sidenav        ±240px, scroll sendiri, input Search + 13 grup
  main#main            iklan leaderboard, share bar, h1, pagination, intro, kotak demo (iframe), pagination
  aside#right          iklan gambar + iklan video + ikon sosmed + REMOVE ADS
section.advb           Learn in Adventure Mode (kartu progress + panggung animasi)
footer#footer          gelap: baris link kuning, 4 kolom link, sosmed, copyright
```
Grup sidebar: HOW TO, MENUS, IMAGES, BUTTONS, FORMS, FILTERS, TABLES, MORE, WEBSITE, GRID, GOOGLE, CONVERTERS, BLOG (cukup 8 sampai 15 link per grup).

Footer 4 kolom: Top Tutorials, Top References, Top Examples, Get Certified.

## 4. Pembagian Tugas

| **Anggota A (kamu): layout** | **Anggota B (Zaki): konten interaktif** |
|---|---|
| Setup repo GitHub + invite B | 22 kartu demo di `demos/*.html` (CSS murni) |
| Kerangka `index.html` + grid 3 kolom | Section Adventure Mode + animasi (`css/adventure.css`) |
| Top nav + panel menu (Tutorials dst) + bar topik | Memasang kartu demo + iframe ke `.howtocontainer` |
| Sidebar 13 grup + versi mobile | Uji semua interaksi CSS |
| Iklan: leaderboard, gambar kanan, video kanan (+ buat asetnya) | Review PR A |
| Share bar, pagination, footer | |
| Responsive, deploy GitHub Pages, README | |

**Kepemilikan file** (supaya tidak bentrok saat merge):
1. A: `index.html` (kecuali isi `.howtocontainer` dan `section.advb`), `css/style.css`, `assets/ads/`, `assets/img/` (logo, ikon).
2. B: `demos/`, `css/adventure.css`, `assets/img/adventure/`, isi `.howtocontainer`, isi `section.advb`.

## 5. Titik Sambung A dan B
A cukup menyiapkan wadah kosong ini di `index.html` dan style kartunya di `css/style.css`:

```html
<div class="howtocontainer">
  <!-- B mengisi kartu demo di sini -->
</div>

<section class="advb" id="adventure">
  <!-- B mengisi Adventure Mode di sini -->
</section>
```

Bentuk satu kartu demo (yang di-style A, diisi B):
```html
<div class="w3-card-4">
  <h2>Slideshow</h2>
  <iframe class="howto-iframe" src="demos/slideshow.html" title="Slideshow" loading="lazy"></iframe>
  <p class="howto-container"><a href="#!" class="howto-link">Learn how to create a Slideshow »</a></p>
</div>
```

## 6. Trik CSS Pengganti JavaScript (yang perlu A)
| Butuh | Cara |
|---|---|
| Panel menu Tutorials/References/Exercises/Certificates (klik buka, × tutup) | checkbox hack: `<input type="checkbox" id="m-tut" hidden>` + `<label for="m-tut">` + `#m-tut:checked ~ .tnb-panel { display:block }` |
| Dropdown hover | `:hover` dan `:focus-within` |
| Hamburger sidebar di HP | checkbox hack `#sidenav-toggle:checked ~ .layout #sidenav` |
| Iklan video | `<video src="assets/ads/iklan.mp4" autoplay muted loop playsinline></video>` (wajib `muted` agar autoplay) |
| Link tidak pindah halaman | `href="#!"` |

## 7. Jadwal
| Hari | A | B |
|---|---|---|
| 1 | Repo, kerangka `index.html`, grid, variabel warna | 3 demo pertama (Slideshow, Login Form, Accordion) |
| 2 sampai 3 | Top nav + panel, sidebar, footer, iklan | 20 demo sisanya |
| 4 | Responsive, share bar, pagination | Adventure Mode, pasang semua iframe |
| 5 | Bandingkan dengan situs asli, rapikan bersama, deploy, README | sama |

## 8. Alur GitHub
Repo: https://github.com/ZakiAndriansa/w3school-howto

**Setup awal sudah dikerjakan Zaki** (karena duluan online): repo, kerangka kosong `index.html`, design tokens + style kartu di `css/style.css`, dan semua branch. Isi layout tetap tugas A. Terima undangan Collaborator dari email GitHub, lalu:
```bash
git clone https://github.com/ZakiAndriansa/w3school-howto.git
cd w3school-howto
```

**Branch yang sudah tersedia:**
| Branch | Pemilik | Isi |
|---|---|---|
| `feat/topnav` | A | top nav, panel menu, bar topik |
| `feat/sidebar` | A | sidebar 13 grup + hamburger mobile |
| `feat/ads` | A | leaderboard, iklan gambar kanan, iklan video + aset |
| `feat/footer` | A | footer |
| `feat/page-extras` | A | share bar, pagination, intro, responsive akhir |
| `feat/demos-basic` | B | Slideshow, Login Form, Accordion |
| `feat/demos-nav` | B | Hover Dropdowns, Click Dropdowns, Side Navigation, Fixed Sidebar, Top Navigation, Responsive Top Navigation, Fullscreen Navigation, Login Form in Navbar |
| `feat/demos-modal-image` | B | Modal Box, Modal Image, Lightbox, Slideshow Gallery, Image Hover Overlay |
| `feat/demos-tabs-buttons` | B | Tabs, Vertical Tabs, Tab Image Gallery, Alert Buttons, Outline Buttons, Change Background on Scroll |
| `feat/adventure` | B | Learn in Adventure Mode + animasi |
| `feat/slideshow-images` | B | Gambar demo Slideshow dari screenshot situs asli |
| `feat/demo-images` | B | Semua gambar demo lain dari screenshot situs asli |

**Setiap mulai kerja di sebuah branch (A dan B):**
```bash
git checkout main
git pull origin main
git checkout feat/topnav             # branch milikmu
git merge main                       # ambil update terbaru dari main
# ... kerjakan ...
git add .
git commit -m "feat: top nav dan panel menu"
git push origin feat/topnav
```
Lalu buka **Pull Request** (`feat/topnav` → `main`) di GitHub, minta partner review, baru **Merge**.

Butuh perbaikan setelah merge? Buat branch baru dari `main`: `git checkout -b fix/sidebar-mobile`.

**Deploy:** Settings > Pages > Source: branch `main`, folder `/ (root)`.

## 9. Checklist Selesai
- [ ] Tidak ada `<script>` dan atribut `on...` di seluruh repo
- [ ] Semua link nav, sidebar, footer tidak pindah halaman
- [ ] Panel menu atas bisa dibuka dan ditutup tanpa JS
- [ ] Sidebar bisa di-scroll sendiri, collapse di HP
- [ ] Iklan gambar tampil, iklan video autoplay
- [ ] 22 kartu demo (iframe) ter-load, Console tanpa error 404
- [ ] Adventure Mode beranimasi
- [ ] Footer lengkap
- [ ] Rapi di lebar 375px, 768px, 1280px
- [ ] Riwayat commit dan PR ada dari kedua anggota
- [ ] Link GitHub Pages jalan

## 10. Pakai Claude Code?
Di root repo ada `CLAUDE.md`. Claude Code otomatis membacanya, jadi cukup buka folder repo lalu minta, misalnya:
> "Kerjakan top nav sesuai CLAUDE.md, aku Anggota A."
