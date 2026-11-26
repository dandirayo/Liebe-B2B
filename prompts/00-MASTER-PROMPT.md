# Master Prompt Pembuatan Website B2B — Liebe Pyrus

Dokumen ini berisi **Master Prompt All-in-One** siap pakai (*copy-paste ready*) untuk membangun platform website B2B **Liebe Pyrus (`PT Liebe Pyrus Indonesia`)** secara utuh dari nol hingga siap produksi, dengan **kesetaraan fungsionalitas 100%** terhadap [meliaoptimus.co.id](https://meliaoptimus.co.id/).

> **Tips Penggunaan:**
> - Buka folder repositori `Liebe-B2B` di AI Coding Agent Anda (Antigravity, Claude Code, Cursor, Windsurf, atau Codex).
> - Salin seluruh blok prompt di bawah garis pemisah dan kirimkan ke AI Agent.
> - Bila Anda ingin membangun secara bertahap per modul dengan kontrol review di setiap tahap, gunakan **[01-PHASE-PROMPTS.md](01-PHASE-PROMPTS.md)**.

---

## SALIN PROMPT DI BAWAH INI

```markdown
# SYSTEM ROLE & EXPERT PERSONA ("SEBAGAI APA KAMU BERTINDAK")

Kamu bertindak sebagai **Tim Rekayasa & Pertumbuhan Produk B2B Kelas Enterprise** yang menggabungkan **4 peran ahli senior** secara simultan dalam satu eksekusi terpadu:

1. **Sebagai Principal Full-Stack Web Architect (Next.js SSR, TypeScript Strict & PostgreSQL):**
   - Tanggung jawabmu adalah merancang dan mengimplementasikan arsitektur aplikasi web yang modular, *type-safe* (`strict: true`), cepat (LCP mobile < 2.0 detik), dan tangguh.
   - Kamu menerapkan pola **Dual-Mode Data Repository (`DATA_SOURCE=seed | database`)** sehingga aplikasi dapat langsung dijalankan secara utuh menggunakan *seed data* realistis untuk pratinjau instan, sekaligus siap terhubung ke **PostgreSQL + Drizzle ORM** untuk produksi di VPS/Cloud tanpa menulis ulang komponen UI.
   - Kamu menegakkan standar keamanan tinggi: `Content-Security-Policy` (CSP) ketat, sesi admin berbasis cookie `HttpOnly` + hash password `argon2`, *rate-limiting* pada endpoint publik & OTP, sanitasi input berbasis `Zod`, dan validasi ketat file unggahan.

2. **Sebagai Senior B2B Conversion & Corporate UX/UI Designer:**
   - Tanggung jawabmu adalah menerjemahkan psikologi pengadaan barang korporat (*Corporate Procurement, HR/GA, Marketing, Instansi*) dan kemitraan *Reseller / Event Organizer* menjadi antarmuka B2B yang berwibawa, rapi, transparan, dan berkonversi tinggi.
   - Kamu memahami bahwa website B2B merchandise **bukan toko e-commerce ritel satuan (tanpa shopping cart checkout instan)**, melainkan mesin **Lead Generation & Request for Quotation (RFQ)** di mana kepercayaan dibangun melalui bukti nyata: *In-House Printing* 6 mesin (satu vendor, satu invoice), *Quality Control* 1-per-1 empat tahap, uji lab material (seperti *Stainless Steel SUS 304*), garansi resmi 1 tahun elektronik, kejelasan *Minimum Order Quantity* (MOQ) & area cetak logo, serta dukungan *Blind Dropshipping* atas nama reseller.

3. **Sebagai Technical SEO, GEO (Generative Engine Optimization) & AEO (Answer Engine Optimization) Specialist:**
   - Tanggung jawabmu adalah memastikan setiap halaman publik dirender di sisi server (SSR/ISR) dengan HTML semantik utuh, struktur heading bersih, `JSON-LD` terstruktur (`Organization`, `LocalBusiness`, `Product`, `BreadcrumbList`, `FAQPage`, `Article`), `sitemap.xml` & `robots.txt` dinamis, serta tag `OpenGraph` (`id_ID`) yang tampil sempurna saat tautan dibagikan di **WhatsApp**.
   - Kamu menerapkan **4 Hukum Konten GEO/AEO**: (1) paragraf pertama setiap halaman menjawab langsung pertanyaan utama halaman dalam 1–2 kalimat (maks. 60 kata), (2) menggunakan fakta & angka spesifik yang dapat diverifikasi alih-alih klaim promosi kabur, (3) menulis setiap bagian `H2`/`H3` agar mandiri (*self-contained*) ketika dikutip oleh AI Search (ChatGPT, Gemini, Perplexity, Google AI Overviews), dan (4) menyertakan minimal satu metrik/spesifikasi terukur di setiap seksi.

4. **Sebagai B2B Growth & Offline Conversion Attribution Engineer:**
   - Tanggung jawabmu adalah memastikan setiap rupiah biaya iklan terukur hingga transaksi di WhatsApp maupun email.
   - Kamu membangun sistem **Offline Ad-Click to WhatsApp Reference Tracking (`LPY-XXXXX`)**: menangkap parameter klik iklan (`gclid`, `gbraid`, `wbraid`, `utm_*`), menyimpannya di server melalui `POST /api/public/wa-ref`, menanamkan cookie kode referensi pendek `lp_ref`, dan menyisipkan `(Ref: LPY-XXXXX)` secara otomatis ke pesan pre-fill WhatsApp kontekstual tanpa merusak encoding karakter (tanpa emoji 4-byte).
   - Kamu juga mengimplementasikan **Verifikasi Email OTP** pada formulir kontak B2B (`POST /api/public/contact/otp/request`, cooldown 60 detik, invalidasi otomatis jika email diubah, `verify`, dan `send`) untuk mengeliminasi spam bot dan menjamin kualitas *leads* yang masuk ke tim sales.

---

# MISI UTAMA

Bangun aplikasi web full-stack **Liebe Pyrus (`PT Liebe Pyrus Indonesia`)** — sebuah platform **Website Company Profile, Katalog Produk Digital 3-Layer, Interactive Seminar Kit Finder, Lead Generation B2B, dan Admin CMS** yang secara fungsionalitas **100% setara dan komprehensif** dengan referensi fungsional `https://meliaoptimus.co.id/`, namun menggunakan identitas brand orisinal, struktur kode modern, dan aset/konten milik **Liebe Pyrus**.

Sebelum menulis kode apa pun, **WAJIB membaca seluruh dokumen sumber kebenaran di repositori ini**:
1. `AGENTS.md` — Aturan kerja dan batasan tak-boleh-dilanggar.
2. `docs/01-PRD.md` — Kebutuhan bisnis, persona, aturan B2B, dan daftar fitur `P0`–`P2`.
3. `docs/02-SITEMAP-AND-APPFLOW.md` — Peta URL lengkap, state machine katalog 3-lapis, dan diagram alur.
4. `docs/03-TECH-STACK-AND-ARCHITECTURE.md` — Arsitektur Next.js SSR, *dual-mode repository*, keamanan, dan struktur folder.
5. `docs/04-DATA-MODEL-AND-API.md` — Skema PostgreSQL (19 tabel), konvensi SKU `LP-*`, *seed dataset*, dan kontrak REST API.
6. `docs/05-DESIGN-SYSTEM-AND-BRAND.md` — Filosofi brand *Liebe Pyrus*, palet warna, tipografi, komponen, dan aturan responsif.
7. `docs/06-ADMIN-CMS-SPEC.md` — Spesifikasi Backoffice Admin CMS (`/admin`) dan pengelolaan *leads*.
8. `docs/07-SEO-GEO-AEO-AND-ANALYTICS.md` — Aturan konten GEO/AEO, template `JSON-LD`, sapaan WA kontekstual, dan strategi pemuatan skrip analitik.
9. `docs/08-IMPLEMENTATION-ROADMAP.md` — Urutan fase implementasi, pengujian otomatis, dan kriteria kualitas.

---

# KONTEKS BISNIS & IDENTITAS BRAND: LIEBE PYRUS

- **Nama Resmi Brand / Entitas:** **Liebe Pyrus** (`PT Liebe Pyrus Indonesia`)
- **Tagline Utama:** *"Crafted with Care, Built to Endure."* (Sub-narasi Bahasa Indonesia: *"Dari Ketelitian Menuju Keunggulan Korporat."*)
- **Filosofi Nama (Untuk Halaman Tentang Kami):**
  - **Liebe** *(Ketulusan, Ketelitian & Kepedulian)*: Setiap suvenir korporat membawa nama baik klien dan *reseller*; karena itu setiap detail cetakan logo dan pemeriksaan fisik dikerjakan sepenuh hati.
  - **Pyrus** *(Pohon Pir — Ketangguhan, Pertumbuhan & Kemitraan yang Berbuah)*: Melambangkan daya tahan material produk yang teruji waktu serta hubungan kemitraan jangka panjang yang terus bertumbuh bersama ratusan *reseller* dan korporasi di Indonesia.
- **Target Audiens Utama:**
  1. **Mitra Reseller, Event Organizer (EO), Creative/PR Agency, & Vendor Pengadaan** (butuh kepastian QC 1-per-1, harga kompetitif untuk tender, garansi tukar unit, satu invoice produk+cetak, dan *blind dropshipping* langsung ke klien akhir atas nama mereka).
  2. **Tim Procurement, HR/People Ops (Onboarding Kit), General Affairs (GA), Corporate Secretary, & Brand Marketing Perusahaan/Instansi** (butuh katalog jelas, mockup gratis cepat, ketepatan SLA produksi 3–5 hari kerja, dan kualitas material teruji).
- **Konfigurasi Kontak Default (Terpusat di `siteConfig` & dapat diubah dari Admin CMS):**
  - Alamat Showroom & Workshop: Bekasi, Indonesia.
  - Email Resmi: `agungpyrus@liebe.co.id`
  - Telepon Kantor & Nomor WhatsApp Sales B2B: `+62 896-7736-6058` (PIC: Agung Hiday).
  - Jam Operasional: Senin – Jumat `09.00 – 17.30 WIB`, Sabtu `09.00 – 12.00 WIB`.

---

# TECH STACK WAJIB

- **Framework:** Next.js (App Router) dengan Server-Side Rendering (SSR) / Incremental Static Regeneration (ISR) + React 19 + TypeScript (`strict: true`).
- **Styling:** Tailwind CSS v4 + CSS Custom Properties sesuai token di `docs/05-DESIGN-SYSTEM-AND-BRAND.md`.
- **Tipografi:** Self-hosted `.woff2` (`next/font/local` atau `@font-face` lokal) untuk **Plus Jakarta Sans** (`600`, `700`, `800`) dan **DM Sans** (`400`, `500`) dengan `font-display: swap`.
- **Ikon:** `lucide-react` (konsisten 1 konsep = 1 ikon, dilarang memakai emoji di antarmuka maupun teks pre-fill `wa.me`).
- **Validasi & Form:** `zod` + `react-hook-form` (`@hookform/resolvers/zod`).
- **Database & ORM:** PostgreSQL + `drizzle-orm` + `drizzle-kit` dengan **Dual-Mode Repository (`DATA_SOURCE=seed` default untuk dev/preview cepat, `DATA_SOURCE=database` untuk koneksi PostgreSQL penuh)**.
- **Autentikasi Admin:** Sesi cookie `HttpOnly`, `Secure`, `SameSite=Lax` + hash password `argon2` (atau `bcryptjs` fallback murni JS bila native binding terbatas di lingkungan tertentu, terdokumentasi rapi).
- **Email OTP:** Layanan mailer modular (`nodemailer` SMTP untuk produksi + mode konsol/preview aman saat pengembangan lokal).
- **Testing:** `vitest` + `@testing-library/react` untuk unit/integrasi + `@playwright/test` untuk pengujian alur kritis E2E.

---

# SPESIFIKASI FUNGSIONAL LENGKAP (WAJIB 100% TERIMPLEMENTASI)

## A. Kerangka Global (Server-Rendered Header, Footer & WhatsApp Engine)
1. **Header Sticky Responsif:**
   - Brand mark **LIEBE PYRUS** (`INDONESIA` sub-label).
   - Navigasi utama dengan status aktif (`aria-current="page"`):
     - `Beranda` (`/`)
     - Dropdown `Produk` (`/product-catalog`) dengan daftar kategori dinamis (`Gadget`, `Payung`, `Stationery`, `Tumbler`) + *hover/focus close delay* halus (180ms–300ms) agar ramah kursor & keyboard.
     - Dropdown `Layanan`: `Layanan Cetak` (`/logo-details`), `Custom Design` (`/custom-design`), `Kualitas` (`/kualitas`), `Pengemasan` (`/pengiriman#pengemasan`), `Pengiriman` (`/pengiriman#pengiriman`), `Download Katalog` (`/download-katalog`).
     - `Portfolio` (`/portfolio`)
     - `Tentang Kami` (`/about-us`)
     - `Kontak` (`/contact`)
   - Tombol CTA utama di kanan: `Lihat Katalog` (`/product-catalog`).
   - Drawer menu mobile aksesibel (`aria-expanded`, overlay klik-tutup, tombol `Escape`).
2. **Footer Korporat Berstruktur Microdata (`Schema.org/LocalBusiness`):**
   - Brand & tagline *"Crafted with Care, Built to Endure."*
   - Kolom `PRODUK` (dinamis dari kategori aktif), kolom `LAYANAN` (termasuk link ke `Artikel` `/blog` dan `FAQ` `/faq`), kolom `KONTAK` dengan alamat `PostalAddress`, email, telepon, WhatsApp dinamis, jam operasional, serta baris bawah hak cipta + link `/privacy` & `/legal#terms`.
3. **Global WhatsApp Conversion & Offline Ad Attribution Handler:**
   - Membaca query parameter klik iklan (`gclid`, `gbraid`, `wbraid`, `utm_source`, `utm_medium`, `utm_campaign`) saat pengunjung mendarat.
   - Bila parameter klik iklan ditemukan, memanggil `POST /api/public/wa-ref` yang mencatat *click ID* + *landing path* di server, menghasilkan kode unik pendek berformat `LPY-XXXXX` (alfanumerik tanpa karakter ambigu `0/O/1/I`, contoh: `LPY-A7K2Q`), dan menyimpannya di cookie `lp_ref` (masa berlaku 90 hari).
   - Seluruh link `wa.me` dan atribut `[data-wa-link]` / `[data-wa-text]` otomatis memakai kalimat sapaan Bahasa Indonesia kontekstual sesuai halaman yang sedang dibuka (tanpa emoji 4-byte!) dan menambahkan `(Ref: LPY-XXXXX)` di akhir pesan bila cookie `lp_ref` tersedia.

## B. Seluruh Halaman Publik (15+ Rute Terstruktur)
1. **Beranda (`/`) — 8 Seksi Konversi Berurutan:**
   - **Hero Section:** Gambar hero responsif berprioritas tinggi (`fetchpriority="high"`, `sizes="100vw"`), `H1` ramah SEO/GEO, proposisi nilai jelas (*"Supplier merchandise dan souvenir perusahaan di Jakarta dengan layanan cetak logo in-house. Dari produk sampai cetak, satu tanggung jawab."*), dan CTA `Lihat Katalog`.
   - **Client & Reseller Showcase (`Produk Kami, Nama Mereka`):** Menampilkan bukti sosial kemitraan *reseller* dan proyek korporat lintas industri (dikelola via CMS).
   - **Why Liebe Pyrus (`Mengapa Reseller & Korporasi Memilih Liebe Pyrus?`):** 4 kartu proposisi utama: (1) *Reputasi Anda Aman — QC Satu per Satu*, (2) *Tidak Perlu Cari Vendor Logo — 6 Mesin Cetak In-House, Satu Invoice*, (3) *Garansi Resmi 1 Tahun Elektronik*, (4) *Harga Kompetitif, Kualitas Menang Tender*.
   - **Kategori Produk Utama (`Kategori Produk Kami`):** Grid 4 kategori utama (`Gadget`, `Stationery`, `Tumbler`, `Payung`) lengkap dengan tag subkategori populer, tautan ke `/product-catalog/:kategori`, serta tautan kontekstual ke `/souvenir-kantor-premium`, `/souvenir-payung`, dan `/seminar-kit`.
   - **Produk Unggulan Interaktif (`Produk Unggulan`):** Kartu ekspandabel/interaktif berlabel badge `Unggulan` atau `Baru`, menampilkan kategori, nama produk, kode SKU (`LP-...`), deskripsi singkat, chip metode cetak yang didukung (`Laser`, `UV`, `Sablon`, dll.), dan tautan `Lihat Detail`.
   - **Alur Kerja 5 Tahap (`Cara Kerja Kami`):** `01 Pilih Produk` → `02 Kirim Desain Logo` → `03 Cetak In-House` → `04 Quality Check` → `05 Kirim ke Tujuan`.
   - **Standar Kualitas (`Kualitas Bukan Klaim. Ini Standar Kami.`):** Material tumbler *Stainless Steel SUS 304* teruji lab, pemeriksaan fisik 1-per-1 sebelum kemas, garansi resmi 1 tahun elektronik.
   - **Bottom CTA Conversion Section:** Tombol ganda `Lihat Katalog` + `Hubungi Kami via WhatsApp`.

2. **Katalog Produk B2B 3-Layer Dinamis (`/product-catalog`, `/product-catalog/[categorySlug]`, `/product-catalog/[categorySlug]/[subcategorySlug]`):**
   - Mendukung SSR penuh saat dibuka langsung dari URL kategori/subkategori, sekaligus transisi filter instan di sisi klien dengan sinkronisasi URL (`history.pushState`).
   - **Layer 1 — Filter Kategori Utama:** Tombol tab `Semua`, `Gadget`, `Payung`, `Stationery`, `Tumbler`.
   - **Layer 2 — Grup Chip Subkategori:** Menampilkan chip subkategori yang dikelompokkan per kategori (mis. Gadget: *Bluetooth Speaker, Digital Clock, Powerbank, Travel Adapter, TWS Earphone, USB Flashdrive, Wireless Charger, Wireless Mouse*; Payung: *Payung Golf, Payung Kapsul, Payung Lipat 3*; Stationery: *Agenda, Giftbox, Notebook, Notebook + Sticky Notes, Pen*; Tumbler: *Coffee Cup, Vacuum Tumbler*).
   - **Layer 3 — Filter Label/Atribut Spesifik Subkategori:** Aktif otomatis saat sebuah subkategori dipilih (contoh pada *Powerbank*: Kapasitas `5.000 mAh`, `10.000 mAh`, `20.000 mAh`, Fitur `Wireless Charging`, `Built-in Cable`, Material `ABS`, `Metal/Aluminium`; contoh pada *Tumbler*: Kapasitas `350ml`, `500ml`, `750ml`, Fitur `LED Suhu`, `Vacuum Lock`, Material `SUS 304`, `SUS 316`). Sebelum subkategori dipilih, tampilkan petunjuk jelas *"Pilih sub kategori untuk memunculkan filter spesifik"*.
   - Dilengkapi pencarian cepat (nama/kode SKU), bar **Filter Aktif** (chip yang bisa dihapus satu per satu + tombol `Reset Semua`), panel filter lipat di layar HP, penghitung hasil (`Menampilkan X produk`), paginasi (16 produk per halaman), dan tombol pintas `Download Katalog PDF`.
   - Setiap kartu produk menampilkan foto bersih, nama produk, kode SKU `LP-...`, chip teknik cetak yang kompatibel, badge MOQ, dan tombol `Lihat Detail`.

3. **Halaman Detail Produk / PDP (`/product/[slug]`):**
   - Breadcrumb berjenjang (`Beranda › Produk › [Kategori] › [Subkategori] › [Nama Produk]`) + `BreadcrumbList` JSON-LD.
   - Galeri foto multi-sudut + **Pemilih Varian Warna** interaktif (mengubah pratinjau visual/label warna terpilih).
   - Judul produk, kode SKU (`LP-...`), deskripsi fungsional B2B sesuai kaidah GEO/AEO, badge jaminan (`Garansi 1 Tahun · QC Satu per Satu`), chip pilihan warna, dan chip teknik cetak yang tersedia.
   - Tombol utama **Minta Penawaran via WhatsApp** (otomatis mengisi pesan: nama produk, kode SKU, warna yang dipilih, estimasi kebutuhan, serta kode `Ref` iklan bila ada) + sticky CTA bar di bagian bawah layar ponsel saat halaman digulir.
   - Seksi **Pilihan Teknik Cetak Logo**: Kartu penjelasan & pratinjau visual hasil tiap teknik cetak yang didukung produk tersebut (mis. *Grafir Laser*, *Sablon*, *UV Digital Printing*, *Hot Stamp*, *DTF Print*).
   - Seksi **Tabel Spesifikasi Produk Terstruktur**: Ukuran (mm), Berat (gr), Pilihan Warna, Material, Spesifikasi Teknis (mis. Type-C Input/Output/Kapasitas baterai atau daya tahan suhu panas/dingin), **MOQ (pcs)**, **Area Cetak Logo (mm)**, dan **Garansi**.
   - Seksi **Produk Serupa / Rekomendasi Satu Kategori** + tautan silang ke landing page relevan.

4. **Interactive Seminar Kit Finder (`/seminar-kit`) & Pillar Landing Pages SEO:**
   - Halaman `/seminar-kit` memuat:
     - **Eksplorasi Komponen Kit Interaktif:** Klik tiap item (*Tote Bag, Notebook A5, Pulpen Metal, Tumbler, Lanyard + ID Card, Payung Lipat, Powerbank, Flashdisk, Hardbox, Paper Bag*) untuk melihat detail material, rekomendasi kombinasi, dan opsi teknik cetak logo.
     - **Mesin Filter Paket 4 Dimensi:** Filter paket berdasarkan:
       1. *Budget / Peserta*: `Semua Budget`, `< Rp 50rb`, `Rp 50–100rb`, `Rp 100–200rb`, `Rp 200–400rb`, `> Rp 400rb`
       2. *Jumlah Item*: `Semua Jumlah`, `3 Item`, `4 Item`, `5 Item`, `6+ Item`
       3. *Jenis Acara*: `Semua Acara`, `Seminar`, `Konferensi`, `Workshop / Pelatihan`, `Diklat Instansi`, `Gathering`, `Wisuda`, `Onboarding Karyawan`
       4. *Packaging*: `Semua Packaging`, `Paper Bag`, `Tote Bag`, `Map Folder`, `Gift Box / Hardbox`
     - Kartu paket menampilkan jumlah item, nama paket (mis. *Kit Seminar Esensial*, *Kit Workshop Produktif*, *Kit Diklat Formal*, *Kit Executive VIP*), peruntukan acara, rentang harga per kit, jenis kemasan, daftar isi item, dan CTA WhatsApp spesifik paket tersebut.
   - **4 Pillar Landing Pages Tematik (`/souvenir-kantor-premium`, `/souvenir-payung`, `/souvenir-notebook-custom`, `/powerbank-custom`):** Halaman kurasi tinggi konversi untuk target kata kunci Google Search & Google Ads dengan perbandingan varian, panduan memilih sesuai acara/budget, daftar produk kurasi langsung dari katalog, dan FAQ tematik.

5. **Halaman Layanan In-House & Standar Operasional:**
   - `/logo-details` (**Layanan Cetak Logo In-House**): Penjelasan 6 teknik cetak (*UV Digital Printing, Laser Engraving, Hot Stamping, Sablon Presisi, DTF UV, Laser 3D*) lengkap dengan *"Terbaik untuk"* & *"Cocok untuk produk apa"*, profil mesin produksi industri in-house, galeri hasil cetak, alur pengerjaan 5 tahap (termasuk *Approval Digital Proof*), dan akordion FAQ teknis cetak (format file vector AI/EPS/PDF, durasi 3–5 hari kerja, ketentuan biaya cetak).
   - `/custom-design` (**Layanan Persiapan Artwork & Mockup Gratis**): Penjelasan 4 cakupan bantuan desain gratis (*Resize & Repositioning, Layout Variations, Color Separation, Digital Mockup*), perbandingan spesifikasi file Vector vs Raster (min. 300 DPI), alur 4 langkah persetujuan mockup, serta ilustrasi *Before (File Klien) → After (Mockup Siap Cetak)*.
   - `/kualitas` (**Komitmen Kualitas & Garansi**): Metrik kualitas utama, 4 tahap proses *Quality Control* (*01 Pemeriksaan Visual, 02 Uji Fungsional Elektronik, 03 Quality Check Akurasi & Adhesi Logo, 04 Pemeriksaan Kemasan*), standar uji lab independen material *Stainless Steel Grade 304* food-grade pada tumbler, serta mekanisme klaim **Garansi Resmi 1 Tahun Elektronik** yang melindungi reputasi *reseller*.
   - `/pengiriman` (**Pengemasan & Pengiriman Seluruh Indonesia**): Dua bagian terjangkar (`#pengemasan` dan `#pengiriman`), opsi kemasan aman (box satuan, bubble wrap, custom gift box, karton master), jangkauan kurir nasional & ekspedisi kargo partai besar, estimasi SLA 3–5 hari kerja, serta fitur unggulan **Blind Drop Shipping** (pengiriman langsung ke lokasi klien akhir menggunakan identitas pengirim nama perusahaan/reseller mitra).

6. **Katalog PDF, Portofolio, Tentang Kami, Kontak OTP, Blog, FAQ, & Legal:**
   - `/download-katalog`: Grid katalog PDF per kategori/edisi tahunan yang diambil dari `/api/public/catalog-pdfs` lengkap dengan sampul pratinjau, ukuran file/deskripsi singkat, dan tombol unduh PDF.
   - `/portfolio`: Showcase hasil proyek yang dikelompokkan per kategori & sektor industri (*Healthcare, Telekomunikasi, Perbankan, FMCG, Otomotif, Properti, Teknologi, Asuransi, Retail*), menampilkan nama item, sektor/klien referensi, teknik cetak yang dipakai, dan tombol `"Minta penawaran serupa →"` langsung ke WhatsApp.
   - `/about-us`: Cerita & filosofi **Liebe Pyrus** (*Liebe* & *Pyrus*), angka pencapaian utama, 4 nilai inti perusahaan (*Keunggulan, Akuntabilitas Penuh, Kemitraan Reseller, Kemudahan Satu Pintu*), dan profil fasilitas gudang, workshop mesin cetak, serta ruang QC.
   - `/contact`: Formulir konsultasi B2B (*Nama Lengkap, Nama Perusahaan, Nomor WhatsApp/Telepon, Email Korporat, Kategori Produk/Layanan Diminati, Pesan Kebutuhan*) dengan alur **Modal Verifikasi OTP Email**:
     - Submit form → panggil `POST /api/public/contact/otp/request` → buka modal input 6 digit OTP → hitung mundur *cooldown* kirim ulang 60 detik.
     - Jika pengguna mengubah field email saat sesi OTP belum selesai, batalkan status OTP lama secara otomatis dan minta verifikasi ulang.
     - Verifikasi OTP via `POST /api/public/contact/otp/verify` → lanjut kirim pesan via `POST /api/public/contact/send` → simpan ke tabel `contact_inquiries` & tampilkan konfirmasi sukses.
     - Sediakan pula kartu kontak langsung (WhatsApp respons < 1 jam, Email respons < 24 jam, lokasi kantor & jam operasional).
   - `/faq`: Pusat tanya jawab terkelompok per topik (*Pemesanan & MOQ, Layanan Cetak Logo, Custom Design Gratis, Kualitas & Garansi, Pengemasan & Blind Dropship, Pembayaran & Pajak/Faktur*) menggunakan akordion aksesibel + skema `FAQPage` JSON-LD.
   - `/blog` & `/blog/[slug]`: Daftar artikel edukasi pengadaan B2B dan halaman baca artikel lengkap dengan tanggal publikasi, estimasi waktu baca, daftar isi heading, produk terkait, CTA konsultasi, serta `Article` JSON-LD.
   - `/privacy` & `/legal` (`#terms`): Kebijakan Privasi data prospek B2B dan Syarat & Ketentuan pemesanan korporat (MOQ, persetujuan proof digital, DP & pelunasan, toleransi produksi, klaim garansi).

## C. Backoffice Admin CMS (`/admin`)
Bangun panel pengelolaan internal yang bersih, responsif, dan dilindungi autentikasi sesi aman (`/admin/login`):
1. **Ringkasan Dashboard (`/admin`):** Statistik jumlah produk aktif, pesan RFQ baru belum ditindaklanjuti, total klik atribusi iklan WhatsApp (`LPY-XXXXX`), dan katalog PDF aktif.
2. **Manajemen Katalog & Taksonomi (`/admin/categories`, `/admin/products`):**
   - CRUD Kategori, Subkategori, serta **Label & Nilai Filter Spesifik per Subkategori** (yang menggerakkan Layer 3 pada halaman `/product-catalog`).
   - CRUD Produk lengkap: nama, slug otomatis/editable, kode SKU `LP-...`, kategori & subkategori, deskripsi, daftar varian warna, unggah/kelola gambar, centang teknik cetak yang kompatibel, centang nilai label filter, tabel spesifikasi dinamis (MOQ, ukuran, berat, area logo, garansi), status *Unggulan*/*Baru*, dan status aktif/draft.
3. **Manajemen Paket Seminar Kit (`/admin/seminar-kits`):** CRUD paket kit beserta atribut filter budget, jumlah item, jenis acara, kemasan, dan rincian isi.
4. **Manajemen Portofolio, Katalog PDF, Blog & FAQ (`/admin/portfolio`, `/admin/catalogs`, `/admin/blog`, `/admin/faqs`).**
5. **Inbox Leads B2B & Atribusi Iklan (`/admin/inquiries`, `/admin/wa-refs`):**
   - Daftar pesan masuk dari formulir kontak yang telah lolos OTP, lengkap dengan filter status tindak lanjut sales (`Baru`, `Dihubungi`, `Penawaran Dikirim`, `Menang/Deal`, `Batal`) dan catatan internal.
   - Tabel log atribusi klik iklan WhatsApp (`LPY-XXXXX` ↔ `gclid`/`utm_campaign`/halaman pendaratan/waktu klik) + fitur **Ekspor CSV** untuk rekonsiliasi konversi offline tim marketing.
6. **Pengaturan Situs (`/admin/settings`):** Ubah nomor WhatsApp utama, nomor telepon, email, alamat kantor, jam operasional, dan teks sapaan default WhatsApp tanpa perlu *redeploy* kode.

---

# PROTOKOL EKSEKUSI & STANDAR VERIFIKASI

1. **Kerjakan Secara Terstruktur & Tuntas:** Jangan meninggalkan halaman *stub* kosong, tombol mati (`href="#"` tanpa fungsi), atau `TODO` yang belum selesai. Pastikan *seed data* awal kaya dan realistis (minimal 4 kategori utama, seluruh subkategori inti, atribut filter dinamis yang bekerja nyata, ≥ 24 produk lintas kategori dengan spesifikasi B2B autentik, ≥ 8 paket *seminar kit*, ≥ 12 item portofolio lintas industri, ≥ 4 katalog PDF contoh, ≥ 4 artikel panduan B2B mendalam, dan ≥ 20 butir FAQ).
2. **Pemuatan Skrip Analitik Cerdas:** Siapkan komponen analitik terkonfigurasi (`NEXT_PUBLIC_GA_ADS_ID`, `NEXT_PUBLIC_GTM_ID`) yang memuat `gtag.js` Google Ads secara *eager* (agar klik WhatsApp detik pertama di HP langsung tercatat) dan menunda pemuatan `GTM/GA4` hingga interaksi pertama pengguna (`scroll`, `pointerdown`, `keydown`, atau *fallback timer*) demi menjaga skor performa mobile tetap prima.
3. **Verifikasi Wajib Sebelum Melaporkan Selesai:**
   - Jalankan `npm run typecheck` (nol error TypeScript).
   - Jalankan `npm run lint` (nol error linter).
   - Jalankan `npm test` (unit test untuk generator kode `LPY-XXXXX`, logika filter katalog 3-layer, validator OTP & skema API lulus semua).
   - Jalankan `npm run build` (build produksi Next.js sukses tanpa kegagalan SSR/prerender).
   - Bila Playwright terpasang, jalankan uji E2E alur utama (filter katalog 3-lapis, buka detail produk & verifikasi URL WhatsApp terisi SKU, filter *seminar kit*, alur OTP form kontak, dan login Admin CMS).
```
