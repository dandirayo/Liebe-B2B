# Modular Phase Prompts (Fase 1 s/d Fase 6) — Liebe Pyrus B2B

Dokumen ini memecah [00-MASTER-PROMPT.md](00-MASTER-PROMPT.md) menjadi **6 Prompt Eksekusi Bertahap** agar pembangunan website **Liebe Pyrus (`PT Liebe Pyrus Indonesia`)** dapat dijalankan secara presisi tinggi, mudah ditinjau di setiap titik henti (*checkpoint*), dan bebas dari pemotongan konteks pada AI Coding Agent.

## Cara Pemakaian

1. Jalankan mulai dari **Prompt Fase 1** hingga selesai dan pastikan seluruh perintah verifikasi di akhir fase lulus hijau.
2. Lanjutkan secara berurutan ke **Fase 2**, **Fase 3**, **Fase 4**, **Fase 5**, hingga **Fase 6**.
3. Setiap fase sudah mencantumkan **Peran Ahli ("Sebagai Apa")**, **Dokumen Acuan Wajib**, **Ruang Lingkup File/Fitur**, dan **Gerbang Verifikasi**.

---

## FASE 1 — Inisialisasi Proyek, Design System Liebe Pyrus, Layout SSR Global & Seed Data Layer

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 1)
Kamu bertindak sebagai **Principal Full-Stack Web Architect & Design Systems Engineer**. Fokusmu pada Fase 1 adalah membangun fondasi proyek Next.js (App Router) + TypeScript (`strict: true`) + Tailwind CSS v4 yang bersih, menerapkan sistem desain resmi **Liebe Pyrus**, membangun kerangka Header/Footer SSR aksesibel, dan menyiapkan lapisan **Dual-Mode Data Repository (`DATA_SOURCE=seed | database`)** beserta *seed data* B2B yang lengkap.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `AGENTS.md`
2. `docs/01-PRD.md`
3. `docs/03-TECH-STACK-AND-ARCHITECTURE.md`
4. `docs/04-DATA-MODEL-AND-API.md`
5. `docs/05-DESIGN-SYSTEM-AND-BRAND.md`

# TUGAS IMPLEMENTASI FASE 1
1. Inisialisasi proyek Next.js App Router + TypeScript strict + Tailwind CSS v4 + `lucide-react` + `zod` + `react-hook-form` + `drizzle-orm` + `vitest` di root repositori `Liebe-B2B` beserta `.env.example`.
2. Konfigurasikan Design Tokens **Liebe Pyrus** di `src/styles/globals.css` (palet Deep Prussian Navy `#0F1D35`, Pyrus Gold `#C89B3C`, Ivory Canvas `#F8F7F4`, permukaan kartu, skala radius, shadow halus, tipografi `Plus Jakarta Sans` & `DM Sans`, serta skala tombol sentuh mobile ≥ 44px).
3. Buat skema tipe domain & skema Drizzle PostgreSQL lengkap di `src/server/db/schema.ts` sesuai `docs/04-DATA-MODEL-AND-API.md`.
4. Bangun *Seed Dataset* B2B yang kaya dan realistis di `src/server/seed/`:
   - 4 Kategori utama (`Gadget`, `Payung`, `Stationery`, `Tumbler`) + seluruh subkategori inti (Powerbank, TWS Earphone, USB Flashdrive, Wireless Charger, Wireless Mouse, Travel Adapter, Digital Clock, Bluetooth Speaker, Payung Golf, Payung Kapsul, Payung Lipat 3, Agenda, Giftbox, Notebook, Notebook + Sticky Notes, Pen, Coffee Cup, Vacuum Tumbler).
   - Grup Label & Nilai Filter spesifik per subkategori (Kapasitas, Material, Fitur, Ukuran).
   - Minimal 24 produk B2B lintas kategori dengan kode SKU `LP-...`, varian warna, kompatibilitas 6 teknik cetak, spesifikasi lengkap (MOQ, ukuran, berat, area cetak logo, garansi), serta flag `isFeatured` / `isNew`.
   - Data awal Paket Seminar Kit (≥ 8 paket), Portofolio Klien lintas industri (≥ 12 proyek), Katalog PDF (≥ 4 katalog), Artikel Blog B2B (≥ 4 artikel sesuai kaidah GEO/AEO), dan FAQ terkelompok (≥ 20 tanya-jawab).
