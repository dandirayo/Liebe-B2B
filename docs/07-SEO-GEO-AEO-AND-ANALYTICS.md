# Standar SEO, GEO/AEO, OpenGraph WhatsApp & Analitik — Liebe Pyrus B2B

**Versi Dokumen:** 1.0
**Tanggal:** 25 November 2026
**Mengacu ke:** [01-PRD.md](01-PRD.md), [02-SITEMAP-AND-APPFLOW.md](02-SITEMAP-AND-APPFLOW.md)

Dokumen ini menetapkan aturan wajib optimasi mesin pencari tradisional (**SEO**), mesin pencari/jawaban berbasis AI (**GEO — Generative Engine Optimization** & **AEO — Answer Engine Optimization**), pratinjau tautan **WhatsApp**, serta arsitektur skrip pelacakan konversi iklan.

---

## 1. Empat Hukum Wajib Konten GEO / AEO

Saat ini tim *procurement* dan *Event Organizer* semakin sering mencari vendor melalui AI (ChatGPT, Google AI Overviews, Gemini, Perplexity) dengan kueri seperti *"Rekomendasi vendor merchandise kantor custom logo di Jakarta yang bisa cetak UV dan garansi"*. Agar halaman **Liebe Pyrus** dipilih dan dikutip langsung oleh mesin AI, setiap halaman publik wajib mematuhi 4 aturan berikut:

1. **Jawaban Langsung di Paragraf Pertama (Maksimal 60 Kata):**
   - Nyatakan secara eksplisit siapa **Liebe Pyrus**, apa yang disediakan halaman tersebut, dan keunggulan terukurnya dalam 1–2 kalimat pembuka sebelum penjelasan panjang.
   - *Contoh Buruk:* "Di era persaingan bisnis yang semakin ketat saat ini, memberikan hadiah kepada relasi merupakan tradisi penting yang telah lama dilakukan berbagai perusahaan..."
   - *Contoh Benar:* "**Liebe Pyrus** adalah supplier merchandise dan souvenir perusahaan di Jakarta dengan fasilitas 6 mesin cetak logo in-house (UV, Laser, Sablon, Hot Stamp, DTF). Melayani pesanan korporat dan mitra reseller mulai MOQ 25 pcs dengan QC satu per satu dan garansi elektronik 1 tahun."
2. **Gunakan Fakta & Angka Spesifik, Bukan Klaim Kabur:**
   - Ganti kata sifat abstrak (*"kualitas terbaik"*, *"proses sangat cepat"*, *"bahan super awet"*) dengan spesifikasi terverifikasi (*"material bagian dalam Stainless Steel SUS 304 teruji lab"*, *"estimasi cetak 3–5 hari kerja setelah approval mockup"*, *"resolusi file raster minimal 300 DPI"*).
3. **Setiap Subjudul `H2` / `H3` Harus Mandiri (*Self-Contained Passage*):**
   - Mesin AI mengutip potongan per subbagian, bukan satu halaman penuh. Pastikan setiap blok di bawah `H2`/`H3` dapat dipahami secara utuh tanpa harus membaca paragraf di seksi lain.
4. **Minimal Satu Metrik Terukur di Setiap Seksi Utama:**
   - Sertakan ukuran (mm/ml), kapasitas (mAh), jumlah minimum order (pcs), masa garansi (12 bulan), atau tahapan proses (4 tahap QC, 5 langkah pemesanan) di setiap seksi.

---

## 2. Standar Metadata & OpenGraph Khusus WhatsApp Indonesia

Setiap rute halaman wajib merender tag `<head>` unik di sisi server:

- `<title>`: `50–65 karakter`, memuat kata kunci utama + `| Liebe Pyrus Indonesia`.
- `<meta name="description">`: `135–160 karakter`, padat fakta (produk, custom logo, cetak in-house, garansi/QC).
- `<link rel="canonical" href="https://liebepyrus.co.id/..." />`: URL bersih tanpa parameter filter/iklan (`?gclid=...` tidak boleh ikut masuk ke canonical!).
- **OpenGraph untuk Pratinjau Chat WhatsApp (`id_ID`):**
  - `og:title`, `og:description`, `og:type` (`website` atau `article`), `og:url`, `og:locale="id_ID"`, `og:site_name="Liebe Pyrus Indonesia"`.
  - `og:image`: Gambar rasio `1.91:1` (`1200×630 px`), ukuran file `< 300 KB` (agar WhatsApp mobile mengunduh dan menampilkan *thumbnail preview* dalam hitungan milidetik tanpa gagal muat).

---

## 3. Matriks Skema Terstruktur (`JSON-LD`) per Halaman

| Tipe Halaman | Skema `@type` yang Wajib Disertakan |
| --- | --- |
| **Beranda (`/`)** | `Organization` + `LocalBusiness` + `WebSite` (dalam satu `@graph`) |
| **Katalog (`/product-catalog/...`)** | `CollectionPage` + `ItemList` + `BreadcrumbList` |
| **Detail Produk (`/product/[slug]`)** | `Product` (memuat `name`, `sku`, `image`, `description`, `brand: "Liebe Pyrus"`, `material`, serta `offers` B2B dengan `eligibleQuantity` MOQ) + `BreadcrumbList` |
| **Pillar Landing Pages & Layanan** | `Service` / `WebPage` + `BreadcrumbList` + `FAQPage` (bila memuat seksi tanya-jawab) |
| **Halaman FAQ (`/faq`)** | `FAQPage` (`mainEntity` daftar `Question` & `AcceptedAnswer`) |
| **Artikel Blog (`/blog/[slug]`)** | `Article` (`headline`, `datePublished`, `dateModified`, `author`, `publisher`, `image`) + `BreadcrumbList` |

