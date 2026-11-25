# Spesifikasi Backoffice Admin CMS & Pengelolaan Leads — Liebe Pyrus B2B

**Versi Dokumen:** 1.0
**Tanggal:** 25 November 2026
**Mengacu ke:** [01-PRD.md](01-PRD.md), [04-DATA-MODEL-AND-API.md](04-DATA-MODEL-AND-API.md)

Dokumen ini merinci fungsionalitas, aturan validasi, alur CRUD, keamanan akses, serta mekanisme pengelolaan prospek (*leads*) dan atribusi iklan di dalam panel internal **`/admin`**.

---

## 1. Prinsip Dasar Panel Admin (`/admin`)

1. **Satu Aplikasi, Satu Sumber Data:** Panel `/admin` berada di dalam aplikasi yang sama (dilindungi rute & middleware sesi server), sehingga setiap perubahan produk, filter, atau nomor WhatsApp langsung tercermin pada halaman publik tanpa perlu *build* ulang kode.
2. **Keamanan di Lapisan Server:** Menyembunyikan tombol atau halaman di browser bukan pengamanan. Setiap endpoint `/api/admin/*` wajib memeriksa cookie sesi `HttpOnly` yang aktif; bila tidak valid, kembalikan `401 Unauthorized`.
3. ** Tidak Menghapus Tanpa Konfirmasi:** Setiap tindakan hapus kategori, produk, paket *seminar kit*, katalog PDF, atau artikel wajib menampilkan dialog konfirmasi yang menyebutkan nama item yang akan dihapus serta dampaknya (mis. kategori yang masih memiliki produk aktif tidak boleh dihapus paksa sebelum produk dipindahkan atau dinonaktifkan).
4. **Dukungan Draft / Nonaktif (`is_active`):** Admin dapat menyembunyikan sementara produk yang sedang kosong stoknya (`is_active = false`) tanpa harus menghapus data historis atau merusak struktur spesifikasi yang sudah diketik.

---

## 2. Rincian Modul Backoffice

### 2.1 Autentikasi (`/admin/login`)
- Form masuk menggunakan email/username dan password.
- Pembatasan percobaan gagal login (*rate-limit* maks. 5 percobaan gagal per 15 menit per IP).
- Tombol `Keluar` menghapus sesi dari database (`admin_sessions`) dan membersihkan cookie sesi.

### 2.2 Dashboard Ringkasan (`/admin`)
Menampilkan 4 kartu metrik utama beserta daftar tindakan cepat:
1. **Produk Aktif:** Jumlah total produk tayang per kategori utama.
2. **Inquiry Baru (`Status: Baru`):** Jumlah pesan masuk dari `/contact` yang belum ditindaklanjuti tim sales.
3. **Klik Iklan Teratribusi (`30 Hari Terakhir`):** Jumlah kode `LPY-XXXXX` baru yang tercipta dari trafik iklan.
4. **Katalog PDF & Artikel Aktif:** Pintasan cepat untuk memperbarui katalog PDF tahunan atau menerbitkan artikel baru.

### 2.3 Manajemen Kategori, Subkategori & Filter Layer 3 (`/admin/categories`)
Mengendalikan penuh perilaku halaman `/product-catalog`:
- **Kategori Utama:** Tambah/ubah nama, slug URL, deskripsi singkat, chip tag populer untuk Beranda, urutan tampil (`sort_order`), dan status aktif.
- **Subkategori:** Tambah/ubah subkategori di bawah kategori induk (mis. menambah subkategori *Tumbler Sport* di bawah *Tumbler*).
- **Editor Grup Filter Spesifik Subkategori (Layer 3):**
  - Pilih subkategori → tambah grup label (contoh: `Kapasitas`, `Material`, `Fitur`) → tambah pilihan nilai di dalamnya (contoh: `350 ml`, `500 ml`, `750 ml`).
  - Perubahan di sini otomatis muncul pada panel filter Layer 3 di halaman `/product-catalog/[kategori]/[subkategori]`.

### 2.4 Manajemen Produk B2B (`/admin/products`)
- **Daftar Produk:** Dilengkapi pencarian instan berdasarkan **Nama Produk** atau **Kode SKU (`LP-*`)**, filter kategori, filter status (`Aktif` / `Nonaktif` / `Unggulan`), serta tombol cepat ubah status tayang.
- **Form Tambah / Sunting Produk:**
  1. *Identitas Utama:* Nama produk, kode SKU unik (divalidasi berawalan `LP-`), slug URL otomatis (dapat disunting manual), Kategori & Subkategori.
  2. *Deskripsi GEO/AEO:* Deskripsi ringkas kartu & deskripsi lengkap produk (dilengkapi petunjuk penulisan faktual ≤ 60 kata di paragraf pembuka).
  3. *Parameter Pengadaan B2B:* `MOQ (pcs)`, `Area Cetak Logo (mm)`, `Garansi (bulan)`, badge (`Tidak Ada`, `Unggulan`, `Baru`), serta centang `Tampilkan di Produk Unggulan Beranda`.
  4. *Varian Warna:* Daftar warna (nama warna + pemilih kode warna hex) yang memunculkan pemilih warna di PDP.
  5. *Kompatibilitas Teknik Cetak:* Kotak centang dari 6 metode cetak in-house (`UV Digital Printing`, `Grafir Laser`, `Hot Stamping`, `Sablon`, `DTF UV`, `Laser 3D`) beserta catatan singkat hasil cetak pada produk tersebut.
  6. *Nilai Filter Layer 3:* Kotak centang atribut filter sesuai subkategori yang dipilih.
  7. *Tabel Spesifikasi Dinamis:* Baris `Label` – `Nilai` yang dapat ditambah, diubah urutannya, atau dihapus (mis. `Ukuran: 102.9 × 50 × 17.8 mm`, `Berat: 120 gr`, `Type-C Input: 5V/2.4A`).
  8. *Galeri Gambar:* Unggah multi-gambar (`.webp`/`.jpg`/`.png`), atur gambar utama (`is_primary`), dan isi `alt_text`.

