# Product Requirements Document (PRD)

## Platform Digital Sentralisasi Pemasaran Dana Usaha (Danus) Kemahasiswaan — Modul Web Dashboard Penjual

## 1. Informasi Dokumen & Konteks Proyek

| Komponen                           | Keterangan                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nama Produk**              | Platform Digital Sentralisasi Pemasaran Dana Usaha (Danus) Kemahasiswaan                                                                                                                                                                                                                                                                                                               |
| **Fokus Modul PRD**          | **Web Dashboard Penjual** (`WBS 1.2` sebagai MVP Utama, terintegrasi dengan `WBS 1.1`, `WBS 1.4`, `WBS 2`, dan lapisan *Security by Design*)                                                                                                                                                                                                                           |
| **Versi Dokumen**            | `v2.0` (Integrasi MPPL, Pemrograman Web, & Keamanan Informasi)                                                                                                                                                                                                                                                                                                                       |
| **Tanggal Penyusunan**       | 25 November 2026                                                                                                                                                                                                                                                                                                                                                                       |
| **Tim Pengembang**           | Kelompok Empat (4) — D4 Teknologi Rekayasa Perangkat Lunak, Politeknik Negeri Cilacap                                                                                                                                                                                                                                                                                                 |
| **Dosen Pengampu / Sponsor** | Joko Purwanto, S.T., M.Kom. (MPPL & Keamanan Informasi)                                                                                                                                                                                                                                                                                                                                |
| **Dokumen Baseline Acuan**   | **MPPL:** P1–P12 (*Charter, Scope, WBS, Schedule, Cost/Risk, Resource, Monitoring, Acceptance*)  **Pemrograman Web:** Modul P2–P13 (HTML5 Semantik, CSS Flexbox/Grid, JS DOM/Fetch, PHP PDO CRUD & JSON API)  **Keamanan Informasi:** Modul P1–P10 (*Security Property Map, SRS, Threat Model, Secure Design, Auth/Authz, Data Protection, Security Testing*) |

### 1.1 Latar Belakang & Pernyataan Masalah

Kegiatan pemasaran Dana Usaha (Danus) oleh Organisasi Mahasiswa (ORMAWA) dan Unit Kegiatan Mahasiswa (UKM) di lingkungan kampus masih mengandalkan pesan promosi di grup WhatsApp akademik serta media sosial. Pola ini menimbulkan tiga masalah utama:

1. Informasi produk Danus tersebar tidak terstruktur dan mengganggu komunikasi akademik (*spam*).
2. Pembeli (mahasiswa) kesulitan mencari produk berdasarkan kategori, lokasi gedung, dan status ketersediaan secara cepat.
3. Penjual (panitia Danus) membutuhkan waktu $30\text{–}60$ menit untuk merekapitulasi pesanan secara manual yang rawan *human error*, serta belum memiliki perlindungan akses, integritas data, dan jejak audit atas pengelolaan katalog maupun transaksi.

### 1.2 Tujuan Produk (Modul Web Dashboard Penjual)

Membangun aplikasi web yang **fungsional sekaligus aman (*Security by Design*)** bagi Panitia Danus ORMAWA/UKM untuk mengelola akun penjual secara aman berbasis peran (*role-based*), mengelola E-Katalog produk Danus (CRUD beserta status `Ready`/`PO`), mencatat jejak audit aktivitas sensitif (*Accountability*), serta mengotomatisasi rekapitulasi pesanan *Cash on Delivery* (COD) pada basis data relasional terpusat.

## 2. Pemangku Kepentingan, Aktor & Struktur Tim

| Aktor / Peran Sistem                        | Kategori                                                | Tanggung Jawab & Hak Akses Konseptual                                                                                                                                                                                                                                     |
| ------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Penjual** (`role: penjual`)       | Pengguna Utama Web Dashboard (Panitia Danus ORMAWA/UKM) | Mendaftar dan masuk ke Web Dashboard, mengelola (lihat, tambah, ubah, hapus) **hanya data produk E-Katalog miliknya sendiri**, memantau & memperbarui status pesanan COD miliknya, melihat rekapitulasi otomatis, serta meninjau riwayat aktivitas akunnya sendiri. |
| **Pembeli** (`role: pembeli`)       | Pengguna Mobile App / Konsumen API (Mahasiswa Umum)     | Hanya berhak melihat data katalog produk publik melalui *endpoint* JSON API (`/api/produk.php`) dan melakukan transaksi dari sisi Pembeli. **Dilarang mutlak** masuk atau memodifikasi data pada Web Dashboard Penjual.                                         |
| **Pengunjung / Anonim** (Belum Login) | Publik                                                  | Hanya dapat mengakses halaman `login.php`, `register.php`, dan data katalog publik (`GET /api/produk.php`). Seluruh halaman operasional Web Dashboard tertutup secara *default*.                                                                                  |
| **Dosen Pembimbing / Project Owner**  | Pengesah Formal (*Sponsor & Evaluator*)               | Memverifikasi kelulusan 8 *Acceptance Criteria* MPPL (`AC-01`–`AC-08`), standar implementasi Pemrograman Web, serta kepatuhan rancangan & pengujian Keamanan Informasi.                                                                                            |

### 2.1 Struktur Tim Pelaksana (Sesuai P10 MPPL)

| No | Nama Anggota            | NIM       | Peran dalam Pembangunan & Pengujian Web                                                                             |
| -- | ----------------------- | --------- | ------------------------------------------------------------------------------------------------------------------- |
| 1  | Rifki Pramudya Pangestu | 250215028 | Project Manager & System Analyst (Arsitektur DB, Kontrak API, Kueri Agregasi, Desain Otorisasi & Audit)             |
| 2  | Tatag Wildan Baihaqy    | 250215031 | UI/UX Designer & Frontend Web Developer (Semantic HTML5, CSS Grid/Flexbox, Antarmuka Web)                           |
| 3  | Hazel Ransy Krishna     | 250215018 | Backend Developer (Autentikasi PHP PDO, *Lockout & Session Timeout*, Logika CRUD, Upload File, API JSON)          |
| 4  | Dea Ameliana Saputri    | 250215011 | Business Analyst & QA Tester (Uji Fungsional `AC-01`–`AC-08`, *Security Testing Positive/Negative/Boundary*) |
| 5  | Afdila Dwiyani          | 250215001 | Researcher & Documentation Officer (Dokumentasi Pengujian, Laporan *Security Testing*, Kuesioner SUS)             |

## 3. Metrik Keberhasilan (Success Criteria)

| Indikator Keberhasilan                                | Target Terukur                                                                                                                                         | Sumber Acuan                      |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------- |
| **Acceptance Criteria Modul Web (`WBS 1.2`)** | $100\%$ ($8$ dari $8$ kriteria `AC-01` s.d. `AC-08` berstatus *Terpenuhi*)                                                                 | LK 12.3–12.5 MPPL                |
| **Efisiensi Waktu Rekapitulasi Pesanan**        | Waktu rekap otomatis $< 5$ menit (efisiensi $\ge 80\%$ dari $30\text{–}60$ menit manual)                                                        | Project Charter P4 MPPL           |
| **Target Adopsi & Uji Coba Lapangan (UAT)**     | Minimal $\ge 5$ akun penjual aktif dan $\ge 30$ transaksi COD tercatat di database                                                                 | Project Charter P4, WBS `4.2.1` |
| **Kualitas Pengalaman Pengguna (UX)**           | Skor evaluasi *System Usability Scale* (SUS) $\ge 70\%$                                                                                            | Requirement `R-09` P5 MPPL      |
| **Kepatuhan Keamanan Informasi**                | $100\%$ *Security Requirement* (`SR-01`–`SR-08`) terakomodasi dan lulus *Security Testing* (*Positive, Negative, Boundary*)               | Modul Keamanan Informasi P3–P10  |
| **Standar Kode Pemrograman Web**                | $100\%$ kueri memakai PDO *Prepared Statement*, $100\%$ *output* terproteksi `htmlspecialchars()` / `textContent`, validasi ganda JS + PHP | Modul Pemrograman Web P7–P13     |

