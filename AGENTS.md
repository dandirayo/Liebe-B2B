# Repository Working Agreement — Liebe Pyrus B2B (`Liebe-B2B`)

Dokumen ini adalah kontrak kerja wajib bagi setiap AI Coding Agent maupun kontributor yang bekerja di repositori **`Liebe-B2B`**.

---

## 1. Ruang Lingkup & Sumber Kebenaran (*Source of Truth*)

1. Bekerja **hanya** di dalam direktori repositori `Liebe-B2B` kecuali pengguna memberi izin eksplisit tertulis untuk menyentuh jalur lain.
2. Jadikan dokumen spesifikasi berikut sebagai sumber kebenaran utama sebelum menulis atau mengubah kode:
   - [docs/01-PRD.md](docs/01-PRD.md) — Kebutuhan bisnis, persona, aturan B2B, dan prioritas fitur (`P0`/`P1`/`P2`).
   - [docs/02-SITEMAP-AND-APPFLOW.md](docs/02-SITEMAP-AND-APPFLOW.md) — Struktur rute URL, state filter 3-lapis, alur OTP, dan alur atribusi WA.
   - [docs/03-TECH-STACK-AND-ARCHITECTURE.md](docs/03-TECH-STACK-AND-ARCHITECTURE.md) — Arsitektur SSR, *dual-mode repository*, keamanan, dan konfigurasi lingkungan.
   - [docs/04-DATA-MODEL-AND-API.md](docs/04-DATA-MODEL-AND-API.md) — Skema tabel PostgreSQL, format SKU `LP-*`, kontrak payload API, dan struktur *seed data*.
   - [docs/05-DESIGN-SYSTEM-AND-BRAND.md](docs/05-DESIGN-SYSTEM-AND-BRAND.md) — Identitas visual **Liebe Pyrus**, token warna, tipografi, skala tombol/kartu, dan responsivitas.
   - [docs/06-ADMIN-CMS-SPEC.md](docs/06-ADMIN-CMS-SPEC.md) — Aturan CRUD panel `/admin`, validasi file unggahan, dan audit log.
   - [docs/07-SEO-GEO-AEO-AND-ANALYTICS.md](docs/07-SEO-GEO-AEO-AND-ANALYTICS.md) — Hukum konten GEO/AEO, skema `JSON-LD`, OpenGraph WhatsApp, dan loading analitik.
   - [docs/08-IMPLEMENTATION-ROADMAP.md](docs/08-IMPLEMENTATION-ROADMAP.md) — Urutan pengerjaan per fase dan *quality gates*.
3. Bila terjadi perbedaan antara dokumentasi dan implementasi kode yang sudah berjalan, **jangan memilih sepihak secara diam-diam** — laporkan perbedaannya dan konfirmasi ke pengguna.

---

## 2. Prinsip Arsitektur Tak-Boleh-Dilanggar (*Non-Negotiable Invariants*)

1. **Wajib Server-Rendered (SSR/SSG/ISR) untuk Seluruh Halaman Publik:**
   - Katalog, detail produk, landing page *seminar kit*, layanan, portofolio, tentang kami, FAQ, dan artikel blog **harus menghasilkan HTML utuh dari server** lengkap dengan tag `<title>`, `<meta name="description">`, `canonical`, OpenGraph (`og:*`), dan `<script type="application/ld+json">`.
   - Dilarang merender halaman publik sebagai *blank client-side SPA* yang baru memuat meta tag lewat JavaScript di browser.
2. **Dual-Mode Data Layer (`DATA_SOURCE=seed | database`):**
   - Seluruh pembacaan/penulisan data wajib melewati lapisan repositori/service terpusat (`src/server/repositories/`), bukan memanggil query SQL mentah langsung di dalam komponen UI.
   - Saat `DATA_SOURCE=seed` (default mode pratinjau lokal/staging awal), seluruh halaman publik, filter katalog 3-lapis, *seminar kit finder*, dan simulasi OTP/WA-Ref harus tetap berfungsi mulus menggunakan *seed data* realistis tanpa error koneksi database.
3. **B2B Lead Generation (Bukan Retail E-Commerce Cart):**
   - Jangan menambahkan keranjang belanja ritel satuan (*shopping cart* B2C) atau *payment gateway checkout* instan.
   - Semua konversi diarahkan ke **Request for Quotation (RFQ) via WhatsApp Kontekstual**, **Formulir Konsultasi B2B Berverifikasi OTP Email**, atau **Unduh Katalog PDF**.