5. Bangun lapisan repositori abstrak di `src/server/repositories/` yang otomatis membaca dari *in-memory/JSON seed store* saat `DATA_SOURCE=seed` (default) dan siap memakai Drizzle PostgreSQL saat `DATA_SOURCE=database`.
6. Bangun **Global Public Layout (`Header`, `MobileNavDrawer`, `Footer`)** yang dirender di server:
   - Dropdown `Produk` & `Layanan` dengan *close delay* halus dan dukungan keyboard penuh (`Escape`, `focusin`/`focusout`, `aria-expanded`).
   - Footer berstruktur microdata `Schema.org/LocalBusiness` & `PostalAddress`.
   - Utilitas pembuat URL WhatsApp kontekstual (`buildWhatsAppUrl`) yang bebas dari karakter emoji 4-byte.

# VERIFIKASI WAJIB FASE 1
Jalankan `npm run typecheck`, `npm run lint`, `npm test`, dan `npm run build`. Pastikan semuanya lulus tanpa error sebelum melaporkan hasil Fase 1.
```

---

## FASE 2 — Beranda (8 Seksi Konversi) & Halaman Kredibilitas Layanan In-House

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 2)
Kamu bertindak sebagai **Senior B2B Conversion UX/UI Designer & GEO/AEO Technical Copywriter**. Fokusmu pada Fase 2 adalah membangun halaman depan dan seluruh halaman layanan serta profil korporat **Liebe Pyrus** yang meyakinkan *Reseller*, *Event Organizer*, dan *Corporate Procurement* untuk mempercayakan pengadaan suvenir mereka.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `docs/01-PRD.md` (kebutuhan `HOM-*` dan `SRV-*`)
2. `docs/02-SITEMAP-AND-APPFLOW.md`
3. `docs/05-DESIGN-SYSTEM-AND-BRAND.md`
4. `docs/07-SEO-GEO-AEO-AND-ANALYTICS.md` (4 Hukum Konten GEO/AEO & JSON-LD)

# TUGAS IMPLEMENTASI FASE 2
1. **Beranda (`/`)** lengkap dengan 8 seksi berurutan:
   - Hero utama berprioritas tinggi (`fetchpriority="high"`) + proposisi nilai satu pintu & CTA `Lihat Katalog`.
   - Showcase Klien & Mitra Reseller (`Produk Kami, Nama Mereka`).
   - 4 Pilar Keunggulan B2B (`Mengapa Reseller & Korporasi Memilih Liebe Pyrus?`).
   - Grid 4 Kategori Produk Utama + tautan kontekstual ke halaman paket kurasi.
   - Produk Unggulan Interaktif (`Produk Unggulan` — kartu ekspandabel dengan badge `Unggulan`/`Baru`, kode SKU `LP-...`, chip teknik cetak, dan link detail).
   - 5 Tahap Alur Kerja (`01 Pilih Produk` s/d `05 Kirim ke Tujuan`).
   - Seksi Standar Kualitas (`Kualitas Bukan Klaim. Ini Standar Kami.` — SUS 304, QC 1-per-1, Garansi 1 Tahun Elektronik).
   - Banner Konversi Bawah (`Lihat Katalog` + `Hubungi Kami via WhatsApp`) + JSON-LD `Organization`, `LocalBusiness`, & `WebSite`.
2. **Layanan Cetak Logo In-House (`/logo-details`):** 6 teknik cetak (*UV Printing, Laser Engraving, Hot Stamping, Sablon, DTF UV, Laser 3D*), profil mesin industri in-house, galeri contoh hasil cetak, alur pengerjaan 5 tahap, dan akordion FAQ teknis cetak.
3. **Custom Design & Mockup Gratis (`/custom-design`):** 4 layanan persiapan artwork gratis, panduan file Vector vs Raster (300 DPI), alur persetujuan digital proof 4 langkah, dan perbandingan visual *File Asli → Mockup Siap Cetak*.
4. **Standar Kualitas & Garansi (`/kualitas`):** Metrik utama, 4 tahap pemeriksaan *Quality Control* 1-per-1, standar uji lab material tumbler *Grade 304*, dan alur klaim garansi 1 tahun elektronik khusus mitra reseller/korporat.
5. **Pengemasan & Pengiriman Nasional (`/pengiriman`):** Seksi `#pengemasan` & `#pengiriman`, opsi box custom, ekspedisi kurir & kargo dedicated, SLA 3–5 hari kerja, dan layanan **Blind Drop Shipping** atas nama perusahaan mitra.
6. **Tentang Kami (`/about-us`)** (filosofi *Liebe* & *Pyrus*, angka pencapaian, 4 nilai inti, fasilitas gudang/cetak/QC) & **Portofolio (`/portfolio`)** (filter/grup per kategori & industri dengan tombol *"Minta penawaran serupa →"* ke WhatsApp).