## 4. Ruang Lingkup Produk (Scope Boundary)

### 4.1 In-Scope — Fase 1 (MVP Inti & Keamanan Dasar / Target Milestone M1: 27 November 2026)

Mencakup `WBS 1.1` (Basis Data Terpusat), `WBS 1.2` (Modul Inti Web Dashboard Penjual), dan fondasi *Security by Design*:

1. Skema database relasional MySQL terpusat (**5 tabel**: `users`, `products`, `orders`, `order_items`, dan **`activity_logs`**) serta koneksi PDO (`config/database.php`).
2. Sistem Registrasi, Login, Logout, pembatasan 5 kali gagal login (*lockout* 15 menit), *idle session timeout* 30 menit, pesan galat login generik, dan proteksi sesi khusus peran `penjual` (`R-01` / `WP 1.2.2`).
3. Manajemen CRUD E-Katalog lengkap milik penjual sendiri (*ownership check*): tampil daftar + pencarian/filter + *empty state* (`AC-06`), tambah produk + unggah foto maks. $2\text{ MB}$ (`AC-03`), ubah produk & status `Ready`/`PO` (`AC-04`), dan hapus produk dengan konfirmasi & transaksi PDO (`AC-05`).
4. Tata letak antarmuka Web Dashboard responsif (Semantic HTML5, CSS Flexbox & Grid) bebas *wrapping* tombol aksi pada layar $1366 \times 768\text{ px}$ (`R-09` / `AC-07`).
5. Pencatatan otomatis aktivitas sensitif (`LOGIN_FAILED`, `ACCESS_DENIED`, `CREATE_PRODUCT`, `UPDATE_PRODUCT`, `DELETE_PRODUCT`, `UPDATE_ORDER_STATUS`) ke tabel `activity_logs` tanpa pernah mencatat kata sandi.

### 4.2 In-Scope — Fase 2 (Rekapitulasi Otomatis & API JSON / Target Milestone M2: 18 Desember 2026)

Mencakup `WBS 1.4` (API & Integrasi) dan `WBS 2` (Modul Dashboard Rekapitulasi Pesanan Otomatis):

1. Halaman `dashboard.php` dengan 4 *Stat Cards* (Total Produk Aktif, Pesanan Hari Ini, Pesanan Menunggu, Total Omzet COD Hari Ini) dan tabel agregasi pesanan harian otomatis (`R-07` / `WP 2.1.1`–`2.2.1`).
2. Halaman `pesanan.php` bagi penjual untuk melihat daftar pesanan masuk COD miliknya dan memperbarui status (`Menunggu` $\to$ `Diproses` $\to$ `Selesai`).
3. Endpoint REST API JSON (`/api/produk.php` dan `/api/rekap_pesanan.php`) yang dikonsumsi via `fetch()` JavaScript sekaligus siap dipakai Mobile App (`R-10` / `WP 1.4.1`–`1.4.2`).
4. Indikator/lencana jumlah pesanan berstatus `Menunggu` sebagai notifikasi sederhana (`R-08`, prioritas *Could Have*) serta halaman `log_aktivitas.php` (*read-only*) untuk peninjauan riwayat aktivitas akun penjual sendiri.

### 4.3 Out-of-Scope (Dilarang Masuk Kode v1.0)

Mengacu pada *Scope Boundary* P5 MPPL:

* **`R-11`:** Integrasi *Payment Gateway* perbankan atau *e-wallet* otomatis pihak ketiga (fokus COD).
* **`R-12`:** Sistem *GPS Live Tracking* atau layanan kurir eksternal.
* **`R-13`:** Modul akuntansi keuangan dan laporan neraca laba-rugi kompleks.
* **Di luar lingkup Keamanan Informasi P10:** Tidak mencakup *penetration testing*, eksploitasi sistem, maupun implementasi algoritma kriptografi buatan sendiri (wajib menggunakan fungsi standar PHP seperti `password_hash()`).

## 5. Arsitektur Sistem & Keputusan Stack Teknologi

| Lapisan                          | Teknologi                                                                                                                                          | Justifikasi Penyelarasan 3 Mata Kuliah                                                                                            |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Struktur Halaman**       | HTML5 Semantik (`<header>`, `<nav>`, `<aside>`, `<main>`, `<section>`, `<footer>`, `<table>`, `<form>`)                            | Memenuhi Modul Pemrograman Web P2–P3 & aksesibilitas UI (`R-09`).                                                              |
| **Tata Letak & Styling**   | CSS3 Eksternal (`assets/css/style.css`): Box Model, **Flexbox**, **Grid**, pseudo-class `:valid`/`:invalid`                      | Memenuhi Modul Pemrograman Web P4–P5 & resolusi `AC-07` P12 MPPL.                                                              |
| **Interaktivitas Klien**   | Vanilla JavaScript ES6+ (`DOM API`, `addEventListener`, *Constraint Validation API*, `Event Delegation`, `fetch()`)                      | Memenuhi Modul Pemrograman Web P6, P7, & P13 (konsumsi JSON API tanpa `innerHTML` berbahaya).                                   |
| **Server-Side & Keamanan** | PHP Native 8.x (`$_POST`, `$_GET`, `$_FILES`, `$_SESSION`, `password_hash()`, `password_verify()`, `htmlspecialchars()`, CSRF Token) | Memenuhi Modul Pemrograman Web P8–P10 & kontrol keamanan Keamanan Informasi P5–P7.                                              |
| **Basis Data & Akses**     | MySQL / MariaDB (5 tabel terpusat) via **PHP PDO** (*Prepared Statements* & *Transactions*)                                              | Memenuhi Modul Pemrograman Web P12 & baseline `R-10` / `WP 1.1.2` MPPL (siap *deploy* dari XAMPP ke Hosting/VPS `N1` P9). |

## 6. Arsitektur Keamanan Informasi (Security by Design — P1 s.d. P9 Keamanan Informasi)

### 6.1 Inventaris Aset, Klasifikasi Data & Pemetaan 5 Security Properties (P1, P2, P7)

| ID Data | Aset / Data Aplikasi | Keadaan Data | Klasifikasi Data | Kepentingan Aset | C | I | A | Auth | Acc | Alasan & Dampak Jika Gagal |
| -------------- | --------------------------------------------------------------------------------- | --------------------------- | ------------------ | ---------------- | -- | -- | -- | ---- | --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **D-01** | **Kredensial Akun (`password_hash`) & Sesi Login** | Diproses, Disimpan, Dikirim | **Sensitif** | Tinggi | ✓ | ✓ | ✓ | ✓ | ✓ | Jika bocor atau ditebak, akun penjual dapat dikuasai (*Account Compromise*) untuk memanipulasi seluruh katalog dan pesanan. |
| **D-02** | **Data Pribadi & Kontak Pengguna (`email`, `no_wa`, `nama_lengkap`)** | Disimpan, Diproses, Dikirim | **Sensitif** | Tinggi | ✓ | ✓ | \- | ✓ | \- | Data pribadi pengguna; jika terbuka ke pihak tidak berhak (*Data Disclosure*) mengganggu privasi dan rawan disalahgunakan. Perlu dibaca kembali untuk koordinasi COD. |
| **D-03** | **Data E-Katalog & Harga Produk (`products`, foto)** | Disimpan, Diproses, Dikirim | **Publik** | Tinggi | \- | ✓ | ✓ | ✓ | ✓ | Ditampilkan untuk umum, namun perubahan harga/status tanpa hak (*Unauthorized Modification*) atau penghapusan (*Data Loss*) merusak kepercayaan pembeli dan transaksi. |
| **D-04** | **Data Transaksi & Rekap Pesanan COD (`orders`, `order_items`)** | Disimpan, Diproses, Dikirim | **Internal** | Tinggi | ✓ | ✓ | ✓ | ✓ | ✓ | Hanya milik penjual dan pembeli terkait; kebocoran atau manipulasi nominal/status menyebabkan kesalahan rekapitulasi keuangan panitia Danus. |
| **D-05** | **Catatan Aktivitas / Audit Trail (`activity_logs`)** | Disimpan, Diproses | **Internal** | Tinggi | ✓ | ✓ | \- | \- | ✓ | Bukti penelusuran pelaku atas perubahan harga, penghapusan produk, atau percobaan login gagal; jika dapat diubah pelaku, jejak pelanggaran hilang. |

