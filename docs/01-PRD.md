# Product Requirements Document (PRD) — Liebe Pyrus B2B

**Produk:** Platform Website B2B Liebe Pyrus (`PT Liebe Pyrus Indonesia`)
**Versi Dokumen:** 1.0
**Tanggal:** 25 November 2026
**Status:** Siap Implementasi
**Referensi Fungsional:** Kesetaraan penuh dengan platform katalog & *lead generation* B2B supplier merchandise korporat ([meliaoptimus.co.id](https://meliaoptimus.co.id/))

---

## 1. Ringkasan Eksekutif

**Liebe Pyrus** adalah platform web resmi **Company Profile, Katalog Produk Digital 3-Layer, Interactive Seminar Kit Finder, dan Mesin Akuisisi Prospek (*Lead Generation*) B2B** untuk penyedia *merchandise*, suvenir kantor, dan perangkat promosi custom logo perusahaan di Indonesia.

Berbeda dari toko *e-commerce* ritel satuan (*B2C*), pengadaan suvenir korporat membutuhkan kepastian ketersediaan stok partai besar, konsultasi pemilihan teknik cetak logo (*UV Print, Laser Engraving, Sablon, Hot Stamp, DTF UV, Laser 3D*), pembuatan *mockup* digital sebelum produksi massal, penawaran harga berjenjang sesuai *quantity*, jaminan kualitas satu per satu (*1-by-1 QC*), serta opsi pengiriman *blind dropship* bagi mitra *reseller*. Oleh karena itu, platform ini dirancang tanpa keranjang belanja instan, melainkan berfokus mengonversi pengunjung menjadi permintaan penawaran berkualitas tinggi (**RFQ**) melalui **WhatsApp Kontekstual Teratribusi** dan **Formulir Konsultasi Berverifikasi OTP Email**.

---

## 2. Masalah Bisnis & Solusi Produk

| Tantangan Pengadaan B2B Saat Ini | Dampak bagi Reseller & Korporasi | Solusi pada Website Liebe Pyrus |
| --- | --- | --- |
| Katalog statis PDF semata sulit dicari berdasarkan spesifikasi teknis (mis. kapasitas mAh, material SUS 304, ukuran) | Tim procurement/EO membuang waktu bertanya bolak-balik hanya untuk menyaring kandidat barang | **Katalog Web 3-Layer Dinamis** (Kategori → Subkategori → Filter Atribut Spesifik) + tetap menyediakan **Katalog PDF** bagi yang perlu presentasi internal |
| Terpisahnya pemasok barang polos dan vendor percetakan logo | Dua invoice, risiko salah cetak saling lempar tanggung jawab, waktu tunggu membengkak | Penonjolan jelas **6 Mesin Cetak In-House** (*Satu Vendor, Satu Tanggung Jawab, Satu Invoice*) di seluruh alur produk & layanan |
| Ketakutan *reseller* terhadap barang cacat atau identitas supplier bocor ke klien akhir | Reputasi *reseller* jatuh di mata korporasi atau klien diambil alih vendor | Halaman pembuktian **QC 4 Tahap Satu per Satu**, **Garansi Resmi 1 Tahun Elektronik**, dan **Blind Drop Shipping** atas nama *reseller* |
| Sulit menyusun paket acara (*seminar kit*) sesuai plafon anggaran per peserta | Panitia acara bingung mencocokkan isi item dan jenis kemasan dengan budget | **Interactive Seminar Kit Finder** dengan 4 filter (*Budget/Peserta, Jumlah Item, Jenis Acara, Packaging*) |
| Biaya iklan Google Ads terbuang karena konversi terjadi lewat chat WhatsApp (sulit dilacak) dan form kontak penuh spam bot | Tim marketing tidak tahu iklan mana yang menghasilkan *deal*; sales terganggu spam | **Offline Conversion Attribution (`Ref: LPY-XXXXX`)** otomatis di chat WhatsApp + **Verifikasi OTP Email** pada form kontak |

---

## 3. Tujuan & Bukan Tujuan (*Goals & Non-Goals*)

### 3.1 Tujuan Utama
1. Menyediakan seluruh kapabilitas fungsional setara referensi industri B2B merchandise dalam satu aplikasi web modern milik **Liebe Pyrus**.
2. Memastikan **100% halaman publik terindeks optimal** oleh Google Search dan *AI Answer Engines* (ChatGPT, Gemini, Perplexity, Google AI Overviews) melalui Server-Side Rendering (SSR), skema `JSON-LD`, dan aturan penulisan **GEO/AEO**.
3. Mempercepat proses seleksi barang hingga permintaan penawaran (RFQ) menjadi kurang dari **60 detik** dari pendaratan pengguna.
4. Memberikan kendali penuh kepada tim internal **Liebe Pyrus** melalui **Backoffice Admin CMS (`/admin`)** untuk memperbarui produk, filter, katalog PDF, portofolio, artikel blog, dan memantau *leads* serta atribusi iklan tanpa perlu mengubah kode.
5. Menjaga performa mobile kelas satu (**LCP < 2.0 detik**, **CLS < 0.05**) karena mayoritas klik iklan B2B di Indonesia berasal dari perangkat seluler dan dibagikan ulang melalui WhatsApp.

### 3.2 Bukan Tujuan (Fase Rilis Pertama)
- Keranjang belanja ritel satuan (*shopping cart*), hitung ongkir otomatis per 1 pcs, dan *payment gateway checkout* instan (karena harga grosir B2B dipengaruhi jumlah pesanan, jumlah titik/warna logo, dan kemasan custom).
- Aplikasi mobile native Android/iOS terpisah.
- Sistem ERP manufaktur/akuntansi gudang penuh di dalam website publik (CMS berfokus pada katalog, konten pemasaran, dan manajemen *leads* awal).

---

## 4. Persona Pengguna & Peran Sistem

| Persona / Peran | Perangkat Utama | Kebutuhan & Perilaku Utama |
| --- | --- | --- |
| **1. Mitra Reseller, Event Organizer (EO), & Creative Agency** | Ponsel & Laptop | Mencari barang cepat berdasarkan kode SKU & spesifikasi untuk diajukan ke tender klien; membutuhkan kepastian MOQ, area logo, garansi 1 tahun, QC 1-per-1, katalog PDF tanpa repot, dan pengiriman *blind dropship*. |
| **2. Corporate Buyer (Procurement, HR/GA, Marketing, Instansi)** | Laptop kantor & Ponsel | Mencari paket *onboarding kit*, *seminar kit*, atau suvenir VIP yang aman secara kualitas (mis. tumbler SUS 304 bersertifikat), desain dibantu gratis sampai *digital mockup*, dan pengiriman tepat jadwal acara. |
| **3. Admin Konten & Katalog Internal** | Laptop / Desktop | Mengelola kategori, subkategori, label filter teknis, produk & SKU, paket seminar kit, portofolio proyek, katalog PDF, FAQ, dan artikel blog lewat `/admin`. |
| **4. Tim Sales & Marketing B2B** | Laptop & Ponsel | Menindaklanjuti *leads* masuk dari form kontak berverifikasi OTP, mencocokkan kode `LPY-XXXXX` dari chat WhatsApp dengan data klik iklan Google Ads (`gclid`), dan mengekspor laporan CSV konversi. |

---

## 5. Aturan Bisnis Inti (*Core Business Rules*)

1. **Identitas Kode SKU (`LP-*`):** Setiap produk wajib memiliki kode SKU unik berawalan `LP-` (contoh: `LP-PB100-01` untuk Powerbank 10.000mAh, `LP-TMB304-02` untuk Vacuum Tumbler SUS 304, `LP-UMB-LP03` untuk Payung Lipat 3, `LP-NBK-A501` untuk Notebook Hardcover A5) agar tim sales dan klien tidak pernah salah merujuk varian barang.
2. **Minimum Order Quantity (MOQ):** Setiap produk mencantumkan nilai MOQ secara eksplisit pada tabel spesifikasi (standar umum: `25 pcs` untuk payung/tumbler premium tertentu, `50 pcs` untuk elektronik/gadget & stationery, `100 pcs` untuk pulpen promosi).
3. **6 Teknik Cetak Logo In-House:** Sistem mendukung pemetaan kompatibilitas produk terhadap 6 metode cetak in-house:
   - `UV Digital Printing` (full color tajam)
   - `Grafir Laser` / `Laser Engraving` (permanen elegan pada logam/kayu/kulit)
   - `Hot Stamping` (efek foil emas/perak pada kulit sintetis/agenda)
   - `Sablon` / `Silkscreen` (warna solid tahan lama & ekonomis partai besar)
   - `DTF UV` / `DTF Print` (detail warna penuh fleksibel)
   - `Laser 3D` (presisi permukaan khusus & kemasan)
4. **Persetujuan Digital Mockup Wajib:** Layanan persiapan *artwork* gratis mencakup penyesuaian ukuran, tata letak, pemisahan warna, dan *digital mockup*. Produksi massal dikomunikasikan berjalan **3–5 hari kerja setelah digital proof disetujui dan DP terkonfirmasi**.
5. **Standar Material & Garansi:**
   - Seluruh produk tumbler stainless wajib memenuhi minimal **Food-Grade SUS 304** (atau SUS 316 untuk seri khusus).
   - Seluruh produk kategori **Gadget/Elektronik** dilindungi **Garansi Resmi 12 Bulan (1 Tahun)** untuk cacat fungsi produksi dengan alur klaim satu pintu melalui Liebe Pyrus.
   - Setiap unit barang wajib melewati **4 Tahap QC Satu per Satu** (Visual, Uji Fungsional, Akurasi/Adhesi Logo, dan Kemasan) sebelum keluar gudang.
6. **Aturan Tautan WhatsApp & Kode Referensi Iklan:**
   - Tautan WhatsApp tidak boleh memuat emoji 4-byte agar tidak rusak saat *redirect* di berbagai perangkat.
   - Pengunjung dari iklan berparameter `gclid`, `gbraid`, atau `wbraid` memperoleh kode referensi `LPY-XXXXX` (aturan *last-click wins*) yang otomatis ditambahkan di ujung pesan WhatsApp. Pengunjung organik tidak diberi kode referensi tambahan.
7. **Kewajiban OTP Email pada Form Kontak:** Pesan dari halaman `/contact` hanya boleh disimpan ke kotak masuk sales apabila alamat email pengirim telah diverifikasi melalui kode OTP 6 digit yang masih berlaku. Mengubah input email sesudah meminta OTP otomatis membatalkan sesi OTP sebelumnya.

---

## 6. Rekomendasi Arsitektur Teknologi

Detail keputusan teknis dan alternatif dijelaskan lengkap di [03-TECH-STACK-AND-ARCHITECTURE.md](03-TECH-STACK-AND-ARCHITECTURE.md).

| Lapisan | Pilihan Utama | Alasan Bisnis & Teknis |
| --- | --- | --- |
| Bahasa Pemrograman | **TypeScript (`strict: true`)** | Satu tipe data konsisten dari database, API, hingga komponen UI |
| Framework Web | **Next.js (App Router, SSR/ISR)** | Menghasilkan HTML utuh dari server untuk SEO Google, kutipan AI (GEO/AEO), dan preview link WhatsApp instan |
| Styling & Komponen | **Tailwind CSS v4** + Design Tokens Liebe Pyrus | Ringan, konsisten, mudah dirawat tanpa ketergantungan CSS berat |
| Tipografi & Ikon | **Plus Jakarta Sans** + **DM Sans** (`.woff2` lokal) & **Lucide** | Bebas *layout shift*, cepat tanpa request font pihak ketiga, visual korporat bersih |
| Validasi & Form | **Zod** + **React Hook Form** | Skema validasi dipakai bersama di browser dan endpoint server |
| Database & ORM | **PostgreSQL** + **Drizzle ORM** (*Dual-Mode Seed/DB*) | Andal di VPS sendiri, mendukung mode pratinjau tanpa DB saat pengembangan awal |
| Keamanan & Sesi | Cookie `HttpOnly` + Hash `argon2` + Rate Limiter + `CSP` | Melindungi panel `/admin` dan mencegah penyalahgunaan pengiriman OTP |
| Pengujian | **Vitest**, **Testing Library**, **Playwright** | Menjamin logika filter 3-lapis, atribusi WA, dan OTP bebas regresi |

---

## 7. Matriks Kebutuhan Fungsional

Keterangan Prioritas:
- **P0:** Wajib tersedia dan berfungsi penuh sejak rilis utama (setara penuh dengan fitur inti website referensi).
- **P1:** Wajib untuk operasional pemasaran & pengelolaan mandiri tim internal.
- **P2:** Penyempurnaan lanjutan pasca-rilis awal.

### 7.1 Navigasi Global, Footer & Mesin WhatsApp (`NAV` & `WA`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `NAV-01` | Header sticky menampilkan logo **LIEBE PYRUS**, menu `Beranda`, dropdown `Produk` (kategori dinamis), dropdown `Layanan` (`Layanan Cetak`, `Custom Design`, `Kualitas`, `Pengemasan`, `Pengiriman`, `Download Katalog`), `Portfolio`, `Tentang Kami`, `Kontak`, dan tombol CTA `Lihat Katalog`. | P0 |
| `NAV-02` | Dropdown desktop memiliki jeda tutup halus (*close delay* 180–300ms) saat kursor keluar atau berpindah fokus keyboard, serta laci navigasi mobile (`drawer`) dengan overlay dan dukungan tombol `Escape`. | P0 |
| `NAV-03` | Footer menampilkan identitas brand, daftar kategori produk dinamis, tautan layanan (termasuk `Artikel` & `FAQ`), alamat berformat microdata `Schema.org/LocalBusiness` & `PostalAddress`, email, telepon, WhatsApp, jam operasional, serta tautan `/privacy` dan `/legal#terms`. | P0 |
| `WA-01` | Seluruh tombol CTA WhatsApp membentuk URL `https://wa.me/<nomor>?text=<pesan>` menggunakan sapaan Bahasa Indonesia yang menyesuaikan halaman aktif (mis. sapaan khusus payung saat berada di `/souvenir-payung` atau `/product-catalog/payung`), tanpa emoji 4-byte. | P0 |
| `WA-02` | Deteksi parameter iklan (`gclid`, `gbraid`, `wbraid`, `utm_source`, `utm_medium`, `utm_campaign`) pada pendaratan, kirim ke `POST /api/public/wa-ref`, simpan cookie `lp_ref` (`LPY-XXXXX`), dan tambahkan `(Ref: LPY-XXXXX)` ke seluruh tautan WhatsApp. | P0 |

### 7.2 Beranda (`HOM`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `HOM-01` | **Hero Section** dengan gambar `webp` responsif berprioritas tinggi (`fetchpriority="high"`), judul utama SEO/GEO, kalimat proposisi nilai satu tanggung jawab produk + cetak in-house, dan CTA `Lihat Katalog`. | P0 |
| `HOM-02` | **Client & Reseller Showcase (`Produk Kami, Nama Mereka`)** menampilkan kartu proyek/klien korporat terpercaya yang urutannya dapat diatur dari CMS. | P0 |
| `HOM-03` | **Why Liebe Pyrus Section** menampilkan 4 kartu nilai utama: (1) QC satu per satu tanggung jawab penuh, (2) 6 mesin cetak in-house satu invoice, (3) Garansi 1 tahun elektronik, (4) Kualitas menang tender. | P0 |
| `HOM-04` | **Kategori Produk Utama** menampilkan 4 kartu kategori (`Gadget`, `Stationery`, `Tumbler`, `Payung`) beserta chip subkategori populer dan tautan dalam teks ke `/souvenir-kantor-premium`, `/souvenir-payung`, serta `/seminar-kit`. | P0 |
| `HOM-05` | **Produk Unggulan Interaktif** menampilkan kartu produk pilihan berlabel `Unggulan` atau `Baru`, kode SKU `LP-*`, kategori, deskripsi ringkas, chip metode cetak logo, dan tautan ke halaman detail produk. | P0 |
| `HOM-06` | **Alur Kerja 5 Tahap** (`01 Pilih Produk`, `02 Kirim Desain Logo`, `03 Cetak In-House`, `04 Quality Check`, `05 Kirim ke Tujuan`) dan **Seksi Standar Kualitas** (SUS 304 teruji lab, QC 1-per-1, Garansi 1 Tahun) diikuti **CTA Penutup** (`Lihat Katalog` + `Hubungi Kami via WhatsApp`). | P0 |

### 7.3 Katalog Produk 3-Layer & Halaman Detail Produk (`CAT` & `PDP`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `CAT-01` | Mendukung rute bersih `/product-catalog`, `/product-catalog/[categorySlug]`, dan `/product-catalog/[categorySlug]/[subcategorySlug]` dengan SSR penuh saat pemuatan awal maupun navigasi langsung dari mesin pencari. | P0 |
| `CAT-02` | **Filter Layer 1 (Kategori)** & **Layer 2 (Grup Subkategori)**: Memilih kategori menyaring grup chip subkategori yang tampil; memilih subkategori memperbarui daftar produk dan membuka Layer 3. | P0 |
| `CAT-03` | **Filter Layer 3 (Label/Atribut Spesifik Subkategori)**: Menampilkan grup filter dinamis sesuai subkategori aktif (mis. kapasitas baterai, volume ml, jenis bahan, fitur khusus). Saat subkategori belum dipilih, layer ini menampilkan status nonaktif dengan instruksi jelas. | P0 |
| `CAT-04` | Bar **Filter Aktif** menampilkan chip semua filter yang sedang dipilih beserta tombol hapus per chip dan `Reset Semua`, disertai pencarian nama/SKU, laci filter mobile, penghitung jumlah produk ditemukan, paginasi (16 item/halaman), dan pintasan `Download Katalog PDF`. | P0 |
| `CAT-05` | Sinkronisasi URL browser otomatis saat pengguna mengganti kategori, subkategori, atribut filter, atau halaman paginasi sehingga tautan hasil filter dapat disalin dan dibagikan ke rekan tim. | P0 |
| `PDP-01` | Halaman `/product/[slug]` menampilkan breadcrumb lengkap, galeri foto produk, pemilih varian warna interaktif, nama produk, kode SKU `LP-*`, deskripsi GEO/AEO, dan jaminan `Garansi 1 Tahun · QC Satu per Satu`. | P0 |
| `PDP-02` | Menampilkan seksi **Pilihan Teknik Cetak Logo** yang relevan untuk produk tersebut beserta penjelasan hasil cetaknya, serta **Tabel Spesifikasi Produk** (Ukuran, Berat, Warna, Material, Spesifikasi Teknis, MOQ, Area Logo, Garansi). | P0 |
| `PDP-03` | Tombol utama **Minta Penawaran via WhatsApp** (serta *sticky bar* di ponsel) menyusun teks otomatis berisi nama produk, kode SKU, warna terpilih, dan kode `Ref` iklan bila ada, ditambah rekomendasi produk sejenis di bagian bawah halaman. | P0 |

### 7.4 Paket Seminar Kit & Pillar Landing Pages (`KIT` & `LND`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `KIT-01` | Halaman `/seminar-kit` menyediakan komponen interaktif **Isi Seminar Kit** (Tote Bag, Notebook A5, Pulpen Metal, Tumbler, Lanyard + ID Card, Payung Lipat, Powerbank, Flashdisk, Hardbox, Paper Bag) yang menampilkan spesifikasi bahan & opsi cetak saat dipilih. | P0 |
| `KIT-02` | **Filter Seminar Kit 4 Dimensi**: Pengguna dapat menyaring daftar paket berdasarkan *Budget/Peserta*, *Jumlah Item*, *Jenis Acara*, dan *Packaging* secara instan, lalu menekan CTA WhatsApp yang langsung menyebutkan nama paket pilihan. | P0 |
| `LND-01` | Menyediakan 4 halaman pendaratan tematik berkonversi tinggi: `/souvenir-kantor-premium`, `/souvenir-payung`, `/souvenir-notebook-custom`, dan `/powerbank-custom`, lengkap dengan panduan pemilihan, kurasi produk langsung dari katalog, dan FAQ topik terkait. | P0 |

### 7.5 Layanan, Katalog PDF, Portofolio, Tentang Kami, Kontak OTP, Blog & Legal (`SRV`, `RFQ`, `BLG`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `SRV-01` | `/logo-details`: Menampilkan 6 teknik cetak in-house, spesifikasi mesin cetak industri yang digunakan, galeri hasil cetak, alur kerja 5 langkah, dan akordion FAQ cetak logo. | P0 |
| `SRV-02` | `/custom-design`: Menampilkan cakupan bantuan artwork gratis (resize, variasi layout, pisah warna, digital mockup), panduan file Vector vs Raster 300 DPI, alur 4 langkah, dan perbandingan visual sebelum–sesudah mockup. | P0 |
| `SRV-03` | `/kualitas`: Menampilkan 4 tahap proses QC satu per satu, standar uji lab material tumbler SUS 304, dan mekanisme klaim garansi resmi 1 tahun produk elektronik. | P0 |
| `SRV-04` | `/pengiriman`: Menampilkan detail `#pengemasan` dan `#pengiriman` nasional, pilihan ekspedisi & kargo partai besar, estimasi 3–5 hari kerja, serta fasilitas **Blind Drop Shipping** atas nama mitra reseller. | P0 |
| `SRV-05` | `/download-katalog`: Memuat daftar katalog PDF dari `/api/public/catalog-pdfs` lengkap dengan gambar sampul dan tombol unduh langsung. | P0 |
| `SRV-06` | `/portfolio` & `/about-us`: Menampilkan portofolio hasil produksi lintas sektor industri dengan tombol *"Minta penawaran serupa →"*, serta profil perusahaan, filosofi nama **Liebe Pyrus**, nilai inti, dan fasilitas operasional. | P0 |
| `RFQ-01` | `/contact`: Formulir konsultasi B2B (*Nama Lengkap, Nama Perusahaan, WhatsApp/Telepon, Email, Kategori Diminati, Pesan*) wajib melalui **Modal Verifikasi OTP Email** (`request` → cooldown 60 detik → `verify` → `send`) dengan pembatalan sesi otomatis jika alamat email diubah di tengah jalan. | P0 |
| `BLG-01` | `/blog`, `/blog/[slug]`, `/faq`, `/privacy`, & `/legal`: Menyediakan pusat artikel edukasi pengadaan B2B, pusat tanya jawab terkelompok, kebijakan privasi, dan syarat ketentuan pemesanan korporat. | P0 |

### 7.6 Backoffice Admin CMS (`CMS`)

| ID | Kebutuhan Fungsional | Prioritas |
| --- | --- | --- |
| `CMS-01` | Login admin aman (`/admin/login`) berbasis sesi cookie `HttpOnly` dan pemeriksaan otorisasi server di seluruh endpoint `/api/admin/*`. | P1 |
| `CMS-02` | CRUD Kategori, Subkategori, serta grup Label & Nilai Filter spesifik per subkategori untuk mengendalikan katalog 3-lapis tanpa menyentuh kode. | P1 |
| `CMS-03` | CRUD Produk lengkap (identitas, SKU `LP-*`, gambar, varian warna, kompatibilitas cetak, nilai filter, tabel spesifikasi, status `Unggulan`/`Baru`, status aktif/draft). | P1 |
| `CMS-04` | CRUD Paket Seminar Kit, item Portofolio, file Katalog PDF, Artikel Blog, dan butir FAQ. | P1 |
| `CMS-05` | Inbox Leads Form Kontak (ubah status tindak lanjut sales & catatan) + Tabel Log Atribusi WhatsApp Ads (`LPY-XXXXX` ↔ `gclid`/`utm_*`) dengan fitur **Ekspor CSV** + Pengaturan Kontak Situs global. | P1 |
| `CMS-06` | Pencatatan otomatis aktivitas perubahan data penting oleh admin ke tabel `audit_logs`. | P2 |

### 7.7 SEO, GEO/AEO & Kebutuhan Non-Fungsional (`SEO` & `NFR`)

| ID | Kebutuhan Teknis & Kualitas | Target / Standar | Prioritas |
| --- | --- | --- | --- |
| `SEO-01` | Kepatuhan 4 Hukum Konten GEO/AEO pada semua halaman publik | Paragraf pembuka ≤ 60 kata menjawab langsung maksud halaman + minimal 1 data terukur per seksi `H2`/`H3` | P0 |
| `SEO-02` | Structured Data (`JSON-LD`) valid & lengkap | `Organization`, `LocalBusiness`, `WebSite`, `Product`, `BreadcrumbList`, `FAQPage`, `Article` | P0 |
| `SEO-03` | Preview tautan WhatsApp (`OpenGraph` `id_ID`) & Sitemap | `og:title`, `og:description`, `og:image` (1200×630), `sitemap.xml` dinamis, `robots.txt` (blokir `/admin`, `/api`, `/uploads`, `Bytespider`) | P0 |
| `NFR-01` | Core Web Vitals & Kecepatan Halaman Mobile | LCP < 2.0 detik, CLS < 0.05, INP < 200 ms; `gtag.js` dimuat *eager*, `GTM/GA4` dimuat *deferred* pada interaksi pertama | P0 |
| `NFR-02` | Keamanan Aplikasi & Anti-Penyalahgunaan | Header `CSP` ketat, `HSTS`, `nosniff`, `SAMEORIGIN`, rate-limit request OTP (maks. 3 kali per 10 menit per email/IP), validasi tipe MIME file unggahan | P0 |
| `NFR-03` | Responsivitas & Aksesibilitas Antarmuka | Tampil rapi dari lebar `360px` s/d `1920px+`, tinggi tombol sentuh mobile ≥ `44px`, navigasi keyboard penuh, kontras teks minimal WCAG 2.1 AA | P0 |
