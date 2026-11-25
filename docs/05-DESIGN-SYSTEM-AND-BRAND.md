# Identitas Brand & Sistem Desain — Liebe Pyrus B2B

**Versi Dokumen:** 1.0
**Tanggal:** 25 November 2026
**Mengacu ke:** [01-PRD.md](01-PRD.md)

Tujuan dokumen ini adalah memastikan setiap halaman publik maupun panel admin **Liebe Pyrus** tampil sebagai satu produk korporat yang berwibawa, terpercaya di mata pengambil keputusan B2B, mudah dipindai di ponsel maupun layar lebar, dan bebas dari gaya visual yang dibuat sembarangan.

---

## 1. Identitas & Filosofi Brand: Liebe Pyrus

- **Nama Brand:** `LIEBE PYRUS` (`PT Liebe Pyrus Indonesia`)
- **Tagline Utama:** *"Crafted with Care, Built to Endure."*
- **Sub-Tagline Bahasa Indonesia:** *"Dari Ketelitian Menuju Keunggulan Korporat."*
- **Arti & Filosofi Nama:**
  1. **Liebe** *(Ketulusan, Ketelitian, & Kepedulian Detail)*: Merepresentasikan komitmen bahwa setiap unit *merchandise* membawa reputasi perusahaan pemesan maupun mitra *reseller*; tidak boleh ada kompromi pada presisi cetak logo dan kerapian kemasan.
  2. **Pyrus** *(Genus Pohon Pir — Ketangguhan Kayu, Pertumbuhan, & Kemitraan yang Berbuah)*: Melambangkan daya tahan fisik material produk (seperti *SUS 304* dan elektronik bergaransi 1 tahun) serta kemitraan bisnis jangka panjang yang terus bertumbuh.
- **Karakter Suara (*Tone of Voice*):**
  - **Tegas, Faktual, & Bertanggung Jawab:** Hindari hiperbola kosong seperti *"paling murah dan paling bagus se-Indonesia"*. Gunakan kalimat terukur seperti *"Material tumbler diuji laboratorium minimal SUS 304, diperiksa satu per satu melalui 4 tahap QC, dan dilindungi garansi resmi 1 tahun untuk seluruh produk elektronik."*
  - **Ramah Reseller & Korporat:** Berbicara sebagai mitra kerja satu pintu yang melindungi reputasi klien (*"Jika hasil cetak cacat, tanggung jawab penuh ada pada kami, bukan Anda"*).

---

## 2. Palet Warna & Token Tema (`CSS Custom Properties`)

Gaya visual memadukan **kontras seksi terang dan gelap bergantian** (*alternating light ivory & executive deep navy sections*) dengan aksen **Warm Pyrus Gold** untuk penekanan premium dan **WhatsApp Emerald** khusus aksi konversi chat.

| Token CSS | Nilai Hex | Peruntukan |
| --- | --- | --- |
| `--color-navy-950` | `#0A1426` | Latar footer paling bawah, overlay gelap |
| `--color-navy-900` | `#0F1D35` | Seksi korporat gelap (`section-navy`), header utama, kartu hero |
| `--color-navy-800` | `#182B4D` | Permukaan kartu di atas latar gelap, hover tombol gelap |
| `--color-gold-500` | `#C89B3C` | Aksen utama **Pyrus Gold**: kicker judul seksi, badge `Unggulan`, CTA utama katalog |
| `--color-gold-600` | `#B08428` | State hover/aktif tombol Pyrus Gold (kontras aman) |
| `--color-gold-100` | `#F9F2E1` | Latar lembut chip/badge bernuansa emas |
| `--color-canvas` | `#F8F7F4` | Latar halaman terang (`section-light`) yang hangat dan tidak menyilaukan mata |
| `--color-surface` | `#FFFFFF` | Latar kartu produk, tabel spesifikasi, modal OTP, dan input form |
| `--color-border` | `#E3E1DA` | Garis tepi kartu, pembatas baris tabel spesifikasi, border filter |
| `--color-ink` | `#121926` | Teks judul dan isi utama di atas latar terang (rasio kontras > 14:1) |
| `--color-muted` | `#525B6C` | Teks pendukung, kode SKU, keterangan waktu/meta (lulus WCAG AA ≥ 4.5:1) |
| `--color-whatsapp` | `#15803D` | Tombol konversi WhatsApp (hijau korporat tegas & mudah terbaca teks putih) |
| `--color-whatsapp-hover` | `#166534` | State hover tombol WhatsApp |
| `--color-info` / `--color-danger` | `#1D4ED8` / `#DC2626` | Badge `Baru`, pesan validasi error form/OTP, aksi hapus di CMS |