*Keterangan Properti: **C** = Confidentiality, **I** = Integrity, **A** = Availability, **Auth** = Authenticity, **Acc** = Accountability.*

### 6.2 Spesifikasi Kebutuhan Keamanan (*Security Requirements* — P3)

| ID SR | Aset Terkait | Properti | Pernyataan Security Requirement (Dapat Diuji) | Jenis | Prioritas |
| --------------- | -------------------------------------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------------- |
| **SR-01** | `D-01` (Akun & Sesi) | `Auth` | Sistem harus memverifikasi identitas penjual dengan email dan kata sandi valid sebelum memberikan akses ke halaman terproteksi, menolak akses tanpa sesi aktif (termasuk pasca-*logout*), dan menampilkan pesan kegagalan login yang generik tanpa menyebut komponen mana yang salah. | Functional | **High** |
| **SR-02** | `D-01` (Akun & Sesi) | `Auth`, `A` | Sistem harus menolak pendaftaran dengan kata sandi kurang dari $8$ karakter, mengunci sementara percobaan login akun selama $15$ menit setelah $5$ kali gagal login berturut-turut, serta mengakhiri sesi secara otomatis setelah $30$ menit tidak ada aktivitas (*idle timeout*). | Functional | **High** |
| **SR-03** | `D-03` (E-Katalog) | `I`, `Auth` | Sistem harus membatasi operasi tambah, ubah, dan hapus data produk E-Katalog hanya bagi pengguna terautentikasi ber-role `penjual` dan hanya pada data produk yang dimiliki akun penjual tersebut (*ownership check* `seller_id`). | Functional | **High** |
| **SR-04** | `D-02`, `D-04` (Kontak & Pesanan) | `C`, `I` | Sistem harus membatasi akses lihat data pesanan COD, kontak pembeli terkait pesanan, dan perubahan status pesanan hanya kepada penjual pemilik transaksi terkait; permintaan lintas akun penjual wajib ditolak. | Functional | **High** |
| **SR-05** | `D-03` (Input Produk & File) | `I`, `A` | Sistem harus memvalidasi seluruh masukan di sisi server (harga wajib bilangan bulat $> 0$, status hanya `Ready`/`PO`, ekstensi foto hanya `jpg`/`jpeg`/`png`, ukuran foto $\le 2\text{ MB}$) dan menetralkan keluaran teks agar skrip berbahaya tidak dieksekusi di peramban. | Functional | **High** |
| **SR-06** | `D-05` (Audit Trail) | `Acc`, `I` | Sistem harus mencatat setiap aktivitas penting (`CREATE_PRODUCT`, `UPDATE_PRODUCT`, `DELETE_PRODUCT`, `UPDATE_ORDER_STATUS`, `LOGIN_FAILED`, `ACCESS_DENIED`) beserta identitas pelaku, waktu, target data, nilai sebelum/sesudah (untuk perubahan), dan hasilnya tanpa pernah mencatat kata sandi, serta bersifat *append-only* (tidak dapat diubah/dihapus melalui aplikasi). | Functional | **High** |
| **SR-07** | `D-01` (Kata Sandi) | `C` | Kata sandi pengguna tidak boleh disimpan dalam bentuk teks biasa (*plaintext*), melainkan wajib disimpan menggunakan algoritma *salted password hashing* standar (`password_hash()` PHP). | Non-Functional | **High** |
| **SR-08** | `D-01`, `D-02`, `D-04` (Data Kirim & Simpan) | `C`, `I` | Data kredensial login dan data pribadi sensitif wajib dikirim melalui kanal komunikasi terenkripsi (HTTPS/TLS pada lingkungan produksi/hosting), dan pesan kesalahan sistem tidak boleh membocorkan detail struktur basis data atau *stack trace* internal. | Non-Functional | **Medium** |

### 6.3 Prinsip Secure Design & Pemetaan Ancaman ke Kontrol (P4 & P5)

Empat prinsip *Secure Software Design* diterapkan secara konsisten di seluruh kode Web Dashboard:

1. **Least Privilege:** Setiap peran hanya mendapat izin minimum sesuai tugasnya. `Pembeli` dan `Pengunjung` hanya dapat membaca katalog publik; `Penjual` hanya mengelola produk dan pesanan miliknya sendiri (*ownership*), dan tidak diberi hak mengubah/menghapus `activity_logs` maupun akun orang lain.
2. **Defense in Depth:** Pengamanan berlapis pada setiap fitur kritis (Autentikasi sesi + Otorisasi peran & kepemilikan + Validasi sisi klien & server + PDO *Prepared Statement* + `htmlspecialchars()` + Audit *Logging*). Menyembunyikan tombol/menu di UI **tidak pernah** dijadikan satu-satunya kontrol akses.
3. **Secure Defaults:** Seluruh rute halaman dan *endpoint* bersifat **tolak secara *default*** (*deny by default*) kecuali secara eksplisit diizinkan; pada `register.php`, penetapan `role = 'penjual'` dikunci di sisi server dan tidak membaca input `role` dari formulir klien.
4. **Fail Secure:** Apabila pemeriksaan sesi, validasi ID, atau transaksi database PDO mengalami kegagalan/pengecualian, akses segera ditolak dan transaksi di-*rollback* sehingga sistem tetap berada pada kondisi tertutup dan konsisten.

#### Matriks Keterlacakan Ancaman ke Desain (*Threat-to-Design Traceability Matrix*)