---

## 4. Kamus Sapaan Kontekstual WhatsApp & Aturan Encoding

### 4.1 Larangan Karakter Emoji 4-Byte
Redirect `https://wa.me/...` pada sejumlah kombinasi browser mobile dan WhatsApp Desktop/Web dapat merusak karakter UTF-8 4-byte (seperti `👋` menjadi ``). Oleh sebab itu, **seluruh template pesan WhatsApp wajib hanya menggunakan karakter ASCII standar dan tanda baca bersih**.

### 4.2 Pemetaan Sapaan Otomatis Berdasarkan Halaman (`WA_GREETINGS`)

Urutan pencocokan dari prefix paling spesifik ke umum:

| Prefix Path Halaman | Teks Pre-fill Otomatis WhatsApp (Sebelum Penambahan Kode `Ref`) |
| --- | --- |
| `/product/[slug]` | `"Halo Liebe Pyrus, saya tertarik meminta penawaran untuk produk [Nama Produk] (Kode: [SKU], Warna: [Warna]) untuk kebutuhan perusahaan."` |
| `/seminar-kit` (klik paket tertentu) | `"Halo Liebe Pyrus, saya tertarik dengan paket [Nama Paket Seminar Kit] ([Budget Label]) untuk acara perusahaan."` |
| `/seminar-kit` (umum) | `"Halo Liebe Pyrus, saya ingin berkonsultasi mengenai paket seminar kit custom logo untuk acara perusahaan/instansi."` |
| `/souvenir-payung`, `/product-catalog/payung` | `"Halo Liebe Pyrus, saya ingin menanyakan penawaran souvenir payung custom logo untuk perusahaan."` |
| `/souvenir-notebook-custom`, `/product-catalog/stationery` | `"Halo Liebe Pyrus, saya ingin menanyakan penawaran souvenir notebook, agenda, dan stationery custom logo."` |
| `/powerbank-custom`, `/product-catalog/gadget` | `"Halo Liebe Pyrus, saya ingin menanyakan penawaran souvenir powerbank dan gadget elektronik custom logo."` |
| `/product-catalog/tumbler` | `"Halo Liebe Pyrus, saya ingin menanyakan penawaran souvenir tumbler stainless SUS 304 custom logo."` |
| `/souvenir-kantor-premium` | `"Halo Liebe Pyrus, saya ingin berkonsultasi mengenai paket souvenir kantor premium dan onboarding kit."` |
| `/logo-details`, `/custom-design` | `"Halo Liebe Pyrus, saya ingin berkonsultasi mengenai layanan cetak logo in-house dan persiapan mockup desain."` |
| *Default semua halaman lain* | `"Halo Liebe Pyrus, saya ingin menanyakan katalog dan penawaran produk souvenir custom untuk perusahaan."` |

Apabila pengunjung memiliki cookie atribusi iklan `lp_ref` (mis. `LPY-A7K2Q`), sistem otomatis merangkai di ujung kalimat:
`"... untuk perusahaan. (Ref: LPY-A7K2Q)"`.

---

## 5. Arsitektur Pemuatan Skrip Analitik Tanpa Mengorbankan LCP

Website B2B membutuhkan akurasi konversi iklan 100% sekaligus kecepatan buka instan di jaringan seluler:

1. **Google Ads Conversion Library (`gtag.js`) — Dimuat *Eager Async*:**
   - Diminta segera secara `async` saat halaman dimuat, sehingga apabila pengguna mobile langsung mengetuk tombol WhatsApp pada detik ke-1 setelah halaman tampil, fungsi pelacak konversi klik WhatsApp sudah siap dan tidak pernah kehilangan pencatatan (*zero race condition*).
2. **Google Tag Manager / GA4 (`gtm.js`) — Dimuat *Deferred on First Engagement*:**
   - Ditunda hingga terjadi interaksi nyata pertama pengguna (`scroll`, `pointerdown`, `touchstart`, `mousemove`, `keydown`, `click` dengan `{ once: true, passive: true }`) atau *fallback timer* `3500 ms`.
   - Strategi ini menjaga *Total Blocking Time* (TBT) mendekati `0 ms` dan skor Lighthouse Mobile Performance tetap di atas `95`.

---

## 6. Aturan `robots.txt` & `sitemap.xml`

- `robots.txt` mengizinkan seluruh perayap mesin pencari utama (`Googlebot`, `Bingbot`, `OAI-SearchBot`, `PerplexityBot`) merayapi halaman publik, tetapi memblokir:
  - `/api/`
  - `/admin/`
  - `/uploads/` (kecuali aset gambar publik yang memang diindeks lewat `/images/`)
  - Bot *scraper* pelatihan agresif yang membebani server tanpa memberi trafik rujukan, seperti `User-agent: Bytespider` (`Disallow: /`).
- `sitemap.xml` dihasilkan secara dinamis dari database/repositori sehingga setiap produk baru, subkategori baru, maupun artikel blog yang dipublikasikan dari `/admin` langsung terdaftar lengkap dengan `<lastmod>`.
