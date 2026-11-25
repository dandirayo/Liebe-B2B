# Arsitektur Teknis, Keamanan & Hosting — Liebe Pyrus B2B

**Versi Dokumen:** 1.0
**Tanggal:** 25 November 2026
**Mengacu ke:** [01-PRD.md](01-PRD.md), [02-SITEMAP-AND-APPFLOW.md](02-SITEMAP-AND-APPFLOW.md)

Dokumen ini menetapkan keputusan arsitektur sistem, struktur direktori proyek, pola **Dual-Mode Data Repository**, kebijakan keamanan aplikasi web, serta strategi *staged deployment* dari pratinjau awal hingga produksi di VPS sendiri.

---

## 1. Mengapa Website B2B Ini Wajib Server-Rendered (SSR/ISR)

Berbeda dari aplikasi kasir atau operasional internal yang berada di balik halaman login, website **Liebe Pyrus** adalah ujung tombak akuisisi pelanggan B2B. Seluruh halaman publiknya wajib menghasilkan HTML utuh dari server karena tiga alasan krusial:

1. **Indeksasi Google Search & Halaman Katalog Bersarang:** Mesin pencari harus langsung melihat daftar produk, spesifikasi MOQ, breadcrumb, dan teks deskripsi pada `/product-catalog/gadget/powerbank` maupun `/product/...` tanpa menunggu eksekusi JavaScript berat di sisi klien.
2. **Kutipan Mesin Jawaban AI (*GEO / AEO*):** Crawler AI (ChatGPT Search, Google Gemini, Perplexity, Claude) mengurai HTML awal dan blok `JSON-LD` secara langsung; SPA kosong (`<div id="root"></div>`) sering diabaikan atau gagal dikutip secara akurat.
3. **Pratinjau Tautan WhatsApp (`OpenGraph`):** Tim *procurement* dan *Event Organizer* di Indonesia sangat sering membagikan tautan produk ke grup WhatsApp direksi/panitia. Crawler WhatsApp hanya membaca tag `<meta property="og:*">` dari respons HTML pertama server—tidak pernah mengeksekusi JavaScript browser.

---

## 2. Pilihan Arsitektur Utama vs Alternatif

### Opsi A — Next.js (App Router) Full-Stack TypeScript + PostgreSQL *(Direkomendasikan Utama)*

| Lapisan | Teknologi | Peran dalam Sistem |
| --- | --- | --- |
| Runtime & Bahasa | **Node.js LTS (≥ 22)** + **TypeScript (`strict: true`)** | Satu basis kode bertipe ketat untuk UI, SSR, dan REST API |
| Framework | **Next.js (App Router)** + **React 19** | SSR/ISR halaman publik, Route Handlers untuk `/api/public/*` & `/api/admin/*`, generator `sitemap.xml` & `robots.txt` bawaan |
| Styling | **Tailwind CSS v4** + CSS Custom Properties | Token warna, tipografi, dan komponen konsisten tanpa overhead CSS-in-JS |
| Form & Skema | **React Hook Form** + **Zod** | Validasi input form dan kontrak API di satu skema bersama |
| Database & ORM | **PostgreSQL 16+** + **Drizzle ORM** | Query SQL bertipe ringan, migrasi terukur, performa tinggi di VPS |
| Penyimpanan File | Disk lokal terproteksi (`/storage/uploads`) atau S3/MinIO | Menyimpan foto produk `.webp` dan file katalog `.pdf` |
| Pengiriman Email | **Nodemailer** (SMTP Korporat / Resend SMTP) | Mengirim kode OTP 6 digit pada `/contact` dan notifikasi *inquiry* baru |
| Pengujian | **Vitest** + **Testing Library** + **Playwright** | Unit test logika bisnis, integrasi endpoint API, dan uji alur E2E browser |

### Opsi B — Alternatif Terpisah: Node.js + Fastify SSR (Eta/EJS) + Admin React + PostgreSQL