| ID Threat | Aset | ID SR | Threat (P4) | Vulnerability yang Ditutup | Design Response & Prinsip (P5) | Security Control |
| -------------- | ------------------ | -------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **T-01** | `D-01` | `SR-01`, `SR-02` | *Account Compromise* & *Masquerading* | Tidak ada pembatasan percobaan gagal login; pesan error membedakan email/sandi salah; sesi tidak pernah kedaluwarsa. | Terapkan pesan gagal generik, *lockout* 15 menit setelah 5x gagal, *idle timeout* 30 menit, dan `session_regenerate_id(true)` (*Defense in Depth, Fail Secure*). | Authentication + Rate Limit/Lockout + Session Mgmt + Logging |
| **T-02** | `D-03` | `SR-03` | *Unauthorized Modification* & *Data Loss* | Otorisasi peran/kepemilikan hanya menyembunyikan tombol UI tanpa verifikasi server pada `edit_produk.php` & `hapus_produk.php`. | Terapkan `auth_guard.php` (cek role `penjual`) dan klausa wajib `AND seller_id = $_SESSION['user_id']` pada setiap kueri server + konfirmasi `POST` & CSRF token (*Least Privilege, Defense in Depth*). | Authorization (RBAC + Ownership) + CSRF + Logging |
| **T-03** | `D-02`, `D-04` | `SR-04` | *Unauthorized Access* & *Data Disclosure* | Parameter URL `?id=` pada pesanan atau API dapat diakses lintas akun penjual (IDOR). | Kunci seluruh kueri `SELECT`/`UPDATE` pesanan dan `api/rekap_pesanan.php` dengan identitas sesi `$_SESSION['user_id']`; tolak dengan `HTTP 403` jika tidak cocok (*Least Privilege, Fail Secure*). | Access Control (Ownership) + Logging (`ACCESS_DENIED`) |
| **T-04** | `D-03` | `SR-05` | *Unauthorized Modification* & *Service Disruption* | Input tidak divalidasi di sisi server (harga negatif/0, unggah skrip `.php` atau file besar, injeksi SQL/XSS). | Validasi ketat tipe data, rentang harga $> 0$, *whitelist* ekstensi `jpg/jpeg/png` $\le 2\text{ MB}$, PDO *Prepared Statement*, dan *output encoding* `htmlspecialchars()` (*Defense in Depth*). | Server-Side Validation + Parameterized Query + Output Encoding |
| **T-05** | `D-01` | `SR-07`, `SR-08` | *Data Disclosure* | Kata sandi tersimpan *plaintext* di database atau dikirim tanpa perlindungan kanal saat *deploy online*. | Simpan kata sandi hanya via *salted hashing* (`password_hash()`); wajibkan HTTPS/TLS saat *deployment* (*Defense in Depth*). | Salted Password Hashing + Secure Transport (TLS) |
| **T-06** | `D-05` | `SR-06` | *Unauthorized Modification* (Penghapusan Jejak) | Tidak ada pencatatan aktivitas perubahan data atau pengguna dapat menghapus log. | Buat tabel `activity_logs` *append-only* yang merekam pelaku, waktu, aksi, target, dan *snapshot* lama/baru tanpa antarmuka ubah/hapus log (*Accountability, Least Privilege*). | Audit Logging (*Append-Only*) |

### 6.4 Rancangan Autentikasi & Otorisasi — Role-Permission Matrix & Aturan Akses (P6)

#### A. Role-Permission Matrix (RBAC + Ownership)

| Fitur / Tindakan | Pengunjung (Belum Login) | Pembeli (`role: pembeli`) | Penjual (`role: penjual`) | Perlu Login? |
| --------------------------------------------------------------------------------- | ------------------------ | -------------------------------------------------------- | --------------------------------------- | ------------ |
| Registrasi & Login Akun Penjual (`register.php`, `login.php`) | Ya | Ya (dibatasi: login pembeli ditolak masuk Web Dashboard) | Ya | Tidak |
| Melihat Katalog Produk Publik (`GET /api/produk.php`) | Ya | Ya | Ya | Tidak |
| Membuka Dashboard & Rekap Otomatis (`dashboard.php`, `api/rekap_pesanan.php`) | Tidak | Tidak | **Ya (Sesuai Kepemilikan)** | **Ya** |
| Melihat Daftar E-Katalog Web (`katalog.php`) | Tidak | Tidak | **Ya (Sesuai Kepemilikan)** | **Ya** |
| Menambah Produk E-Katalog (`tambah_produk.php`) | Tidak | Tidak | **Ya** | **Ya** |
| Mengubah Produk & Status `Ready`/`PO` (`edit_produk.php`) | Tidak | Tidak | **Ya (Sesuai Kepemilikan)** | **Ya** |
| Menghapus Produk (`hapus_produk.php`) | Tidak | Tidak | **Ya (Sesuai Kepemilikan)** | **Ya** |
| Melihat & Mengubah Status Pesanan COD (`pesanan.php`) | Tidak | Tidak | **Ya (Sesuai Kepemilikan)** | **Ya** |
| Melihat Log Aktivitas Sendiri (`log_aktivitas.php`) | Tidak | Tidak | **Ya (Baca Saja, Milik Sendiri)** | **Ya** |
| Mengubah / Menghapus Log Aktivitas (`activity_logs`) | Tidak | Tidak | **Tidak** | N/A |

#### B. Aturan Akses Eksplisit & Respons Penolakan (`AR-01` s.d. `AR-05`)

| ID | Aturan Akses (Tingkat Fitur & Tingkat Data) | Alasan Keamanan | Respons Sistem Jika Dilanggar |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **AR-01** | Hanya pengguna yang telah terautentikasi dengan sesi valid (belum kedaluwarsa $< 30$ menit) yang dapat mengakses halaman Web Dashboard dan endpoint rekapitulasi. | *Authenticity* pelaku dan *Fail Secure*. | Tindakan tidak dijalankan; pengguna diarahkan (*redirect*) ke `login.php` (atau `HTTP 401` pada JSON API). |
| **AR-02** | Hanya pengguna ber-role `penjual` yang dapat mengakses halaman operasional Web Dashboard (`dashboard.php`, `katalog.php`, CRUD produk, `pesanan.php`). | *Least Privilege* dan pemisahan ruang kerja `R-01`. | Permintaan ditolak (`HTTP 403` / pesan *"Akses tidak diizinkan untuk peran Anda"*), data tidak berubah, kejadian dicatat ke `activity_logs` (`ACCESS_DENIED`). |
| **AR-03** | Penjual hanya dapat melihat, mengubah, atau menghapus data produk (`products`) dan pesanan (`orders`) yang memiliki `seller_id` sama dengan `$_SESSION['user_id']`. | *Integrity* & *Confidentiality* data lintas penjual (mencegah IDOR). | Permintaan ditolak, data tidak berubah sedikit pun, tampil pesan *"Data tidak ditemukan atau Anda tidak memiliki akses"*, kejadian dicatat (`ACCESS_DENIED`). |
| **AR-04** | Pada proses login gagal, sistem menampilkan pesan generik (*"Email atau kata sandi salah"*) dan mengunci akun selama $15$ menit setelah $5$ kali percobaan gagal beruntun. | Mencegah *account enumeration* dan *brute-force*. | Akses tetap tertutup (walau sandi benar saat masa kunci aktif); percobaan gagal dicatat di `activity_logs` (`LOGIN_FAILED`) **tanpa mencatat kata sandi**. |
| **AR-05** | Tidak ada peran pengguna di dalam aplikasi Web Dashboard yang diizinkan mengubah atau menghapus baris pada tabel `activity_logs`. | Menjaga *Integrity* & *Accountability* jejak audit. | Tidak disediakan fitur/endpoint ubah maupun hapus log; kueri aplikasi hanya melakukan `INSERT` dan `SELECT`. |

### 6.5 Rancangan Perlindungan Data — Data at Rest vs. Data in Transit (P7 / File P9)