4. **Keamanan Link WhatsApp (`wa.me`):**
   - Dilarang menyisipkan karakter emoji 4-byte (seperti `👋`, `📦`, `✨`) ke dalam parameter `?text=` pada URL `https://wa.me/...` karena redirect WhatsApp sering merusaknya menjadi karakter ``. Gunakan teks Bahasa Indonesia yang sopan, rapi, dan bersih.
   - Setiap tautan WhatsApp harus menghormati mekanisme penyisipan kode referensi iklan `(Ref: LPY-XXXXX)` apabila pengunjung memiliki cookie atribusi `lp_ref`.
5. **Kepatuhan Konten GEO/AEO:**
   - Setiap halaman publik wajib membuka bagian utamanya dengan kalimat jawaban langsung yang padat dan faktual (maksimal 60 kata), menyertakan angka spesifik yang dapat diverifikasi (mis. *SUS 304*, *MOQ 25 pcs*, *6 mesin cetak in-house*, *garansi resmi 12 bulan*), dan memastikan setiap subjudul `H2`/`H3` dapat dipahami mandiri saat dikutip oleh mesin AI.

---

## 3. Konsistensi UI, Desain & Aksesibilitas

1. Gunakan token warna, skala tipografi (`Plus Jakarta Sans` untuk judul & `DM Sans` untuk isi), radius sudut, dan tinggi kontrol dari [docs/05-DESIGN-SYSTEM-AND-BRAND.md](docs/05-DESIGN-SYSTEM-AND-BRAND.md).
2. Jangan menuliskan nilai warna hex sembarangan di komponen apabila token tema sudah tersedia.
3. Gunakan satu pustaka ikon secara konsisten (**Lucide**) dan SVG vektor bersih untuk ilustrasi teknis. Jangan menggunakan emoji sebagai pengganti ikon UI.
4. Pastikan antarmuka nyaman digunakan di **layar ponsel (`375px`)**, **tablet (`768px`)**, dan **desktop lebar (`1440px+`)**:
   - Target sentuh di layar `< 1024px` minimal tinggi `44px`.
   - Sediakan akses navigasi keyboard (`Tab`, `Escape` untuk menutup menu/modal, atribut `aria-expanded`, `aria-controls`, `aria-current="page"`), label eksplisit pada setiap input form, serta kontras warna minimal **WCAG 2.1 AA**.

---

## 4. Keamanan Lingkungan Kerja & Kerahasiaan

1. Jangan pernah menyimpan kredensial nyata, API key, password database, atau SMTP secret di dalam kode atau melakukan commit atas file `.env`. Selalu sediakan `.env.example` berisi nama variabel kosong/contoh aman.
2. Jangan menjalankan perintah destruktif seperti `git reset --hard`, `git clean -fd`, `push --force`, ataupun perintah penghentian proses sistem operasi (`taskkill`, `Stop-Process`, `kill`).
3. Jangan mengubah pengaturan sistem operasi Windows, registry, firewall, layanan sistem, atau memasang perangkat lunak tingkat global/administrator.
4. Saat menjalankan server pengembangan lokal, ikat ke `localhost` (`127.0.0.1`), bukan ke antarmuka jaringan publik.

---

## 5. Tindakan yang Memerlukan Persetujuan Eksplisit Pengguna

Minta konfirmasi pengguna terlebih dahulu sebelum:
- Menambah, menghapus, atau mengubah versi dependensi utama yang sudah terkunci di `package-lock.json` (setelah fase inisialisasi proyek selesai).
- Menjalankan migrasi destruktif pada database produksi atau menghapus tabel/kolom yang sudah berisi data.
- Menghapus file dokumentasi atau modul fitur yang memiliki isi substansial.
- Membuat `git commit`, branch baru, tag, pull request, atau melakukan `git push` ke repositori remote GitHub.
- Melakukan deployment ke server eksternal/produksi.

---

## 6. Kriteria Penyelesaian Tugas (*Definition of Done*)

Sebuah perubahan kode hanya dinyatakan selesai apabila:
1. Seluruh kebutuhan fungsional yang diminta telah diimplementasikan sesuai dokumen spesifikasi.
2. Pemeriksaan tipe (`npm run typecheck` / `tsc --noEmit`), linter (`npm run lint`), pengujian relevan (`npm test`), dan proses build (`npm run build`) telah dijalankan dan lulus tanpa error.
3. Tampilan dan interaksi telah diverifikasi pada mode mobile maupun desktop tanpa regresi layout atau error konsol.
4. Dokumentasi diperbarui apabila ada penambahan route, variabel `.env`, atau perubahan perilaku API.
5. Laporan akhir mencantumkan daftar file yang dibuat/diubah, perintah verifikasi yang dijalankan beserta hasilnya, serta asumsi atau tindak lanjut yang tersisa.