Apabila di kemudian hari ingin dijalankan pada server mini dengan jejak memori ultra-kecil tanpa ekosistem Next.js:
- Halaman publik dirender oleh **Fastify** memakai template server ringan + modul JS interaktif khusus per halaman (pola yang juga dipakai oleh `meliaoptimus.co.id`).
- Semua aturan database PostgreSQL, kontrak REST API di [04-DATA-MODEL-AND-API.md](04-DATA-MODEL-AND-API.md), dan sistem desain di [05-DESIGN-SYSTEM-AND-BRAND.md](05-DESIGN-SYSTEM-AND-BRAND.md) **tetap 100% berlaku sama**.

> **Keputusan Default Proyek:** Menggunakan **Opsi A (Next.js App Router + TypeScript + Drizzle PostgreSQL)** karena menyatukan SSR publik, API publik, dan dashboard React `/admin` dalam satu proyek modern yang bersih dan cepat dibangun.

---

## 3. Pola Dual-Mode Data Repository (`DATA_SOURCE=seed | database`)

Agar proyek dapat langsung dijalankan, ditinjau tampilannya, dan diuji seluruh interaksinya bahkan **sebelum server PostgreSQL dinyalakan**, seluruh akses data wajib melewati antarmuka repositori di `src/server/repositories/`:

```mermaid
flowchart LR
    Pages["SSR Pages & Route Handlers (/api/*)"] --> RepoInterface["Repository Layer (CatalogRepo, LeadRepo, CmsRepo)"]
    RepoInterface --> EnvSwitch{"process.env.DATA_SOURCE"}
    EnvSwitch -- "seed (Default Pratinjau)" --> SeedStore["In-Memory / Seed Store (Data Lengkap Realistis)"]
    EnvSwitch -- "database (Produksi)" --> DrizzleDB["Drizzle ORM -> PostgreSQL"]
```

- **Mode `seed` (Default pengembangan awal & demo):**
  - Membaca koleksi data awal yang lengkap dari `src/server/seed/`.
  - Mendukung simulasi penuh filter katalog 3-lapis, filter *seminar kit*, pembuatan kode `LPY-XXXXX`, alur OTP email (kode OTP dicetak jelas di terminal server lokal untuk kemudahan uji), dan pratinjau halaman `/admin`.
- **Mode `database` (Staging & Produksi VPS):**
  - Membaca dan menulis secara persisten ke PostgreSQL dengan transaksi atomik dan pencatatan `audit_logs`.

---

## 4. Struktur Direktori Proyek Standar