### 2.5 Manajemen Seminar Kit (`/admin/seminar-kits`)
- Mengelola paket acara untuk halaman `/seminar-kit`:
  - Nama paket, rentang budget (`< Rp 50rb`, `Rp 50–100rb`, `Rp 100–200rb`, `Rp 200–400rb`, `> Rp 400rb`), jumlah item (`3`, `4`, `5`, `6+`), pilihan multi-acara (*Seminar, Konferensi, Workshop, Diklat Instansi, Gathering, Wisuda, Onboarding*), jenis kemasan (*Paper Bag, Tote Bag, Map Folder, Gift Box*), daftar komponen isi, foto paket, dan status aktif.

### 2.6 Manajemen Portofolio, Katalog PDF, Blog & FAQ
- **Portofolio (`/admin/portfolio`):** CRUD kartu proyek (nama produk, industri klien, nama klien/referensi, teknik cetak yang digunakan, foto hasil, dan opsi tampil di showcase Beranda).
- **Katalog PDF (`/admin/catalogs`):** Unggah file `.pdf` resmi beserta gambar sampul (`thumbnail`), ukuran file, urutan tampil, dan status aktif untuk halaman `/download-katalog`.
- **Artikel Blog (`/admin/blog`):** Editor Markdown bersih dengan pratinjau langsung, judul & deskripsi SEO, tag topik, tanggal terbit, dan status `Draft` / `Published`.
- **FAQ (`/admin/faqs`):** CRUD pertanyaan & jawaban per kelompok topik, ditambah centang `Tampilkan juga di halaman Layanan Cetak (/logo-details)`.

### 2.7 Inbox Leads RFQ (`/admin/inquiries`)
- Menampilkan seluruh permintaan konsultasi yang masuk melalui verifikasi OTP email di `/contact`.
- Kolom tampilan: Tanggal Masuk, Nama & Perusahaan, Kontak (klik langsung buka WhatsApp atau `mailto:`), Kategori Diminati, Kode Ref Iklan (`wa_ref_code` bila pengirim mendarat dari iklan), dan Status Tindak Lanjut.
- Panel detail memungkinkan tim sales mengubah status (`Baru` → `Dihubungi` → `Penawaran Dikirim` → `Deal` / `Batal`) dan menyimpan catatan tindak lanjut internal (`sales_notes`).

### 2.8 Log Atribusi Iklan WhatsApp (`/admin/wa-refs`)
- Memecahkan masalah klasik iklan B2B di mana prospek mengklik iklan Google lalu melanjutkan transaksi di WhatsApp:
  - Kotak pencarian cepat berdasarkan **Kode Referensi** (mis. ketik `LPY-K7M3P` yang muncul di ujung chat WhatsApp pelanggan).
  - Menampilkan detail asal klik: `gclid` / `gbraid` / `wbraid`, `utm_source`, `utm_medium`, `utm_campaign`, halaman pendaratan awal (`landing_path`), dan waktu pendaratan.
  - Tombol **Ekspor CSV** untuk diunggah kembali ke fitur *Google Ads Offline Conversion Import*.

### 2.9 Pengaturan Situs Global (`/admin/settings`)
- Mengubah konfigurasi operasional tanpa menyentuh kode:
  - Nomor WhatsApp Sales utama (format internasional bersih `628...` dan label tampilan `+62 8...`).
  - Nomor telepon kantor, email resmi, alamat lengkap showroom/kantor, link titik Google Maps, serta jam operasional.
  - Daftar sapaan otomatis WhatsApp per kategori halaman (`WA_GREETINGS`).

---

## 3. Pencatatan Audit (`audit_logs`)

Setiap operasi `POST`, `PATCH`, `PUT`, dan `DELETE` di `/api/admin/*` mencatat satu baris audit berisi:
- `admin_user_id` (pelaku perubahan)
- `action` (`CREATE`, `UPDATE`, `DELETE`, `STATUS_CHANGE`, `SETTINGS_UPDATE`)
- `entity_type` (`product`, `category`, `seminar_kit`, `inquiry`, `settings`, dll.)
- `entity_id`
- `summary` (ringkasan singkat perubahan dalam Bahasa Indonesia)
- `created_at` (waktu server UTC)