# VERIFIKASI WAJIB FASE 2
Pastikan setiap halaman memenuhi aturan GEO/AEO (jawaban langsung ≤ 60 kata di awal halaman + angka spesifik), responsif di `375px` / `768px` / `1440px`, serta lulus `npm run typecheck`, `npm run lint`, dan `npm run build`.
```

---

## FASE 3 — Katalog Produk 3-Layer Dinamis & Product Detail Page (PDP) B2B

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 3)
Kamu bertindak sebagai **Principal Frontend/SSR Engineer & E-Catalog Information Architect**. Fokusmu pada Fase 3 adalah membangun mesin katalog B2B 3-lapis beserta halaman detail produk yang cepat, mendukung indeksasi URL bersarang secara SSR, dan mulus saat difilter di browser.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `docs/01-PRD.md` (kebutuhan `CAT-*` dan `PDP-*`)
2. `docs/02-SITEMAP-AND-APPFLOW.md` (State Machine Filter Katalog 3-Layer)
3. `docs/04-DATA-MODEL-AND-API.md` (Endpoint `/api/public/catalog/*` & struktur produk)

# TUGAS IMPLEMENTASI FASE 3
1. Bangun endpoint API publik katalog (`/api/public/catalog/categories`, `/api/public/catalog/subcategories`, `/api/public/catalog/labels`, `/api/public/catalog/products`) dengan validasi query parameter penuh.
2. Bangun halaman SSR + Client Interactive **Katalog Produk 3-Layer** yang menangani ketiga pola rute:
   - `/product-catalog`
   - `/product-catalog/[categorySlug]`
   - `/product-catalog/[categorySlug]/[subcategorySlug]`
3. Implementasikan perilaku lengkap 3-layer sesuai spesifikasi:
   - **Layer 1:** Tab Kategori (`Semua`, `Gadget`, `Payung`, `Stationery`, `Tumbler`).
   - **Layer 2:** Grup Chip Subkategori yang otomatis menyaring grup sesuai kategori aktif.
   - **Layer 3:** Filter Atribut/Label Spesifik Subkategori yang terbuka saat sebuah subkategori dipilih (dan menampilkan pesan petunjuk yang jelas saat belum ada subkategori dipilih).
   - Pencarian kata kunci/kode SKU, bar **Filter Aktif** dengan chip yang bisa dilepas satu-satu + tombol `Reset Semua`, laci filter responsif di mobile, sinkronisasi URL bersih tanpa reload penuh, penghitung total produk, paginasi 16 item/halaman, dan tombol pintas ke `/download-katalog`.
4. Bangun **Product Detail Page (`/product/[slug]`)**:
   - Breadcrumb berjenjang + `BreadcrumbList` & `Product` JSON-LD.
   - Galeri multi-gambar + **Pemilih Varian Warna** interaktif.
   - Informasi utama: Nama produk, kode SKU `LP-...`, badge jaminan (`Garansi 1 Tahun · QC Satu per Satu`), deskripsi B2B, chip pilihan warna & metode cetak.
   - Tombol utama **Minta Penawaran via WhatsApp** + sticky CTA bar di layar ponsel yang menyertakan Nama Produk, Kode SKU, dan Warna terpilih ke pesan WhatsApp.
   - Seksi **Pilihan Teknik Cetak Logo** khusus produk tersebut + **Tabel Spesifikasi Produk** lengkap (Ukuran, Berat, Warna, Material, Spesifikasi Teknis, MOQ, Area Logo, Garansi) + **Produk Serupa**.
5. Tambahkan unit test di Vitest untuk logika penyaringan 3-lapis, sinkronisasi slug URL, dan pembentukan pesan RFQ WhatsApp produk.

# VERIFIKASI WAJIB FASE 3
Jalankan `npm run typecheck`, `npm run lint`, `npm test`, dan `npm run build`. Pastikan semua rute dinamis katalog & PDP tervalidasi tanpa error.
```

---

## FASE 4 — Seminar Kit Finder 4-Dimensi, Pillar SEO Pages, Katalog PDF, Blog, FAQ & Legal

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 4)
Kamu bertindak sebagai **B2B Product Growth Engineer & Technical Content Architect**. Fokusmu pada Fase 4 adalah membangun fitur kurasi paket acara (*Seminar Kit Finder*), halaman pendaratan iklan/SEO berkonversi tinggi, pusat unduhan katalog PDF, blog edukasi B2B, pusat FAQ, serta dokumen legal korporat.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `docs/01-PRD.md` (kebutuhan `KIT-*`, `LND-*`, `PDF-*`, `BLG-*`, `FAQ-*`)
2. `docs/02-SITEMAP-AND-APPFLOW.md`
3. `docs/07-SEO-GEO-AEO-AND-ANALYTICS.md`

# TUGAS IMPLEMENTASI FASE 4
1. **Interactive Seminar Kit Finder (`/seminar-kit`):**
   - Seksi eksplorasi komponen item interaktif (*Tote Bag, Notebook A5, Pulpen Metal, Tumbler, Lanyard + ID Card, Payung Lipat, Powerbank, Flashdisk, Hardbox, Paper Bag*) yang menampilkan detail bahan & opsi cetak saat diklik.
   - Mesin filter paket 4 dimensi secara real-time: *Budget / Peserta*, *Jumlah Item*, *Jenis Acara*, dan *Packaging*, lengkap dengan penghitung paket cocok, tombol reset, dan CTA WhatsApp spesifik paket (`[data-wa-text]`).
2. **4 Pillar SEO / Google Ads Landing Pages:**
   - `/souvenir-kantor-premium`
   - `/souvenir-payung`
   - `/souvenir-notebook-custom`
   - `/powerbank-custom`
   Masing-masing dilengkapi ringkasan jawaban langsung GEO/AEO, tabel panduan pemilihan produk/teknik cetak, kurasi produk langsung dari repositori katalog, keunggulan QC/garansi, dan FAQ spesifik kategori.
3. **Download Katalog PDF (`/download-katalog`) + Endpoint `GET /api/public/catalog-pdfs`:** Menampilkan grid katalog PDF beserta sampul thumbnail dan tombol unduh aman.
4. **Blog & Artikel Edukasi B2B (`/blog` dan `/blog/[slug]`):** Daftar artikel dengan kategori/tanggal terbit, halaman baca artikel dengan tipografi nyaman, daftar isi otomatis, rekomendasi produk terkait, dan `Article` JSON-LD.
5. **Halaman FAQ (`/faq`)** dengan filter/grup topik + akordion aksesibel + `FAQPage` JSON-LD, serta halaman **Kebijakan Privasi (`/privacy`)** dan **Syarat & Ketentuan (`/legal` dengan anchor `#terms`)**.

# VERIFIKASI WAJIB FASE 4
Jalankan `npm run typecheck`, `npm run lint`, `npm test`, dan `npm run build`. Pastikan seluruh tautan di Header, Footer, dan internal linking antar-halaman mengarah ke rute yang hidup (nol 404).
```

---

## FASE 5 — Mesin Konversi: Email OTP Contact Form, Offline WA Ad-Ref (`LPY-XXXXX`), Sitemap & Security

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 5)
Kamu bertindak sebagai **B2B Growth Attribution & Application Security Engineer**. Fokusmu pada Fase 5 adalah mengimplementasikan formulir kontak anti-spam berverifikasi Email OTP, pelacakan atribusi konversi iklan offline ke WhatsApp (`LPY-XXXXX`), skrip analitik cerdas, serta kelengkapan SEO teknis & header keamanan produksi.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `docs/02-SITEMAP-AND-APPFLOW.md` (Sequence OTP & Flowchart WA Ad-Ref)
2. `docs/03-TECH-STACK-AND-ARCHITECTURE.md` (Security, CSP, Rate Limiting)
3. `docs/04-DATA-MODEL-AND-API.md` (Kontrak endpoint `/api/public/contact/*` & `/api/public/wa-ref`)
4. `docs/07-SEO-GEO-AEO-AND-ANALYTICS.md` (WA Greetings, Eager `gtag` + Deferred `GTM`)

# TUGAS IMPLEMENTASI FASE 5
1. **Sistem Formulir Kontak B2B Berverifikasi Email OTP (`/contact` + API):**
   - Implementasikan `POST /api/public/contact/otp/request`: validasi email & rate-limit per IP/email, hasilkan kode OTP 6 digit dengan masa berlaku 10 menit (disimpan ter-hash), kirim lewat layanan mailer (atau tampilkan ke log dev aman saat SMTP belum diatur).
   - Implementasikan `POST /api/public/contact/otp/verify`: validasi kecocokan OTP, batas maksimal percobaan salah (maks. 5x), dan terbitkan token bukti verifikasi berumur pendek.
   - Implementasikan `POST /api/public/contact/send`: wajib memvalidasi bukti verifikasi OTP email yang sama sebelum menyimpan data ke `contact_inquiries`.
   - Bangun UI `/contact` lengkap dengan modal OTP aksesibel, hitung mundur kirim ulang **60 detik**, dan pembatalan sesi OTP otomatis apabila pengguna mengubah input email setelah meminta OTP.
2. **Offline Google Ads → WhatsApp Conversion Attribution (`LPY-XXXXX`):**
   - Implementasikan `POST /api/public/wa-ref`: menerima `gclid`/`gbraid`/`wbraid`, `utm_*`, dan `landing_path`, menyimpan ke `wa_ad_refs`, mengembalikan kode unik `LPY-XXXXX` (`^LPY-[23456789ABCDEFGHJKLMNPQRSTUVWXYZ]{5}$`), dan menyetel cookie `lp_ref`.
   - Pasang client tracker ringan yang menerapkan aturan *last-click wins*, memilih sapaan WA kontekstual sesuai prefix URL halaman, dan menambahkan `(Ref: LPY-XXXXX)` ke seluruh CTA WhatsApp (termasuk CTA dinamis PDP & Seminar Kit) tanpa merusak karakter teks.
3. **Skrip Analitik & Technical SEO Lengkap:**
   - Komponen `AnalyticsScripts` yang memuat Google Ads `gtag.js` secara *eager* dan menunda `GTM/GA4` hingga interaksi pertama pengguna.
   - Generator dinamis `src/app/sitemap.ts` (`/sitemap.xml`) dan `src/app/robots.ts` (`/robots.txt` — blokir `/admin/`, `/api/`, `/uploads/`, serta bot scraper agresif seperti `Bytespider`).
   - Konfigurasi Security Headers (`Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: SAMEORIGIN`, `Referrer-Policy`, `Strict-Transport-Security`) di `next.config.ts`.
4. Tulis pengujian unit & integrasi Vitest untuk alur OTP (request, cooldown, salah kode, ubah email, send) dan generator/cookie `LPY-XXXXX`.

# VERIFIKASI WAJIB FASE 5
Jalankan `npm run typecheck`, `npm run lint`, `npm test`, dan `npm run build`. Pastikan semua tes keamanan input, OTP, dan atribusi WA lulus 100%.
```

---

## FASE 6 — Backoffice Admin CMS (`/admin`), Integrasi Database Penuh & E2E QA Audit

```markdown
# SEBAGAI APA KAMU BERTINDAK (FASE 6)
Kamu bertindak sebagai **Principal Full-Stack Systems Engineer & QA Lead**. Fokusmu pada Fase 6 adalah menyelesaikan panel pengelolaan internal **Liebe Pyrus Admin CMS (`/admin`)**, memastikan migrasi/seed database PostgreSQL berjalan mulus, serta menjalankan pengujian End-to-End dan audit kualitas akhir.

# BACA DOKUMEN INI TERLEBIH DAHULU
1. `docs/04-DATA-MODEL-AND-API.md` (Endpoint `/api/admin/*`)
2. `docs/06-ADMIN-CMS-SPEC.md`
3. `docs/08-IMPLEMENTATION-ROADMAP.md` (Checklist QA & Playwright)

# TUGAS IMPLEMENTASI FASE 6
1. **Autentikasi & Guard Admin (`/admin/login` & Middleware/Server Check):**
   - Login username/email + password ter-hash, sesi cookie `HttpOnly`, tombol logout bersih, dan proteksi wajib di setiap endpoint `/api/admin/*` (bukan sekadar menyembunyikan menu di UI).
2. **Modul-Modul Utama Admin CMS (`/admin`):**
   - **Dashboard Ringkasan:** Metrik total produk aktif, leads RFQ baru, log klik WA Ads, dan aktivitas terbaru.
   - **Kelola Kategori, Subkategori & Label Filter:** Tambah/ubah/urutkan/nonaktifkan kategori, subkategori, serta atribut filter Layer 3.
   - **Kelola Produk:** Tabel pencarian/filter produk + form tambah/edit produk (nama, slug, kode SKU `LP-...`, kategori/subkategori, deskripsi, varian warna, teknik cetak, nilai label filter, tabel spesifikasi, gambar, flag `Unggulan`/`Baru`, status publikasi) + konfirmasi hapus aman.
   - **Kelola Seminar Kit, Portofolio, Katalog PDF, Artikel Blog, & FAQ:** Operasi CRUD tervalidasi Zod + penanganan unggah gambar (WebP) dan dokumen katalog (PDF).
   - **Inbox Leads RFQ (`/admin/inquiries`):** Lihat detail pesan prospek korporat, ubah status progres sales (`Baru` → `Dihubungi` → `Penawaran Dikirim` → `Deal` / `Batal`), tambah catatan tindak lanjut.
   - **Log Atribusi WhatsApp Ads (`/admin/wa-refs`):** Pencarian kode `LPY-XXXXX` yang masuk ke chat sales untuk melihat asal `gclid` / `utm_campaign` + tombol **Unduh CSV** untuk upload konversi offline Google Ads.
   - **Pengaturan Situs (`/admin/settings`):** Ubah nomor WhatsApp aktif, email, telepon, alamat kantor, jam operasional, dan sapaan default WhatsApp.
   - **Jejak Audit (`audit_logs`):** Catat setiap perubahan penting yang dilakukan admin.
3. **Skrip Database & Dokumentasi Operasional:**
   - Sediakan skrip `db:generate`, `db:migrate`, dan `db:seed` di `package.json` untuk pengisian awal PostgreSQL produksi, sambil menjaga `DATA_SOURCE=seed` tetap berjalan mulus tanpa database eksternal.
4. **Pengujian End-to-End (Playwright) & Audit Akhir:**
   - Buat suite tes E2E utama: (a) Beranda → Katalog filter 3-layer → Detail Produk → verifikasi tautan WhatsApp berisi SKU, (b) Filter 4 dimensi di `/seminar-kit`, (c) Alur OTP form kontak, dan (d) Login Admin → kelola produk & cek status leads.
   - Perbarui `README.md` dengan petunjuk menjalankan aplikasi, variabel lingkungan, akun admin contoh untuk pengembangan lokal, dan perintah pengujian.

# VERIFIKASI AKHIR PROYEK
Jalankan berurutan: `npm run typecheck`, `npm run lint`, `npm test`, `npm run build`, dan uji E2E yang tersedia. Pastikan tidak ada error konsol, tidak ada link putus, dan seluruh spesifikasi di `docs/01-PRD.md` terpenuhi tuntas.
```