```text
Liebe-B2B/
├── docs/                                   # PRD & 7 dokumen pendukung teknis
├── prompts/                                # Master Prompt & Phase Prompts
├── public/
│   ├── fonts/                              # Plus Jakarta Sans & DM Sans (.woff2 self-hosted)
│   └── images/                             # Placeholder/aset visual brand Liebe Pyrus (.webp/.svg)
├── src/
│   ├── app/
│   │   ├── (public)/                       # Group rute publik dengan Header & Footer SSR
│   │   │   ├── page.tsx                    # Beranda (/)
│   │   │   ├── product-catalog/            # /product-catalog, /[categorySlug], /[subcategorySlug]
│   │   │   ├── product/[slug]/page.tsx     # Detail Produk (PDP)
│   │   │   ├── seminar-kit/page.tsx        # Interactive Seminar Kit Finder
│   │   │   ├── souvenir-kantor-premium/    # Pillar Landing Page 1
│   │   │   ├── souvenir-payung/            # Pillar Landing Page 2
│   │   │   ├── souvenir-notebook-custom/   # Pillar Landing Page 3
│   │   │   ├── powerbank-custom/           # Pillar Landing Page 4
│   │   │   ├── logo-details/page.tsx       # Layanan Cetak 6 Mesin
│   │   │   ├── custom-design/page.tsx      # Persiapan Artwork & Mockup Gratis
│   │   │   ├── kualitas/page.tsx           # QC 1-per-1, Uji Lab SUS 304 & Garansi
│   │   │   ├── pengiriman/page.tsx         # Pengemasan, Pengiriman & Blind Dropship
│   │   │   ├── download-katalog/page.tsx   # Unduh Katalog PDF
│   │   │   ├── portfolio/page.tsx          # Portofolio Klien per Industri
│   │   │   ├── about-us/page.tsx           # Tentang Liebe Pyrus
│   │   │   ├── contact/page.tsx            # Form Konsultasi Berverifikasi OTP
│   │   │   ├── faq/page.tsx                # Pusat Tanya Jawab
│   │   │   ├── blog/                       # /blog & /blog/[slug]
│   │   │   ├── privacy/page.tsx            # Kebijakan Privasi
│   │   │   └── legal/page.tsx              # Syarat & Ketentuan (#terms)
│   │   ├── admin/                          # Backoffice Admin CMS (dilindungi Auth Guard)
│   │   ├── api/
│   │   │   ├── public/                     # Endpoint katalog, PDF, OTP kontak, wa-ref
│   │   │   └── admin/                      # Endpoint CRUD CMS, inbox leads, ekspor CSV
│   │   ├── robots.ts                       # Generator /robots.txt
│   │   └── sitemap.ts                      # Generator /sitemap.xml dinamis
│   ├── components/
│   │   ├── layout/                         # Header, MobileDrawer, Footer, StickyWaBar
│   │   ├── catalog/                        # Filter 3-layer, ProductCard, SpecTable, PrintMethods
│   │   ├── seminar-kit/                    # KitItemExplorer, KitFilterGrid
│   │   ├── contact/                        # ContactForm & OtpVerificationModal
│   │   ├── seo/                            # JsonLd, AnalyticsScripts, WaAttributionTracker
│   │   └── ui/                             # Button, Badge, Card, Accordion, Modal, Field
│   ├── config/
│   │   └── site.ts                         # Konfigurasi default identitas & sapaan WA Liebe Pyrus
│   ├── lib/
│   │   ├── whatsapp.ts                     # Pembentuk URL wa.me & penyisip (Ref: LPY-XXXXX)
│   │   ├── validation/                     # Skema Zod bersama (kontak, OTP, produk, kit)
│   │   └── utils.ts                        # Format teks, slugify, sanitasi
│   ├── server/
│   │   ├── auth/                           # Hash argon2, sesi cookie HttpOnly, guard admin
│   │   ├── db/                             # Koneksi PostgreSQL, schema.ts Drizzle, migrasi
│   │   ├── mail/                           # Pengirim email OTP & fallback dev logger
│   │   ├── rate-limit/                     # Pembatas laju request per IP & email
│   │   ├── repositories/                   # Implementasi Seed vs PostgreSQL
│   │   └── seed/                           # Dataset awal lengkap kategori, produk, kit, blog, FAQ
│   └── styles/
│       └── globals.css                     # Token warna, tipografi, komponen dasar Liebe Pyrus
├── tests/
│   ├── unit/                               # Tes Vitest (filter 3-layer, WA ref, OTP)
│   └── e2e/                                # Tes Playwright end-to-end
├── drizzle.config.ts
├── next.config.ts
├── package.json
└── tsconfig.json
```

---

## 5. Arsitektur Keamanan & Perlindungan Penyalahgunaan

1. **HTTP Security Headers Wajib (`next.config.ts`):**
   - `Content-Security-Policy`: Membatasi `default-src 'self'`, font dari `'self'`, frame hanya yang diizinkan (mis. Google Maps lokasi kantor bila diaktifkan & GTM), `object-src 'none'`, `base-uri 'self'`, `frame-ancestors 'self'`.
   - `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`
   - `X-Content-Type-Options: nosniff`
   - `X-Frame-Options: SAMEORIGIN`
   - `Referrer-Policy: strict-origin-when-cross-origin`
