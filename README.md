# Sistem Danus Kemahasiswaan — Web Dashboard Penjual

Platform Digital Sentralisasi Pemasaran Dana Usaha (Danus) Kemahasiswaan (Kelompok 4 — D4 TRPL Politeknik Negeri Cilacap).

## Tech Stack

- **Frontend:** Semantic HTML5, CSS3 (Flexbox & Grid), Vanilla JavaScript (DOM, Constraint Validation API, Fetch API)
- **Backend:** PHP Native (PDO Prepared Statements)
- **Database:** MySQL (via Laragon / XAMPP)

## Setup Lokal untuk Anggota Tim

1. Clone repositori ke folder web root (`C:\laragon\www\` atau `C:\xampp\htdocs\`).
2. Impor file `database.sql` ke phpMyAdmin (nama database: `danushub_db`).
3. Salin `config/database.example.php` menjadi `config/database.php`, lalu sesuaikan kredensial MySQL lokal Anda.
4. Akses aplikasi melalui `http://localhost/Sistem-Danus/` atau `http://sistem-danus.test/`.

## Dokumentasi

- Spesifikasi lengkap (PRD) tersedia di `docs/PRD_Web_Dashboard_Penjual_Danus.md`.

## Alur Kerja & Jadwal Pemicu Pengerjaan Tim

| Tahap | Branch | PIC Utama | Pemicu Mulai (Kapan Mulai Kerja?) | Output Utama |
| :---------: | :----------------------- | :------------------ | :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| **1** | `feature/db-security` | Hazel & Rifki | **Langsung mulai** (dari `dev`) | `database.sql`, `config/database.example.php`, `auth_guard.php`, `audit_logger.php` |
| **2** | `feature/ui-layout` | Tatag | **Langsung mulai paralel** (dari `dev`) | `includes/header.php`, `footer.php`, `assets/css/style.css` |
| **3** | `feature/auth` | Hazel | Setelah PR Tahap 1 di-merge ke `dev` | `login.php`, `register.php`, `logout.php`, `validasi.js` |
| **4** | `feature/katalog-crud` | Tatag & Hazel | Setelah PR Tahap 1 & 2 di-merge ke `dev` | `katalog.php`, `tambah_produk.php`, `edit_produk.php`, `hapus_produk.php` |
| **5** | `feature/rekap-api` | Rifki, Hazel, Tatag | Setelah PR Tahap 4 di-merge ke `dev` | `api/produk.php`, `api/rekap_pesanan.php`, `pesanan.php`, `dashboard.php`, `dashboard.js` |
| **6** | `docs/qa-testing` | Dea & Afdila | Persiapan **langsung mulai**; eksekusi setelah Tahap 3–5 di-merge ke `dev` | Bukti uji aktual UAT (`AC-01`–`AC-08`) & Security Testing (`TC-01`–`TC-12`) |

## Aturan Branching & Perintah Git Harian

> **Dilarang push langsung ke `main` atau `dev`.** Semua pengerjaan wajib di branch `feature/...` atau `docs/...`.

### Memulai tugas baru

```bash
git checkout dev
git pull origin dev
git checkout -b feature/nama-fitur
```

### Menyimpan progres harian

```bash
git add .
git commit -m "feat: deskripsi singkat perubahan"
git push origin feature/nama-fitur
```

### Membuat Pull Request

1. Buka repositori di GitHub.
2. Klik **"Compare & pull request"** pada branch yang baru di-push.
3. Arahkan target merge ke branch **`dev`** (bukan `main`).
4. Minta minimal **1 review** dari anggota tim lain sebelum merge.