| ID Keputusan | Data & Klasifikasi | Perlu Dibaca Kembali? | Mekanisme Perlindungan | Lokasi Perlindungan (*At Rest / In Transit*) | Alasan & Batasan Rancangan |
| --------------- | ------------------------------------------------------------------ | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **DD-01** | `D-01` Kata Sandi Penjual (**Sensitif**) | **Tidak** (hanya diverifikasi) | **Salted Password Hashing** (`password_hash($pw, PASSWORD_DEFAULT)` / bcrypt-Argon2) + verifikasi `password_verify()` | **At Rest:** Tersimpan sebagai hash + salt otomatis.  **In Transit:** Wajib HTTPS/TLS saat *deployment online*. | Sistem tidak pernah perlu membaca sandi asli; hashing satu arah mencegah pembacaan jika database bocor. *Batasan:* Tidak mencegah sandi lemah, sehingga dilapis minimal 8 karakter & *lockout* 5x gagal (`SR-02`). |
| **DD-02** | `D-02` Data Kontak (`email`, `no_wa`) (**Sensitif**) | **Ya** (untuk login & koordinasi COD) | **Kontrol Akses Ketat (RBAC + Ownership)** + perlindungan kanal kirim. **Dilarang di-hash** karena wajib dapat dibaca kembali. | **At Rest:** Dibatasi akses baca per pemilik & transaksi terkait (enkripsi *at rest* dipertimbangkan jika *deploy* produksi dengan kunci terpisah dari DB/kode).  **In Transit:** HTTPS/TLS pada produksi. | Hashing tidak sesuai karena data kontak harus ditampilkan untuk transaksi COD. *Batasan:* Pada pengujian lokal XAMPP (`http://localhost`), enkripsi transport TLS belum aktif dan dicatat sebagai keterbatasan lingkungan pengembangan. |
| **DD-03** | `D-03` Data E-Katalog & Harga (**Publik**) | **Ya** (ditampilkan ke seluruh pembeli) | **Kontrol Akses (RBAC + Ownership)** + Validasi Server + Audit Log (`activity_logs`). **Tidak dienkripsi/di-hash**. | **At Rest:** Teks terstruktur biasa dengan kontrol integritas.  **In Transit:** HTTPS/TLS pada produksi untuk mencegah modifikasi di jalur. | Data memang bersifat publik sehingga enkripsi kerahasiaan tidak menyelesaikan masalah utama (integritas harga). *Batasan:* Penjual sah yang salah input tetap bisa mengubah harga, sehingga dimitigasi validasi harga $> 0$ dan pencatatan nilai lama/baru di audit log. |
| **DD-04** | `D-04` & `D-05` Transaksi COD & Audit Log (**Internal**) | **Ya** (untuk rekap & penelusuran) | **Kontrol Akses Kepemilikan** + *Append-only* pada `activity_logs` + PDO *Prepared Statement*. | **At Rest:** Isolasi akses `seller_id`, tanpa fungsi edit/hapus log.  **In Transit:** HTTPS/TLS pada produksi. | Menjaga keakuratan omzet harian dan keutuhan bukti audit. *Batasan:* Tidak melindungi dari akses langsung administrator server/phpMyAdmin secara fisik (*out of app scope*). |

*Catatan Pengelolaan Kunci:* Pada versi MVP v1.0, enkripsi simetris kolom database belum diaktifkan karena data sensitif utama (`password`) menggunakan *salted hashing* satu arah (`DD-01`), sedangkan data kontak (`DD-02`) dan data publik/internal (`DD-03`, `DD-04`) mengutamakan kontrol akses dan kanal TLS. Jika enkripsi kolom diterapkan pada pengembangan lanjutan, kunci rahasia **wajib disimpan di *environment variable* (`.env`) di luar repositori Git dan terpisah dari basis data** agar kebocoran database tidak serta-merta membocorkan kunci dekripsi.

## 7. Spesifikasi Kebutuhan Fungsional & Keterlacakan (MPPL + Web + Keamanan)

### 7.1 F-WEB-01 — Registrasi Akun Penjual (`register.php`)

* **Traceability:** `R-01` (`WP 1.2.2`) | `AC-01`, `AC-08` | `SR-02`, `SR-07`
* **Input (`POST`):** `nama_lengkap` (wajib, min 3 karakter), `nama_organisasi` (wajib), `email` (wajib, format valid, unik), `no_wa` (wajib, 10–15 digit angka), `password` (wajib, **minimal 8 karakter**), `confirm_password` (cocok *real-time* via JS).
* **Logika Server:** `trim()` semua teks, validasi ulang semua aturan di PHP, cek duplikasi email via PDO, hash kata sandi via `password_hash($password, PASSWORD_DEFAULT)`, paksa `role = 'penjual'` di kode server (bukan dari `$_POST`), simpan via PDO `INSERT`, dan tampilkan konfirmasi sukses.

### 7.2 F-WEB-02 — Login, Lockout, Session Timeout & Logout (`login.php`, `logout.php`, `includes/auth_guard.php`)

* **Traceability:** `R-01` (`WP 1.2.2`) | `AC-02` | `SR-01`, `SR-02`, `SR-06`, `AR-01`, `AR-02`, `AR-04`
* **Aturan Login:**

  1. Periksa kolom `locked_until` pada tabel `users`: jika masih di masa depan (`locked_until > NOW()`), tolak login dengan pesan *"Akun dikunci sementara karena terlalu banyak percobaan gagal. Silakan coba lagi setelah 15 menit."* (meski sandi benar).
  2. Verifikasi kredensial via `password_verify()`. Jika email tidak ditemukan **atau** sandi salah, tampilkan **pesan generik** (*"Email atau kata sandi tidak valid."*), naikkan `failed_login_attempts`, jika mencapai $5$ set `locked_until = NOW() + 15 menit`, dan catat kejadian `LOGIN_FAILED` ke `activity_logs` **tanpa menyimpan nilai password**.
  3. Jika kredensial benar namun `role !== 'penjual'`, tolak akses ke Web Dashboard, tampilkan pesan penolakan peran, dan catat `ACCESS_DENIED`.
  4. Jika valid dan `role === 'penjual'`, reset `failed_login_attempts = 0`, `locked_until = NULL`, jalankan `session_regenerate_id(true)`, simpan `user_id`, `nama_lengkap`, `nama_organisasi`, `role`, `last_activity = time()`, dan buat `csrf_token`.
* **Penjaga Sesi (`includes/auth_guard.php`):** Dipasang di baris pertama setiap halaman terproteksi. Memeriksa keberadaan sesi, `role === 'penjual'`, dan **idle timeout** (`time() - $_SESSION['last_activity'] > 1800` detik / $30$ menit $\to$ hancurkan sesi & *redirect* ke `login.php?timeout=1`). Memperbarui `last_activity` pada setiap permintaan sah.

### 7.3 F-WEB-03 — Tampilan Daftar E-Katalog, Pencarian & Empty State (`katalog.php`)

* **Traceability:** `R-02`, `R-09` (`WP 1.2.3`) | `AC-06`, `AC-07` | `SR-03`, `SR-05`
* **Spesifikasi:** Menampilkan produk dengan `WHERE seller_id = :seller_id ORDER BY created_at DESC`. Menyediakan filter pencarian `GET`/JS (nama, kategori, status `Ready`/`PO`), tombol **"+ Tambah Produk"**, dan tabel semantik 7 kolom (Foto, Nama, Kategori, Harga, Lokasi Gedung, Status *Badge*, dan Aksi).
* **Resolusi Remarks P12:**

  * **`AC-06` (*Empty State*):** Jika data $= 0$, tampilkan pesan *"Belum ada produk Danus di katalog Anda. Yuk, tambahkan produk pertama agar mahasiswa dapat mulai memesan!"* disertai tombol pintasan **"Tambah Produk Pertama"** menuju `tambah_produk.php`.
  * **`AC-07` (*Layout Tabel*):** Kolom **Aksi** menggunakan `white-space: nowrap; display: flex; gap: 8px;` agar tombol **Edit** dan **Hapus** tetap sejajar horizontal tanpa *wrapping* pada layar $1366 \times 768\text{ px}$.

### 7.4 F-WEB-04 — Tambah Produk E-Katalog (`tambah_produk.php`)

