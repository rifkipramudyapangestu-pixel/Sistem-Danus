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
