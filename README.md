# UPNVJT SIGAP — Aplikasi Desktop Admin (Flutter)

UPNVJT Sigap dibuat untuk membantu pengelolaan layanan bantuan antar mahasiswa di Universitas Pembangunan Nasional "Veteran" Jawa Timur. Merupakan pengembangan dari layanan UPNVJT Sigap yang sebelumnya masih dilakukan melalui chat. Dengan ini, proses pengelolaan data dan pesanan dibuat lebih terstruktur sehingga admin dapat mengelola pengguna, kategori layanan, pesanan, transaksi, dan data lainnya menjadi satu. 

## Fitur yang tersedia

- **Login Admin:** Untuk masuk ke halaman utama aplikasi (panel desktop dibatasi untuk role Admin). Kata sandi bisa dilihat dan disembunyikan melalui ikon mata.
- **Registrasi Pelanggan:** Untuk membuat akun baru.
- **Dashboard:** Untuk melihat ringkasan data pengguna, pesanan, kategori layanan, dan transaksi.
- **Master Kategori Layanan:** Untuk menambah, mengubah, menghapus, dan melihat kategori layanan.
- **Master Pengguna:** Untuk mengelola data pelanggan dan kru. Akun Kru hanya dapat didaftarkan oleh Admin lewat Master Pengguna (jadwal KRS wajib diisi).
- **Master Pesanan:** Untuk melihat dan mengelola pesanan yang masuk.
- **Negoisasi Harga:** Untuk pesanan dengan layanan khusus yang menggunakan harga negoisasi.
- **Laporan Transaksi:** Untuk melihat data transaksi dan komisi.
- **Profil Admin:** Untuk mengubahh data profil dan kata sandi.
- **Logout:** Untuk keluar dari akun dan kembali ke halaman login.

## Teknologi yang digunakan

- Flutter
- Dart
- MySQL sebagai rancangan database/PDM

## Cara Menjalankan Aplikasi

Pastikan Flutter SDK sudah terpasang dan `flutter doctor` tidak menunjukkan masalah untuk Windows desktop.

1. Ekstrak ZIP.
2. Buka CMD/Terminal, masuk ke folder `sigap`.
3. Jalankan `flutter create --platforms=windows .` untuk membuat berkas platform desktop yang belum disertakan dalam ZIP.
4. Jalankan `flutter pub get`.
5. Jalankan `flutter run -d windows`.

## Akun Demo

Untuk mencoba Aplikasi sebagai Admin, gunakan akun berikut:
**Email:** `sultan@email.com`
**Password:** `admin123`

Akun demo digunakan untuk mencoba alur aplikasi tanpa perlu membuat akun admin terlebih dahulu. Form login diisi dengan akun demo tersebut saat pertama kali dibuka. 

## Ekspor CSV

Tombol Ekspor (Master Kategori) dan Ekspor CSV (Laporan Keuangan) menampilkan data dalam bentuk teks CSV
di dialog. Klik **Salin CSV**, lalu tempel ke Excel atau simpan sebagai berkas `.csv`.

## Fitur Negosiasi Harga

Beberapa layanan pada UPNVJT Sigap menggunakan sistem harga negoisasi. Admin dapat mencatat proses tawar-menawar harga melalui menu negoisasi pesanan. Berlaku untuk kategori bertipe harga **Negosiasi** (Pindahan Kos, Jasa Khusus, Lainnya).

**Alur:**
1. Buka Master Pesanan, klik ikon **Negosiasi** (gelembung chat) pada pesanan.
2. Pelanggan atau kru mengajukan harga tawar (dicatat admin pada form).
3. Pihak lawan **Terima & sepakati**, **Tolak**, atau **Tawar ulang** (tawar ulang otomatis menolak tawaran yang masih menunggu).
4. Tawaran yang diterima menjadi harga final pesanan (`estimasi_biaya`). Bila tawaran diterima berasal dari kru, kru tersebut otomatis memegang pesanan (status Diambil).

Kolom Estimasi di Master Pesanan menampilkan status negosiasi (disepakati / menunggu / belum ada), dan ada pengingat jumlah tawaran yang menunggu keputusan.

## Kategori "Lainnya (Request)"

Menyediakan kategori **Lainnya (Request)** untuk permintaan layanan yang belum tersedia pada daftar kategori. Pada form pesanan, kolom detail berubah menjadi **Layanan yang diminta pelanggan** dan wajib diisi. 

Pada kategori ini, pelanggan dapat memberikan detail layanan yang ingin diminta. Karena jenis layanan dan harganya berbeda-beda, kategori ini menggunakan sistem harga negoisasi.

## Pemetaan Database

| Model aplikasi | Tabel PDM | Keterangan |
|---|---|---|
| `UserModel` | `users` | data akun dan role |
| `KategoriLayanan` | `kategori_layanan` | nama kategori dan tarif dasar per km |
| `Pesanan` | `pesanan` | pelanggan, kru, kategori, lokasi, waktu, biaya, status |
| `Negosiasi` | `negosiasi` | tawaran harga, pengirim, status tawaran |
| `TransaksiKeuangan` | `transaksi_keuangan` | total bayar, komisi admin, pendapatan kru |

## Struktur Project

```text
lib/
  main.dart
  core/theme.dart
  models/models.dart
  data/app_store.dart
  widgets/common.dart
  pages/auth_pages.dart
  pages/home_shell.dart
  pages/dashboard_page.dart
  pages/kategori_page.dart
  pages/pengguna_page.dart
  pages/pesanan_page.dart
  pages/laporan_page.dart
  pages/profil_page.dart
```

## Dokumentasi PDM

Pemetaan antara fitur aplikasi dan tabel dapat dilihat pada file: `PDM_MAPPING.md`

## Catatan 

 Untuk versi project saat ini, data aplikasi masih menggunakan penyimpanan sementara melalui `AppStore` sehingga perubahan data hanya digunakan untuk kebutuhan demonstrasi aplikasi.

 Struktur model dan nama tabel tetap disesuaikan dengan PDM yang telah dibuat. Integrasi langsung dengan database MySQL dapat dikembangkan lebih lanjut menggunakan repository ayau API.

## Tim Pengembang

Project UPNVJT Sigap dikembangkan sebagai project kelompok untuk mata kuliah Pemrograman Desktop

| Nama | NPM | Peran |
|---|---|---|
| Meutia Zaini Siregar | 25082010199 | Captain |
| Zaskia Syakira Nazahrani | 25082010206 | Hustler |
| Aprilia Tri Jayanti A. | 25082010221 | Hipster |
| Anggie Ayu Ramadhani | 25082010225 | Hacker |