* **Traceability:** `R-02`, `R-10` (`WP 1.2.3`) | `AC-03`, `AC-08` | `SR-03`, `SR-05`, `SR-06`
* **Input (`POST`, `enctype="multipart/form-data"` + `csrf_token`):** `nama_produk`, `kategori` (`Makanan Berat`, `Camilan`, `Minuman`, `Merchandise`), `harga` (bilangan bulat $> 0$), `lokasi_gedung`, `status_ketersediaan` (`Ready` / `PO`), `foto` (`accept=".jpg,.jpeg,.png"`), `deskripsi` (opsional).
* **Validasi Server & Keamanan:** Verifikasi CSRF token; validasi semua kolom wajib tidak kosong; `harga > 0`; cek `$_FILES['foto']['error'] === UPLOAD_ERR_OK`; validasi *whitelist* ekstensi (`jpg`, `jpeg`, `png`) + cek MIME (`finfo_file` / `getimagesize`) + ukuran $\le 2\text{ MB}$ ($2 \times 1024 \times 1024$ byte); simpan file dengan nama acak unik ke `uploads/products/`; eksekusi PDO `INSERT` dengan `seller_id = $_SESSION['user_id']`; catat `CREATE_PRODUCT` ke `activity_logs`.

### 7.5 F-WEB-05 — Ubah Produk & Status Ready/PO (`edit_produk.php`)

* **Traceability:** `R-02`, `R-10` (`WP 1.2.3`) | `AC-04`, `AC-08` | `SR-03`, `SR-05`, `SR-06`, `AR-03`
* **Logika Server:** Validasi `$_GET['id']` (`FILTER_VALIDATE_INT`); ambil data lama via `SELECT * FROM products WHERE id = :id AND seller_id = :seller_id`. Jika kosong (tidak ada atau milik penjual lain), catat `ACCESS_DENIED` dan tampilkan pesan penolakan aman. Isi formulir dengan nilai lama terbungkus `htmlspecialchars()`. Foto baru bersifat opsional (jika kosong, pertahankan `foto_path` lama). Saat `POST`, validasi CSRF & input, jalankan `UPDATE ... WHERE id = :id AND seller_id = :seller_id`, lalu catat `UPDATE_PRODUCT` ke `activity_logs` beserta `old_value` dan `new_value` (harga & status sebelum/sesudah).

### 7.6 F-WEB-06 — Hapus Produk (`hapus_produk.php`)

* **Traceability:** `R-02`, `R-10` (`WP 1.2.3`) | `AC-05`, `AC-08` | `SR-03`, `SR-06`, `AR-03`
* **Logika Server:** Validasi `$_GET['id']` dan kepemilikan `seller_id`. Tampilkan halaman konfirmasi ringkas dengan tombol **"Ya, Hapus"** (form `POST` membawa `csrf_token` + `id`) dan **"Batal"**. Saat dikonfirmasi `POST`, jalankan transaksi PDO (`beginTransaction()`, `DELETE`, catat `DELETE_PRODUCT` + `old_value` ke `activity_logs`, `commit()`, atau `rollBack()` jika gagal).

### 7.7 F-WEB-07 — Dashboard Rekapitulasi Otomatis, Pesanan COD & Log Aktivitas *(Fase 2)*

* **Traceability:** `R-07`, `R-08`, `R-10` (`WP 1.4.1`–`1.4.2`, `WP 2.1.1`–`2.2.1`) | `SR-04`, `SR-06`
* **`dashboard.php`:** Menampilkan 4 *Stat Cards* (Total Produk Aktif, Pesanan Hari Ini, Pesanan Menunggu, Total Omzet COD Hari Ini) dan tabel rekap porsi terjual per produk hari ini (`GROUP BY product_id`) dengan tombol muat ulang dinamis via `fetch("api/rekap_pesanan.php")` (dirender memakai `textContent`).
* **`pesanan.php`:** Menampilkan daftar pesanan masuk COD khusus `WHERE seller_id = :seller_id` dengan form `POST` (+ CSRF) untuk mengubah `status_pesanan` (`Menunggu` $\to$ `Diproses` $\to$ `Selesai`) dan mencatat `UPDATE_ORDER_STATUS` ke `activity_logs`.
* **`log_aktivitas.php`:** Menampilkan tabel *read-only* riwayat aktivitas akun penjual yang sedang login (`WHERE user_id = :user_id ORDER BY created_at DESC LIMIT 50`) sebagai bukti visual *Accountability*.

### 7.8 F-WEB-08 — Endpoint JSON API (`api/produk.php` & `api/rekap_pesanan.php`) *(Fase 2)*

* Header wajib: `Content-Type: application/json; charset=utf-8`.
* **`GET api/produk.php`:** Akses publik (*read-only*), mendukung filter query `?kategori=&lokasi_gedung=&status=&seller_id=`, hanya mengekspos kolom publik produk & nama organisasi penjual (tidak pernah mengekspos `password_hash` atau data privat akun).
* **`GET api/rekap_pesanan.php`:** Wajib sesi `penjual` aktif (jika tidak, kembalikan `HTTP 401` JSON `{"status":"error","message":"Autentikasi diperlukan."}`), mengembalikan ringkasan agregasi khusus `$_SESSION['user_id']`.

## 8. Rancangan Basis Data Relasional (`danushub_db` — 5 Tabel)

### 8.1 Tabel `users` (Diperluas untuk Lockout Keamanan)

| Kolom | Tipe Data | Constraint | Keterangan |
| ------------------------- | ----------------------------- | ------------------------------- | ----------------------------------------------------- |
| `id` | `INT UNSIGNED` | `PRIMARY KEY, AUTO_INCREMENT` | ID unik pengguna |
| `nama_lengkap` | `VARCHAR(100)` | `NOT NULL` | Nama lengkap pengguna |
| `nama_organisasi` | `VARCHAR(100)` | `NULL` | Nama ORMAWA/UKM (wajib untuk `penjual`) |
| `email` | `VARCHAR(100)` | `NOT NULL, UNIQUE` | Identitas login unik |
| `password_hash` | `VARCHAR(255)` | `NOT NULL` | *Salted hash* via `password_hash()` (`DD-01`) |
| `no_wa` | `VARCHAR(20)` | `NOT NULL` | Nomor WhatsApp koordinasi COD (`DD-02`) |
| `role` | `ENUM('penjual','pembeli')` | `NOT NULL, DEFAULT 'pembeli'` | Pemisahan hak akses RBAC (`R-01`) |
| `failed_login_attempts` | `TINYINT UNSIGNED` | `NOT NULL, DEFAULT 0` | Penghitung gagal login beruntun (`SR-02`) |
| `locked_until` | `DATETIME` | `NULL` | Batas waktu penguncian sementara 15 menit (`SR-02`) |
| `created_at` | `TIMESTAMP` | `DEFAULT CURRENT_TIMESTAMP` | Waktu pendaftaran akun |

### 8.2 Tabel `products`