### Aturan Ritme Seksi Halaman:
- Gunakan pergantian seksi `.section-light` (`#F8F7F4`) dan `.section-navy` (`#0F1D35` dengan teks putih `#F8FAFC` dan judul aksen `#E0B65A`) agar halaman panjang tetap nyaman dipindai dan memiliki hierarki visual yang jelas.
- Pada satu tampilan layar, maksimal hanya ada **satu grup CTA utama** yang mencolok agar perhatian pengunjung tidak terpecah.

---

## 3. Tipografi (*Self-Hosted `.woff2`*)

Font dimuat dari domain sendiri (`/fonts/*.woff2`) dengan `font-display: swap` untuk mencegah *layout shift* dan ketergantungan koneksi luar:

1. **Heading & Navigasi — `Plus Jakarta Sans` (`600`, `700`, `800`):**
   - `H1` (Hero / Judul Halaman Utama): `clamp(2rem, 3.6vw, 3.125rem)`, `font-weight: 800`, `line-height: 1.15`, `letter-spacing: -0.02em`.
   - `H2` (Judul Seksi): `clamp(1.5rem, 2.5vw, 2.25rem)`, `font-weight: 700`, `line-height: 1.22`.
   - `H3` (Judul Kartu / Nama Produk): `1.125rem` – `1.25rem`, `font-weight: 700`, `line-height: 1.35`.
2. **Isi Teks, Tabel & Form — `DM Sans` (`400`, `500`):**
   - Body Large (Lead / Subjudul Hero): `1.125rem` (`18px`), `line-height: 1.65`.
   - Body Standar: `1rem` (`16px`), `line-height: 1.6`.
   - Kode SKU & Label Kecil: `0.875rem` (`14px`), `font-weight: 500`, `letter-spacing: 0.03em`.

---

## 4. Skala Bentuk, Tombol & Komponen Inti

### 4.1 Ukuran & Sudut Komponen

| Elemen | Radius Sudut | Tinggi Desktop | Tinggi Mobile (`< 1024px`) |
| --- | --- | --- | --- |
| Tombol Utama / CTA (`btn`) | `10px` (korporat tegas) | `44px` (`btn-lg`: `50px`) | `48px` (`btn-lg`: `54px`) |
| Chip Filter Kategori / Subkategori | `9999px` (kapsul) | `38px` | `44px` |
| Input Text, Select, Input OTP | `10px` | `44px` | `48px` (teks `16px` cegah auto-zoom iOS) |
| Kartu Produk / Layanan / Portfolio | `16px` | Otomatis (rasio gambar `1:1` atau `4:3` konsisten) | Otomatis |
| Badge Status (`Unggulan`, `Baru`) | `9999px` | `26px` | `26px` |
| Modal Dialog (OTP / Konfirmasi) | `20px` | Lebar maks. `460px` | Lebar penuh dengan margin `16px` |

### 4.2 Varian Tombol Standar

