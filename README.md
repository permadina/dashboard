# Dashboard Survei Kesehatan Masyarakat Indonesia (Versi HTML)

Dashboard interaktif berbasis satu file `index.html`, dengan fitur **tambah, edit, hapus, dan simpan data**. Angka dan grafik otomatis menyesuaikan data terbaru yang tersimpan.

> Data contoh bersifat **sintetis** (1.000 responden, 12 provinsi, survei 2022–2026). Bukan hasil survei nyata dan tidak mewakili populasi Indonesia.

---

## 1. Isi Paket

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi (tampilan, perhitungan, dan 1.000 data awal) |
| `README.md` | Panduan ini |

Tidak perlu instalasi apa pun. Cukup buka `index.html` di browser (Chrome, Edge, Firefox, Safari). Koneksi internet diperlukan karena grafik memuat Chart.js dari CDN.

---

## 2. Cara Upload ke Vercel

1. Buat sebuah folder, misalnya `dashboard-kesehatan`, lalu letakkan `index.html` di dalamnya.
2. Buka [vercel.com](https://vercel.com), masuk, lalu pilih **Add New → Project**.
3. Pilih salah satu cara:
   - **Drag & drop** folder ke Vercel, atau
   - **Vercel CLI**: jalankan `npm i -g vercel`, masuk ke folder, lalu ketik `vercel`.
4. Framework preset pilih **Other**. Kosongkan Build Command dan Output Directory.
5. Klik **Deploy**. Vercel akan memberi alamat seperti `https://nama-proyek.vercel.app`.

---

## 3. Tab Dashboard

### Filter
Di bagian atas terdapat tiga filter: **Provinsi**, **Tahun survei**, dan **Wilayah**. Pilihan filter berasal dari data yang tersimpan, jadi provinsi atau tahun baru akan muncul otomatis setelah disimpan.

### Kartu KPI (12 kartu)
Total responden, JKN, akses faskes mudah, air minum layak, sanitasi layak, berisiko gangguan mental, hipertensi, perokok, masalah gigi & mulut, persalinan di faskes, imunisasi dasar lengkap, dan stunting balita. Tulisan `n = ...` di bawah angka adalah jumlah penyebut yang dipakai.

### Grafik (11 grafik)
Tren tahunan, komposisi usia & jenis kelamin, akses & lingkungan, prevalensi penyakit, status gizi dewasa (IMT), kesehatan ibu-bayi-balita, status gizi balita, PHBS, status merokok per jenis kelamin, kesehatan mental-gigi-farmasi, dan disabilitas.

Catatan: grafik **tren tahunan** hanya mengikuti filter Provinsi dan Wilayah (filter Tahun tidak berlaku).

---

## 4. Tab Kelola Data

### Alur kerja (penting)

```
Tambah / Edit / Hapus  →  masuk DRAF  →  tekan [Simpan]  →  dashboard diperbarui
```

Semua perubahan **belum** memengaruhi dashboard sebelum tombol **💾 Simpan** (pojok kanan atas) ditekan. Selama ada perubahan yang belum disimpan, muncul penanda oranye **"● Ada perubahan belum disimpan"**.

### Menambah data
1. Klik **＋ Tambah Data**.
2. Isi form. Kolom bertanda `*` wajib diisi (ID, Nama, Usia, Provinsi, Tanggal Survei). ID terisi otomatis dan bisa diubah, tetapi tidak boleh sama dengan ID lain.
3. Klik **OK (masuk draf)**, lalu tekan **Simpan**.

### Mengedit data
1. Cari responden dengan kotak pencarian (ID, nama, atau provinsi).
2. Klik **Edit** pada baris tersebut, ubah isiannya, klik **OK**, lalu **Simpan**.

### Menghapus data
Klik **Hapus**, konfirmasi, lalu tekan **Simpan** agar penghapusan berlaku pada dashboard.

### Tombol lain

| Tombol | Fungsi |
|---|---|
| **Batalkan perubahan** | Membuang semua perubahan yang belum disimpan |
| **Impor CSV** | Menambah atau memperbarui data dari file CSV (lihat bagian 5) |
| **Unduh CSV** | Mengunduh seluruh data tersimpan sebagai cadangan |
| **Reset data awal** | Mengembalikan ke 1.000 data contoh (data Anda terhapus) |

---

## 5. Mengisi Form dengan Benar

### Aturan umum
- Kolom yang tidak relevan untuk responden diisi **"Tidak berlaku"** (misalnya status kehamilan untuk laki-laki).
- Kolom angka yang tidak diukur boleh dikosongkan.
- Kolom bertipe teks pilihan (Provinsi, Pekerjaan, Sumber air, dll.) dapat diketik bebas. Nilai yang sudah ada muncul sebagai saran, jadi **tulis persis sama** agar tidak terhitung sebagai kategori baru.

### Kolom yang dihitung otomatis (tidak perlu diisi)
Kelompok usia, tahun survei, akses faskes mudah, air minum layak, sanitasi layak, status mental, hipertensi, kategori literasi, ANC standar (K6), persalinan di faskes, IMT, kategori IMT, status stunting, dan status wasting.

### Kelompok sasaran per indikator

| Indikator | Penyebut |
|---|---|
| Gangguan mental, perokok, literasi | Usia ≥ 15 tahun |
| Hipertensi, diabetes, jantung, IMT | Usia ≥ 18 tahun |
| Gigi & mulut | Usia ≥ 3 tahun |
| CTPS | Usia ≥ 5 tahun |
| Aktivitas fisik, sayur-buah | Usia ≥ 10 tahun |
| ANC, persalinan, nifas | Ibu yang melahirkan ≤ 2 tahun terakhir |
| Imunisasi | Anak 12–59 bulan |
| ASI eksklusif | Anak 6–23 bulan |
| Posyandu, perkembangan, stunting, wasting | Balita 0–59 bulan |

### Ambang batas yang dipakai (sama dengan sheet Parameter Excel)
Akses mudah ≤ 30 menit · SRQ-20 ≥ 6 · hipertensi ≥ 140/90 mmHg · ANC ≥ 6 kali · literasi rendah < 50 dan baik ≥ 75 · IMT kurus < 18,5, normal ≤ 25, BB lebih ≤ 27, obesitas > 27 · Z-score pendek/kurus < −2 dan sangat pendek/sangat kurus < −3 · gizi lebih > +2 · Posyandu rutin ≥ 8 kali/tahun.

Untuk mengubah ambang, edit objek `P` di dalam `index.html` (sekitar baris `const P={Waktu:30,SRQ:6,...}`).

---

## 6. Impor CSV

1. Siapkan file CSV (pemisah koma atau titik koma) dengan baris pertama berisi nama kolom.
2. Kolom wajib: `ID_Responden` dan `Nama_Responden`. Nama kolom lain harus sama dengan nama kolom pada data awal.
3. Cara termudah: klik **Unduh CSV** dulu, lalu pakai file tersebut sebagai templat.
4. Tanggal ditulis `YYYY-MM-DD` (contoh `2026-03-15`).
5. ID yang sudah ada akan **diperbarui**, ID baru akan **ditambahkan**. Setelah impor, tekan **Simpan**.

---

## 7. Tempat Penyimpanan Data (Penting)

Data disimpan di **localStorage browser** perangkat yang dipakai, bukan di server.

- Data **hanya terlihat di browser dan perangkat yang sama**. Pengunjung lain, atau perangkat lain, melihat data awal dari file.
- Jika cache atau data situs browser dihapus, data kembali ke data awal.
- Mode incognito/privat tidak menyimpan data setelah jendela ditutup.
- **Lakukan Unduh CSV secara berkala** sebagai cadangan.

Agar data bisa dibagikan ke banyak pengguna, dibutuhkan database online (misalnya Supabase atau Vercel KV). Versi ini belum memilikinya.

### Memperbarui data awal untuk semua pengunjung
Data awal tertanam di `index.html` pada konstanta `DATA`. Untuk menggantinya secara permanen bagi semua orang, ganti isi `DATA` dengan data baru lalu deploy ulang ke Vercel.

---

## 8. Pemecahan Masalah

| Masalah | Penyebab / solusi |
|---|---|
| Grafik tidak muncul | Tidak ada internet atau CDN diblokir. Periksa koneksi lalu muat ulang. |
| Perubahan tidak tampil di dashboard | Tombol **Simpan** belum ditekan. |
| Data hilang setelah dibuka di perangkat lain | Normal: data tersimpan per browser. Pakai Unduh/Impor CSV untuk memindahkan. |
| "ID_Responden sudah dipakai" | Gunakan ID lain yang belum ada. |
| Persentase aneh pada filter sempit | Jumlah sasaran (`n`) terlalu kecil, misalnya hanya beberapa ibu bersalin atau balita. |
| Muncul peringatan saat menutup tab | Ada perubahan yang belum disimpan. |

---

## 9. Pemetaan dari Excel

| Excel | Versi HTML |
|---|---|
| Sheet `Dashboard` (KPI, grafik, filter) | Tab **Dashboard** |
| Sheet `Data_Survei` (kolom putih = input) | Tab **Kelola Data** (form) |
| Kolom abu-abu (rumus) | Dihitung otomatis oleh JavaScript |
| Sheet `Kalkulasi` (COUNTIFS) | Fungsi perhitungan indikator di dalam skrip |
| Sheet `Parameter` | Objek `P` di dalam skrip |
| Sheet `Kamus_Data` | Label dan pilihan pada form |