| Kolom                   | Tipe Data                                                   | Constraint                                                | Keterangan                               |
| ----------------------- | ----------------------------------------------------------- | --------------------------------------------------------- | ---------------------------------------- |
| `id`                  | `INT UNSIGNED`                                            | `PRIMARY KEY, AUTO_INCREMENT`                           | ID unik produk                           |
| `seller_id`           | `INT UNSIGNED`                                            | `NOT NULL, FK -> users(id)`                             | Pemilik produk (*ownership* `AR-03`) |
| `nama_produk`         | `VARCHAR(120)`                                            | `NOT NULL`                                              | Nama produk Danus                        |
| `kategori`            | `ENUM('Makanan Berat','Camilan','Minuman','Merchandise')` | `NOT NULL`                                              | Kategori produk                          |
| `harga`               | `INT UNSIGNED`                                            | `NOT NULL`                                              | Harga satuan dalam Rupiah ($> 0$)      |
| `lokasi_gedung`       | `VARCHAR(80)`                                             | `NOT NULL`                                              | Lokasi gedung kampus                     |
| `foto_path`           | `VARCHAR(255)`                                            | `NOT NULL`                                              | Path relatif di `uploads/products/`    |
| `status_ketersediaan` | `ENUM('Ready','PO')`                                      | `NOT NULL, DEFAULT 'Ready'`                             | Status ketersediaan (`R-02`)           |
| `deskripsi`           | `TEXT`                                                    | `NULL`                                                  | Keterangan tambahan produk               |
| `created_at`          | `TIMESTAMP`                                               | `DEFAULT CURRENT_TIMESTAMP`                             | Waktu penambahan                         |
| `updated_at`          | `TIMESTAMP`                                               | `DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Waktu perubahan terakhir                 |

### 8.3 Tabel `orders` & `order_items`

* **`orders`:** `id` (PK), `kode_pesanan` (VARCHAR 30 UNIQUE), `buyer_id` (FK $\to$ `users.id`), `seller_id` (FK $\to$ `users.id`), `total_harga` (INT UNSIGNED), `metode_bayar` (ENUM `'COD'`), `titik_cod` (VARCHAR 100), `status_pesanan` (ENUM `'Menunggu'`, `'Diproses'`, `'Selesai'`), `created_at` (TIMESTAMP).
* **`order_items`:** `id` (PK), `order_id` (FK $\to$ `orders.id` `ON DELETE CASCADE`), `product_id` (FK $\to$ `products.id`), `qty` (INT UNSIGNED), `harga_satuan` (INT UNSIGNED), `subtotal` (INT UNSIGNED).

### 8.4 Tabel `activity_logs` *(Baru — Mendukung Accountability `SR-06`)*

| Kolom             | Tipe Data                    | Constraint                                   | Keterangan                                                                                                                                  |
| ----------------- | ---------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`            | `BIGINT UNSIGNED`          | `PRIMARY KEY, AUTO_INCREMENT`              | ID unik catatan audit                                                                                                                       |
| `user_id`       | `INT UNSIGNED`             | `NULL, FK -> users(id) ON DELETE SET NULL` | ID pelaku (`NULL` jika email tak terdaftar saat `LOGIN_FAILED`)                                                                         |
| `user_role`     | `VARCHAR(20)`              | `NOT NULL`                                 | Peran saat kejadian (`penjual`, `pembeli`, `guest`)                                                                                   |
| `action_type`   | `VARCHAR(50)`              | `NOT NULL`                                 | `LOGIN_SUCCESS`, `LOGIN_FAILED`, `ACCESS_DENIED`, `CREATE_PRODUCT`, `UPDATE_PRODUCT`, `DELETE_PRODUCT`, `UPDATE_ORDER_STATUS` |
| `target_table`  | `VARCHAR(50)`              | `NULL`                                     | Nama tabel terdampak (`users`, `products`, `orders`)                                                                                  |
| `target_id`     | `INT UNSIGNED`             | `NULL`                                     | ID baris data terdampak                                                                                                                     |
| `old_value`     | `TEXT`                     | `NULL`                                     | Ringkasan JSON nilai sebelum perubahan (tidak pernah memuat password)                                                                       |
| `new_value`     | `TEXT`                     | `NULL`                                     | Ringkasan JSON nilai sesudah perubahan (tidak pernah memuat password)                                                                       |
| `result_status` | `ENUM('ALLOWED','DENIED')` | `NOT NULL`                                 | Hasil keputusan kontrol akses                                                                                                               |
| `created_at`    | `TIMESTAMP`                | `DEFAULT CURRENT_TIMESTAMP`                | Waktu kejadian tercatat                                                                                                                     |

## 9. Arsitektur Direktori Proyek

```
danushub-web/
├── config/
│   └── database.php          # Koneksi PDO ($pdo) ke danushub_db, tanpa output HTML
├── includes/
│   ├── auth_guard.php        # Proteksi session, idle timeout 30 menit, role === 'penjual', & CSRF helper
│   ├── audit_logger.php      # Helper fungsi catatLogAktivitas($pdo, ...) untuk tabel activity_logs
│   ├── header.php            # Template semantik <header> + <aside> navigasi
│   └── footer.php            # Template semantik <footer>
├── assets/
│   ├── css/
│   │   └── style.css         # Stylesheet eksternal (Box Model, Flexbox, Grid, Badge, Non-wrap Action)
│   └── js/
│       ├── validasi.js       # Client-side validation (Constraint Validation API + cek panjang sandi >= 8)
│       └── dashboard.js      # Fetch API untuk pembaruan rekap otomatis menggunakan textContent
├── uploads/
│   └── products/             # Penyimpanan fisik foto produk (maks. 2 MB; .htaccess blokir eksekusi PHP)
├── api/
│   ├── produk.php            # Endpoint GET JSON publik daftar produk E-Katalog
│   └── rekap_pesanan.php     # Endpoint GET JSON terproteksi rekapitulasi pesanan harian
├── database.sql              # Skema DDL 5 tabel + data awal (seed) untuk pengujian
├── index.php                 # Pengarah awal ke dashboard.php atau login.php
├── register.php              # F-WEB-01: Registrasi akun penjual
├── login.php                 # F-WEB-02: Login penjual + lockout 5x gagal
├── logout.php                # F-WEB-02: Hancurkan sesi & redirect ke login.php
├── dashboard.php             # F-WEB-07: Stat Cards & Rekap Otomatis
├── katalog.php               # F-WEB-03: Daftar E-Katalog + Filter + Empty State
├── tambah_produk.php         # F-WEB-04: Tambah produk baru + upload foto
├── edit_produk.php           # F-WEB-05: Edit produk & status Ready/PO (ownership check)
├── hapus_produk.php          # F-WEB-06: Konfirmasi & hapus produk (transaksi PDO)
├── pesanan.php               # F-WEB-07: Daftar pesanan masuk COD & ubah status
└── log_aktivitas.php         # F-WEB-07: Riwayat audit aktivitas akun (read-only)


```

## 10. Rencana Pengujian Terpadu (Acceptance Testing P12 + Security Testing P10)

Matriks pengujian ini menyatukan **Acceptance Criteria MPPL (`AC-01`–`AC-08`)** dan **Security Testing Keamanan Informasi (`SR-01`–`SR-08`)** dengan cakupan skenario **Positive, Negative, dan Boundary** menggunakan akun uji fiktif (`uji_penjual1`, `uji_penjual2`, `uji_pembeli1`):