- `btn-primary` (Pyrus Gold `#C89B3C` dengan teks `#0A1426` tebal `700` atau Navy `#0F1D35` dengan teks putih): untuk `Lihat Katalog` dan submit form utama.
- `btn-whatsapp` (`#15803D` dengan ikon telepon/chat vektor + teks putih): khusus untuk `Minta Penawaran via WhatsApp` dan `Konsultasi via WhatsApp`.
- `btn-outline`: garis tepi `1.5px` untuk aksi sekunder seperti `Download Katalog PDF`, `Reset Semua`, atau `Lihat Detail`.
- `btn-danger`: khusus aksi hapus/batalkan di dalam `/admin` (selalu disertai dialog konfirmasi).

### 4.3 Komponen Khas B2B Liebe Pyrus

1. **Kartu Produk Katalog (`ProductCard`):**
   - Rasio kotak foto `1:1` berlatar bersih dengan zoom halus (`scale(1.03)`) hanya pada perangkat ber-kursor (`@media (hover: hover)`).
   - Badge sudut kiri atas (`Unggulan` berwarna emas, `Baru` berwarna biru tua).
   - Nama produk (maks. 2 baris rapi), kode SKU `LP-...` dalam huruf kapital rapi, daftar chip mini metode cetak (`UV`, `Laser`, `Sablon`), info `MOQ 50 pcs`, dan tombol `Lihat Detail`.
2. **Tabel Spesifikasi B2B (`ProductSpecTable`):**
   - Dua kolom bergaris bersih (`Label Spesifikasi` di kiri dengan lebar tetap `38%` berlatar tipis, `Nilai Spesifikasi` di kanan), menonjolkan baris `MOQ`, `Area Logo`, dan `Garansi` agar langsung tertangkap mata tim *procurement*.
3. **Sticky Mobile RFQ Bar (`StickyWaBar` pada PDP):**
   - Muncul menempel di tepi bawah layar ponsel (`< 768px`) saat tombol utama di atas mulai tergulir lewat, menampilkan nama ringkas + SKU di kiri dan tombol `Tanya Harga (WA)` di kanan dengan `padding-bottom: env(safe-area-inset-bottom)`.
4. **Akordion FAQ (`FaqAccordion`):**
   - Menggunakan `<button aria-expanded="true|false">` dengan indikator `+` / `−` jelas, mendukung pembukaan mandiri tanpa lompatan layout.

---

## 5. Standar Ikonografi & Visual

1. Gunakan satu pustaka ikon: **Lucide Icons** (`16px` di dalam tombol/chip, `20px` di navigasi/info kontak, `24px–28px` di kotak keunggulan layanan).
2. **Larangan Keras Emoji:** Jangan pernah menggunakan karakter emoji di judul, kartu fitur, tombol, badge, maupun di dalam string URL `?text=` WhatsApp.
3. Setiap gambar konten (`<img>`) wajib memiliki atribut `width`, `height`, dan `alt` deskriptif Bahasa Indonesia (kecuali ilustrasi murni dekoratif yang wajib diberi `alt=""` dan `aria-hidden="true"`).

---

## 6. Breakpoint Responsif & Tata Letak

| Lebar Layar | Perilaku Tata Letak |
| --- | --- |
| `< 640px` (Ponsel) | Navigasi menjadi drawer; grid katalog 1 atau 2 kolom padat; panel filter 3-layer berada di dalam akordion/laci filter dengan tombol `Filter (N aktif)`; sticky bar WA aktif di halaman produk |
| `640px – 1023px` (Tablet) | Grid kategori & produk 2–3 kolom; tabel spesifikasi dan galeri PDP mulai berdampingan proporsional |
| `1024px – 1439px` (Laptop) | Navigasi horizontal penuh dengan dropdown hover/focus; grid produk 4 kolom; lebar kontainer utama maks. `1240px` terpusat |
| `≥ 1440px` (Desktop Lebar) | Kontainer maks. `1320px` dengan ruang napas lega; sidebar Admin CMS menempel tetap (`sticky`) di sisi kiri |
