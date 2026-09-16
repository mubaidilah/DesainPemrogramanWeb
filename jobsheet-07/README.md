# Jobsheet 7 — PHP Dasar & Form Handling (SIMPUS-Mini)

Lanjutan dari jobsheet-06. Seluruh halaman kini berupa file `.php` yang diproses
di server: navbar/footer dipakai ulang lewat `include`, form Tambah benar-benar
mengirim data ke `proses_tambah.php`, data disimpan sementara di `$_SESSION`,
dan `list.php` merender tabel langsung dari server.

## Menjalankan

Dari dalam folder `jobsheet-07/`:

```
php -S localhost:8000
```

Buka http://localhost:8000/index.php

Path CSS/JS/menu dihitung otomatis lewat variabel `$base` di
`includes/header.php`, jadi proyek ini juga tetap benar diakses lewat Laragon
meskipun bersarang di dalam beberapa folder
(mis. http://dp2026.test/kode-praktikum/jobsheet-07/).

## Struktur

```
jobsheet-07/
├── index.php
├── includes/
│   ├── header.php          # BARU — <head> + navbar + $base + session_start()
│   └── footer.php          # BARU — </main> + footer + <script>
├── assets/
│   ├── css/style.css       # ditambah gaya .flash
│   └── js/app.js           # tidak berubah dari jobsheet-06
├── buku/
│   ├── list.php            # render dari $_SESSION['buku']
│   ├── tambah.php          # form method="post" action="proses_tambah.php"
│   └── proses_tambah.php   # BARU — validasi server + simpan ke $_SESSION
├── anggota/
│   ├── list.php
│   ├── tambah.php
│   └── proses_tambah.php   # BARU
└── docs/wireframe.md       # identik dengan jobsheet-06
```

## Uji cepat

1. Tambah Buku dengan data valid → diarahkan ke `list.php` + flash hijau.
2. Refresh `list.php` → flash hilang, data tetap ada (bukti `unset()`).
3. Submit form kosong → flash merah di `tambah.php`, tidak ada data tersimpan.
4. Matikan JavaScript di browser, submit form kosong lagi → validasi server
   tetap bekerja.
5. Tutup browser sepenuhnya, buka lagi → data hilang (sifat sementara
   `$_SESSION`).

Catatan: data `$_SESSION` bersifat sementara. Penyimpanan permanen dengan
database PostgreSQL dimulai di Jobsheet 8.