2. **Keamanan OTP Formulir Kontak:**
   - Kode OTP 6 digit dibangkitkan dengan generator acak kriptografis (`crypto.randomInt(100000, 999999)`).
   - Kode OTP **tidak pernah disimpan dalam teks telanjang** di database—selalu disimpan dalam bentuk hash SHA-256/HMAC beserta waktu kedaluwarsa (`10 menit`).
   - *Cooldown* kirim ulang minimal **60 detik**, batas maksimal permintaan **3 OTP per 10 menit** per alamat email / IP, dan hangus otomatis setelah **5 kali salah tebak**.
3. **Autentikasi Backoffice `/admin`:**
   - Password admin di-hash menggunakan **Argon2id**.
   - Sesi disimpan di tabel `admin_sessions` dengan token acak 256-bit di dalam cookie `HttpOnly; Secure; SameSite=Lax; Path=/`.
   - Setiap route handler `/api/admin/*` wajib memeriksa validitas sesi di server sebelum memproses pembacaan sensitif atau mutasi data.
4. **Keamanan Unggah File (Gambar Produk & Katalog PDF):**
   - Validasi ukuran maksimum (`≤ 5 MB` untuk gambar, `≤ 25 MB` untuk katalog PDF).
   - Pemeriksaan *magic bytes* file sebenarnya (hanya mengizinkan `image/webp`, `image/jpeg`, `image/png`, dan `application/pdf`), penamaan ulang file memakai UUID bersih, dan dilarang mengeksekusi skrip dari folder unggahan.

---

## 6. Variabel Lingkungan (`.env.example`)

```ini
# Mode Sumber Data: "seed" (pratinjau cepat tanpa DB) atau "database" (PostgreSQL produksi)
DATA_SOURCE="seed"

# Koneksi PostgreSQL (wajib saat DATA_SOURCE="database")
DATABASE_URL="postgresql://liebe_user:CHANGE_ME@127.0.0.1:5432/liebe_pyrus_b2b"

# URL Kanonik Situs Publik
NEXT_PUBLIC_SITE_URL="https://liebepyrus.co.id"

# Rahasia Kriptografi Sesi Admin & Token Verifikasi OTP (min. 32 karakter acak)
SESSION_SECRET="CHANGE_ME_WITH_64_HEX_RANDOM_CHARACTERS"

# Konfigurasi SMTP untuk Pengiriman OTP Email (jika kosong di dev lokal, OTP dicetak ke log server)
SMTP_HOST=""
SMTP_PORT="587"
SMTP_USER=""
SMTP_PASS=""
SMTP_FROM="Liebe Pyrus Indonesia <no-reply@liebepyrus.co.id>"
SALES_NOTIFICATION_EMAIL="hello@liebepyrus.co.id"

# Integrasi Analitik & Konversi Iklan (Opsional)
NEXT_PUBLIC_GOOGLE_ADS_ID=""
NEXT_PUBLIC_GTM_ID=""
```

---

## 7. Strategi Hosting Bertahap (*Staged Deployment*)

| Tahap | Lingkungan | Konfigurasi | Tujuan |
| --- | --- | --- | --- |
| **Tahap 1 — Pratinjau UI & Alur** | Lokal / Vercel / Cloudflare | `DATA_SOURCE=seed` | Meninjau desain **Liebe Pyrus**, kesempurnaan 15+ halaman, filter katalog 3-lapis, dan alur WA/OTP bersama pemilik bisnis tanpa biaya server DB |
| **Tahap 2 — Staging Internal** | VPS / Staging Server | `DATA_SOURCE=database` + PostgreSQL + SMTP uji | Mengisi foto produk asli **Liebe Pyrus**, mengunggah katalog PDF resmi, menguji Admin CMS & pengiriman email OTP sungguhan |
| **Tahap 3 — Produksi Penuh** | VPS Linux (Docker Compose: App + PostgreSQL + Caddy/Nginx) | SSL otomatis, backup harian `pg_dump` + folder `uploads/`, monitoring uptime | Melayani trafik organik SEO/GEO dan kampanye iklan Google Ads korporat |
