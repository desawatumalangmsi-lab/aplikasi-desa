# Panduan: Aplikasi Desa dengan Data Bersama (GitHub Pages + Supabase, gratis)

File: `index.html` (aplikasi), `config.js` (isi kunci Supabase), `supabase.sql` (membuat tabel).

## A. Buat database Supabase (gratis)
1. Buka https://supabase.com, daftar, klik **New project**. Isi nama, kata sandi database (simpan), pilih region terdekat (mis. Singapore), plan **Free**.
2. Tunggu project siap. Buka **SQL Editor > New query**, tempel isi `supabase.sql`, klik **Run**. Harus muncul "Success".
3. Buka **Authentication > Sign In / Providers** dan pastikan **Email** aktif. Matikan **Allow new users to sign up** supaya orang asing tidak bisa daftar.
4. Buka **Authentication > Users > Add user > Create new user**. Isi email dan kata sandi, centang **Auto Confirm User**. Ulangi untuk setiap petugas desa.
5. Buka **Project Settings > API**. Salin **Project URL** dan **anon public key** (JANGAN pakai `service_role`).

## B. Isi config.js
Buka `config.js`, ganti `url` dan `key` dengan hasil langkah A5. Simpan.

## C. Pasang di GitHub Pages
1. github.com > **+ > New repository**, nama `aplikasi-desa`, **Public**.
2. **uploading an existing file**, seret `index.html`, `config.js`, `README.md`, **Commit changes**.
3. **Settings > Pages > Deploy from a branch > main / (root) > Save**.
4. Tunggu 1-3 menit. Buka `https://NAMA-AKUN.github.io/aplikasi-desa/`.
5. Masuk dengan email/kata sandi dari A4. Pojok kiri bawah menampilkan 🟢 **Data bersama aktif**.

## D. Uji data bersama
1. Buka link di dua perangkat/browser, login akun berbeda atau sama.
2. Di perangkat 1 tambah satu kegiatan. Dalam beberapa detik muncul di perangkat 2.
3. Di perangkat 2 catat satu pencairan, cek muncul di perangkat 1.

## Catatan penting
- **Batas gratis Supabase** (dicek per pertengahan 2026, cek ulang di supabase.com/pricing): database 500 MB, 5 GB egress, 2 project. **Project gratis otomatis dijeda jika 7 hari tidak aktif**. Data tidak hilang, cukup klik **Restore** di dashboard Supabase. Buka aplikasi minimal seminggu sekali agar tidak dijeda.
- `anon public key` memang boleh terlihat publik. Keamanan data dijaga oleh login dan aturan tabel (RLS), jadi **jangan pernah** menaruh `service_role` key di `config.js`.
- Sinkron per kelompok data (kegiatan, rincian, pencairan, dll.). Jika dua orang menyimpan kelompok yang sama dalam hitungan detik, yang terakhir menang. Bagi tugas per tab.
- Semua petugas yang punya akun bisa membaca dan mengubah semua data. Tidak ada pembatasan per peran.
- Tetap lakukan **Ekspor Cadangan Data** rutin (tab Kontrol Bulanan).
- Jika pojok kiri bawah tertulis 🔴, cek koneksi dan login ulang. Jika ⚪ Mode lokal, `config.js` belum terisi benar.