| ID TC | Ref. AC / SR | Tipe Uji | Precondition & Skenario Uji | Expected Result (Dapat Diamati) | Bukti Uji |
| --------------- | ------------------------------------------ | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **TC-01** | `AC-01`, `AC-08`, `SR-07` | *Positive* | Registrasi akun `uji_penjual1` dengan sandi 8+ karakter (`Danus#2026`), lalu periksa tabel `users` di phpMyAdmin. | Registrasi sukses; baris tersimpan dengan `role = 'penjual'`; kolom `password_hash` berisi string hash (bukan `Danus#2026`). | Tangkapan layar UI & baris tabel `users` (disamarkan) |
| **TC-02** | `SR-02` | *Boundary* | Registrasi dengan kata sandi $7$ karakter (di bawah batas $8$) lalu coba $8$ karakter. | Input $7$ karakter ditolak dengan pesan validasi; input $8$ karakter diterima. | Tangkapan layar pesan validasi |
| **TC-03** | `AC-02`, `SR-01` | *Negative* | (a) Buka `katalog.php` tanpa login; (b) Login memakai `uji_pembeli1`; (c) Login dengan sandi salah. | (a) Dialihkan ke `login.php`; (b) Ditolak dengan pesan peran tidak berwenang & tercatat `ACCESS_DENIED`; (c) Muncul pesan generik (*"Email atau kata sandi tidak valid"*), tercatat `LOGIN_FAILED` tanpa kata sandi. | Tangkapan layar penolakan & baris `activity_logs` |
| **TC-04** | `SR-02` | *Boundary* | Pada `uji_penjual1`, masukkan sandi salah $5$ kali berturut-turut, lalu pada percobaan ke-$6$ masukkan sandi yang **benar**. | Percobaan ke-$5$ memicu penguncian 15 menit; percobaan ke-$6$ tetap ditolak dengan pesan akun dikunci sementara meski sandi benar. | Tangkapan layar pesan kunci & kolom `locked_until` |
| **TC-05** | `AC-02`, `SR-02` | *Negative / Boundary* | Login `uji_penjual1`, biarkan sesi melewati batas *idle* ($> 30$ menit) atau klik Logout lalu tekan *Back* dan akses `katalog.php`. | Sesi berakhir; halaman terproteksi tidak dapat dibuka dan langsung dialihkan ke `login.php`. | Tangkapan layar redirect |
| **TC-06** | `AC-06` | *Positive* | Login sebagai `uji_penjual2` (belum memiliki produk), lalu buka `katalog.php`. | Tampil kartu *empty state* sesuai redaksi disepakati beserta tombol pintasan **"Tambah Produk Pertama"**. | Tangkapan layar *empty state* |
| **TC-07** | `AC-03`, `AC-08`, `SR-05`, `SR-06` | *Positive* | Login `uji_penjual1`, tambah 1 produk baru lengkap 6 atribut + foto JPG $\le 2\text{ MB}$. | Produk tampil di `katalog.php`, file tersimpan di `uploads/products/`, baris ada di tabel `products`, dan `CREATE_PRODUCT` tercatat di `activity_logs`. | Tangkapan layar katalog, tabel `products`, & `activity_logs` |
| **TC-08** | `AC-04`, `AC-05`, `AC-08`, `SR-06` | *Positive* | Ubah harga & status produk `uji_penjual1` (`Ready` $\to$ `PO`), lalu uji Hapus (klik Batal lalu Ya, Hapus). | Perubahan tampil & tercatat (`old_value`/`new_value`) di `activity_logs`; setelah Ya, Hapus data hilang dari katalog & database serta tercatat `DELETE_PRODUCT`. | Tangkapan layar UI, DB, & `activity_logs` |
| **TC-09** | `SR-03`, `SR-04`, `AR-03` | *Negative* (IDOR) | Login sebagai `uji_penjual2`, akses langsung URL `edit_produk.php?id={id_milik_uji_penjual1}` atau `hapus_produk.php?id={id_milik_uji_penjual1}`. | Akses ditolak dengan pesan tidak berwenang; data produk `uji_penjual1` **tetap tidak berubah**; kejadian `ACCESS_DENIED` tercatat di `activity_logs`. | Tangkapan layar penolakan, bukti DB utuh, & log |
| **TC-10** | `SR-05` | *Negative / Boundary* | (a) Masukkan harga `0` atau `-5000`; (b) Unggah file `.docx`/`.php` atau gambar $3\text{ MB}$; (c) Masukkan `<script>alert('XSS')</script>` pada nama produk. | (a) Ditolak validasi server; (b) Ditolak pesan format/ukuran maks. $2\text{ MB}$ & layanan tetap jalan; (c) Tampil sebagai teks murni tanpa eksekusi JavaScript. | Tangkapan layar penolakan & tampilan teks aman |
| **TC-11** | `AC-07` | *Positive* | Periksa `login.php`, `dashboard.php`, dan `katalog.php` pada resolusi layar laptop $1366 \times 768\text{ px}$. | Navigasi, *Stat Cards*, tabel produk, dan tombol aksi **Edit / Hapus** sejajar horizontal tanpa terpotong atau *wrapping*. | Tangkapan layar DevTools $1366 \times 768$ |
| **TC-12** | `R-07`, `R-10`, `SR-06` | *Positive / Negative* | Isi data pesanan COD *dummy* untuk `uji_penjual1`, buka `dashboard.php`, panggil `api/rekap_pesanan.php` (dengan & tanpa sesi), dan cek `log_aktivitas.php`. | Stat cards & rekap per produk akurat; API mengembalikan `200 OK` JSON saat login dan `401` saat tanpa login; `log_aktivitas.php` tampil *read-only* tanpa kata sandi. | Tangkapan layar dashboard, Network DevTools, & log |

## 11. Roadmap Eksekusi & Pembagian Kerja Tim

| Tahap | Estimasi | Fokus Pekerjaan & Deliverables Teknis | PIC Utama & Pendamping |
| ----------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **1** | Hari 1 | Inisialisasi repositori Git (`main`, `dev`, *feature branches*), bangun `database.sql` (**5 tabel** termasuk `activity_logs` + data *seed* akun uji), impor ke phpMyAdmin, buat `config/database.php` & `includes/audit_logger.php`. | **Rifki** & **Hazel** |
| **2** | Hari 1–2 | Bangun `includes/header.php`, `footer.php`, dan `assets/css/style.css` (CSS Grid *dashboard*, Flexbox autentikasi, tombol aksi sejajar anti-*wrapping* `AC-07`). | **Tatag** |
| **3** | Hari 2–3 | Implementasi `register.php` (sandi $\ge 8$ karakter, `password_hash()`), `login.php` (pesan generik, *lockout* 5x gagal / 15 menit), `logout.php`, `includes/auth_guard.php` (*idle timeout* 30 menit + CSRF), dan `assets/js/validasi.js`. | **Hazel** & **Tatag** |
| **4** | Hari 3–4 | Implementasi CRUD E-Katalog aman: `katalog.php` (+ *empty state* `AC-06`), `tambah_produk.php` (+ validasi upload $\le 2\text{ MB}$), `edit_produk.php` (+ *ownership check* & log nilai lama/baru), `hapus_produk.php` (+ transaksi PDO). | **Tatag** & **Hazel** |
| **5** | Hari 5–7 | Implementasi Fase 2: `api/produk.php`, `api/rekap_pesanan.php`, `pesanan.php`, `dashboard.php` + `assets/js/dashboard.js` (`fetch()`), serta `log_aktivitas.php` (*read-only*). | **Rifki**, **Tatag**, & **Hazel** |
| **6** | Hari 8 | Eksekusi pengujian aktual `TC-01` s.d. `TC-12` (mengganti bukti `SIMULASI` LK 12.5 MPPL menjadi bukti aktual sekaligus melengkapi *Security Testing Report* P10 Keamanan Informasi). | **Dea** & **Afdila** |

### Aturan Pengendalian Versi & Perubahan (MPPL P12 + Keamanan Informasi)

1. **Workflow Git:** Setiap fitur dikerjakan di *branch* terpisah (`feature/db-audit`, `feature/ui-layout`, `feature/auth-hardening`, `feature/crud-katalog`, `feature/rekap-api`), dilakukan *code review* keamanan (cek PDO, `htmlspecialchars`, `seller_id`, CSRF), lalu di-*merge* ke `dev` sebelum `main`.
2. **Keamanan Repositori:** Dilarang melakukan *commit* kredensial produksi atau berkas `.env` ke GitHub; gunakan `.gitignore` untuk melindungi berkas konfigurasi sensitif dan foto unggahan uji.
3. **Pengendalian Ruang Lingkup:** Perubahan di luar PRD v2.0 wajib melalui persetujuan Project Manager & Project Owner sebelum dikodekan.
