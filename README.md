# Liebe Pyrus B2B — Corporate Merchandise & Souvenir Platform

**PT Liebe Pyrus Indonesia (`Liebe Pyrus`)** adalah platform website **Company Profile, Katalog Produk Digital 3-Layer, & Lead Generation B2B** untuk bisnis penyedia *merchandise*, suvenir korporat, *seminar kit*, dan barang promosi custom logo in-house.

Repositori ini memuat **Master Prompt AI**, **Prompt Eksekusi Bertahap (Fase 1–6)**, **Product Requirements Document (PRD)**, serta **7 dokumen cetak biru teknis & desain** untuk membangun aplikasi web **Liebe Pyrus** dari nol hingga siap produksi dengan kesetaraan fungsionalitas penuh terhadap standar industri supplier B2B terkemuka ([meliaoptimus.co.id](https://meliaoptimus.co.id/)).

---

## Ringkasan Kapabilitas Utama

| Pilar Fungsional | Cakupan Fitur |
| --- | --- |
| **Katalog Produk 3-Layer Dinamis** | Filter bertingkat *Kategori* → *Subkategori* → *Atribut/Label Spesifik Subkategori*, sinkronisasi URL ramah SEO (`/product-catalog/:kategori/:subkategori`), chip filter aktif, reset instan, dan paginasi. |
| **Product Detail Page (PDP) B2B** | Galeri multi-gambar, pemilih warna/varian, kode SKU (`LP-...`), rekomendasi teknik cetak logo per produk, tabel spesifikasi B2B lengkap (Ukuran, Berat, Material, MOQ, Area Logo, Garansi), dan tombol RFQ WhatsApp dinamis. |
| **Interactive Seminar Kit Finder** | Eksplorasi komponen isi *seminar kit* interaktif + filter 4 dimensi (*Budget/Peserta*, *Jumlah Item*, *Jenis Acara*, *Packaging*) beserta halaman landing SEO tematik. |
| **Halaman Layanan & Kredibilitas** | Layanan Cetak In-House 6 Mesin (`/logo-details`), Custom Design & Digital Mockup Gratis (`/custom-design`), Standar QC 1-per-1 & Uji Lab SUS 304 + Garansi 1 Tahun Elektronik (`/kualitas`), Pengemasan & Blind Dropshipping Nasional (`/pengiriman`), Portofolio per Industri (`/portfolio`), dan Unduh Katalog PDF (`/download-katalog`). |
| **Mesin Konversi & Anti-Spam** | Pelacakan konversi offline iklan Google Ads (`gclid`/`gbraid`/`wbraid`) ke kode referensi WhatsApp (`Ref: LPY-XXXXX`) + Formulir Kontak/RFQ B2B berproteksi **Verifikasi OTP Email** (cooldown 60 detik). |
| **Backoffice Admin CMS (`/admin`)** | Manajemen penuh Kategori, Subkategori, Label Filter, Produk & Varian, Seminar Kit, Portofolio, Katalog PDF, Artikel Blog, Inbox Leads RFQ, Log Atribusi Klik WA Ads, dan Pengaturan Situs. |
| **SEO, GEO/AEO & Performa Tinggi** | SSR/ISR untuk indeksasi instan, 4 Aturan Konten *Generative/Answer Engine Optimization*, `JSON-LD` lengkap (`Organization`, `LocalBusiness`, `Product`, `BreadcrumbList`, `FAQPage`, `Article`), OpenGraph khusus preview WhatsApp Indonesia, dan strategi pemuatan `gtag.js` *eager* + `GTM/GA4` *deferred*. |

---

## Struktur Repositori & Peta Dokumen

```text
Liebe-B2B/
├── README.md                                  # Gambaran umum proyek & panduan navigasi dokumen
├── AGENTS.md                                  # Kontrak kerja AI Agent khusus repositori Liebe-B2B
├── prompts/
│   ├── 00-MASTER-PROMPT.md                    # Master Prompt tunggal lengkap + Multi-Role Persona ("Sebagai Apa")
│   └── 01-PHASE-PROMPTS.md                    # 6 Prompt eksekusi bertahap (Fase 1 s/d Fase 6) untuk presisi tinggi
└── docs/
    ├── 01-PRD.md                              # Product Requirements Document (Persona, Aturan Bisnis, Matriks Fitur P0–P2)
    ├── 02-SITEMAP-AND-APPFLOW.md              # Arsitektur Informasi, Peta URL, State Machine Filter, & Diagram Alur
    ├── 03-TECH-STACK-AND-ARCHITECTURE.md      # Arsitektur SSR, Dual-Mode Data Layer, Keamanan (CSP/OTP), & Hosting Bertahap
    ├── 04-DATA-MODEL-AND-API.md               # ERD PostgreSQL (19 Tabel), Aturan Kode SKU, Seed Data, & Kontrak REST API
    ├── 05-DESIGN-SYSTEM-AND-BRAND.md          # Identitas Brand Liebe Pyrus, Palet Warna, Tipografi, & Skala Komponen UI
    ├── 06-ADMIN-CMS-SPEC.md                   # Spesifikasi Backoffice Admin CMS, CRUD, Validasi File, & Rekonsiliasi Leads
    ├── 07-SEO-GEO-AEO-AND-ANALYTICS.md        # Standar Konten GEO/AEO, Skema JSON-LD, Format WA, & Tracking Konversi
    └── 08-IMPLEMENTATION-ROADMAP.md           # Checklist Pengerjaan per Fase, QA Gates, Vitest, Playwright, & Lighthouse
```

---

## Cara Menggunakan Paket Prompt Ini

Tersedia **dua metode eksekusi** sesuai cara kerja AI Coding Agent yang Anda gunakan (Antigravity, Claude Code, Cursor, Windsurf, atau Codex):

### Metode A — Eksekusi Menyeluruh (*One-Shot Autonomous Build*)
1. Buka repositori `Liebe-B2B` sebagai workspace aktif di AI Coding Agent Anda.
2. Salin seluruh isi **[prompts/00-MASTER-PROMPT.md](prompts/00-MASTER-PROMPT.md)** dan jalankan.
3. AI Agent akan membaca seluruh dokumen spesifikasi di `docs/01-PRD.md` s/d `docs/08-IMPLEMENTATION-ROADMAP.md` sebagai *source of truth* dan membangun aplikasi secara terstruktur dari fondasi hingga verifikasi.

### Metode B — Eksekusi Bertahap per Fase (*Recommended untuk Kontrol Kualitas Maksimal*)
1. Buka **[prompts/01-PHASE-PROMPTS.md](prompts/01-PHASE-PROMPTS.md)**.
2. Jalankan **Prompt Fase 1**, tinjau hasil tampilan & verifikasi build, lalu lanjutkan berurutan hingga **Prompt Fase 6**:
   - **Fase 1:** Setup Proyek Next.js TypeScript, Sistem Desain *Liebe Pyrus*, Layout Global SSR, & *Dual-Mode Seed Repository*.
   - **Fase 2:** Homepage (8 Seksi Konversi) & Halaman Kredibilitas/Layanan In-House.
   - **Fase 3:** Katalog Produk 3-Layer Dinamis & Product Detail Page (PDP) B2B.
   - **Fase 4:** Interactive Seminar Kit Finder, Pillar SEO Pages, Download Katalog PDF, Blog, FAQ, & Legal.
   - **Fase 5:** Mesin Konversi (Email OTP Contact Form + Offline Ad-to-WhatsApp Ref Tracking `LPY-XXXXX`) & Technical SEO (`sitemap.xml`, `robots.txt`, `JSON-LD`).
   - **Fase 6:** Backoffice Admin CMS (`/admin`), Koneksi PostgreSQL + Drizzle ORM, & Pengujian Otomatis End-to-End.

---

## Rekomendasi Stack Utama

- **Framework & Rendering:** Next.js (App Router, SSR/ISR) + React 19 + TypeScript (`strict: true`)
- **Styling & UI:** Tailwind CSS v4 + CSS Design Tokens (`Plus Jakarta Sans` & `DM Sans` *self-hosted* `.woff2`) + Lucide Icons
- **Validasi & Form:** Zod + React Hook Form
- **Database & ORM:** PostgreSQL + Drizzle ORM *(dilengkapi Dual-Mode Repository sehingga Mode Pratinjau dapat berjalan langsung dengan data contoh lengkap tanpa server database)*
- **Email OTP & Keamanan:** Nodemailer / SMTP (dengan fallback log dev lokal), `argon2` password hashing, sesi cookie `HttpOnly`, rate limiter, dan `Content-Security-Policy` ketat
- **Pengujian:** Vitest + Testing Library + Playwright E2E

---

## Lisensi & Kepemilikan

Hak Cipta © PT Liebe Pyrus Indonesia / Repositori Internal `dandirayo/Liebe-B2B`. Seluruh dokumen dan kode di dalam repositori ini ditujukan khusus untuk pengembangan platform resmi **Liebe Pyrus**.
