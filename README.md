# 🔐 LockerVault — Sistem Manajemen Loker Karyawan

> Aplikasi manajemen loker karyawan berbasis web yang berjalan sepenuhnya di sisi klien — tanpa backend, tanpa database, tanpa instalasi.

---

## 📋 Daftar Isi

- [Tentang Aplikasi](#tentang-aplikasi)
- [Fitur Utama](#fitur-utama)
- [Struktur Data](#struktur-data)
- [Cara Penggunaan](#cara-penggunaan)
- [Manajemen Data (Export & Import JSON)](#manajemen-data-export--import-json)
- [Alur Kerja yang Disarankan](#alur-kerja-yang-disarankan)
- [Tampilan & UI](#tampilan--ui)
- [Teknologi yang Digunakan](#teknologi-yang-digunakan)
- [Catatan Teknis](#catatan-teknis)

---

## Tentang Aplikasi

**LockerVault** adalah sistem manajemen loker karyawan berbasis HTML tunggal yang dirancang untuk kebutuhan administrasi loker di lingkungan perkantoran atau perusahaan. Seluruh logika aplikasi berjalan di browser (client-side) menggunakan JavaScript murni — tidak memerlukan server, hosting, atau koneksi internet setelah file dibuka.

Aplikasi ini cocok digunakan oleh:
- Admin HR / General Affairs untuk mengelola loker karyawan
- Tim fasilitas/umum yang mengelola aset fisik kantor
- Instansi atau perusahaan yang membutuhkan pencatatan loker sederhana namun terstruktur

---

## Fitur Utama

### 📊 Dashboard Summary
Menampilkan ringkasan data secara real-time di bagian atas halaman:
- **Total Loker** — jumlah keseluruhan loker yang terdaftar
- **Total Terisi** — jumlah loker yang sedang digunakan
- **Total Kosong** — jumlah loker yang tersedia

### ✏️ CRUD Lengkap
Operasi data penuh melalui antarmuka modal yang bersih:
- **Create** — tambah data loker baru dengan form lengkap
- **Read** — tampilan tabel terurut dengan semua informasi loker
- **Update** — edit data loker yang sudah ada, timestamp diperbarui otomatis
- **Delete** — hapus data dengan konfirmasi dialog agar terhindar dari kesalahan

### 🔍 Filter & Pencarian
- **Search** berdasarkan nama karyawan (real-time)
- **Filter Gender** — Laki-laki / Perempuan / Semua
- **Filter Status** — Terisi / Kosong / Semua
- **Filter Departemen** — dropdown dinamis berdasarkan data yang ada
- **Sort kolom** — klik header kolom mana saja untuk mengurutkan naik/turun

### 🕐 Tracking Waktu Otomatis
Setiap data loker memiliki pencatatan waktu otomatis:
- **Dibuat** — dicatat saat pertama kali data ditambahkan
- **Diperbarui** — diperbarui otomatis setiap kali data diedit

Ditampilkan di kolom **Tanggal** dengan format `dd-mm-yyyy hh:mm:ss`:
- 🟢 **Chip Hijau** — data belum pernah diedit (menampilkan waktu pembuatan)
- 🟡 **Chip Kuning `Update`** — data pernah diubah (menampilkan waktu terakhir diperbarui)

### 💾 Export & Import JSON
- **Export** — unduh seluruh data sebagai file `loker-data.json` kapan saja
- **Import** — muat data dari file `.json` yang sudah ada, dengan validasi struktur otomatis

### 🔔 Notifikasi Toast
Setiap aksi CRUD menampilkan notifikasi singkat di pojok kanan bawah layar:
- 🟢 Hijau — tambah / update berhasil
- 🔴 Merah — hapus berhasil / error
- 🟡 Kuning — peringatan (misal: export saat data kosong)

---

## Struktur Data

Setiap loker disimpan sebagai objek JavaScript dengan struktur berikut:

```json
{
  "id": "1748392012345",
  "lockerNumber": "L-001",
  "keySerial": "K-1001",
  "gender": "L",
  "status": "TERISI",
  "employeeName": "Ahmad Arif",
  "position": "Staff IT",
  "department": "Information Technology",
  "note": "Catatan tambahan jika ada",
  "createdAt": "2026-02-18T07:30:00.000Z",
  "updatedAt": "2026-02-18T07:30:00.000Z"
}
```

| Field | Tipe | Keterangan |
|---|---|---|
| `id` | String | ID unik, dibuat otomatis dari timestamp |
| `lockerNumber` | String | Nomor loker (contoh: L-001, P-002) |
| `keySerial` | String | Nomor seri kunci loker |
| `gender` | String | `"L"` untuk Laki-laki, `"P"` untuk Perempuan |
| `status` | String | `"TERISI"` atau `"KOSONG"` |
| `employeeName` | String | Nama lengkap karyawan pemegang loker |
| `position` | String | Jabatan karyawan |
| `department` | String | Nama departemen/divisi |
| `note` | String | Catatan tambahan (opsional) |
| `createdAt` | ISO 8601 | Waktu pembuatan data, diisi otomatis |
| `updatedAt` | ISO 8601 | Waktu terakhir diperbarui, diisi otomatis |

---

## Cara Penggunaan

### Membuka Aplikasi
Cukup buka file `index.html` langsung di browser (Chrome, Firefox, Edge, Safari). Tidak perlu server lokal atau koneksi internet.

```
Klik dua kali → index.html
```

### Menambah Data Loker Baru
1. Klik tombol **`+ Tambah Loker`** di pojok kanan atas
2. Isi form yang muncul:
   - **No. Loker** *(wajib)* — contoh: `L-001`
   - **Serial Kunci** *(wajib)* — contoh: `K-1234`
   - **Gender** *(wajib)* — pilih Laki-laki atau Perempuan
   - **Status** *(wajib)* — TERISI atau KOSONG
   - **Nama Karyawan** — isi jika status TERISI
   - **Jabatan** & **Departemen** — informasi karyawan
   - **Catatan** — keterangan tambahan (opsional)
3. Klik **`Simpan`**
4. Data otomatis tersimpan ke LocalStorage dan tabel diperbarui

### Mengedit Data Loker
1. Klik ikon ✏️ (pensil) pada baris loker yang ingin diubah
2. Ubah data yang diperlukan di form modal
3. Di bagian atas modal akan tampil info: tanggal dibuat, terakhir diperbarui, dan ID loker
4. Klik **`Update`** untuk menyimpan perubahan
5. Kolom Tanggal di tabel akan berubah menjadi chip kuning **`Update`**

### Menghapus Data Loker
1. Klik ikon 🗑️ (tempat sampah) pada baris loker yang ingin dihapus
2. Dialog konfirmasi akan muncul
3. Klik **`Ya, Hapus`** untuk mengonfirmasi penghapusan

### Mencari & Memfilter Data
- Ketik nama karyawan di kolom **pencarian** untuk filter real-time
- Klik pill **Laki-laki / Perempuan** untuk filter berdasarkan gender
- Klik pill **Terisi / Kosong** untuk filter berdasarkan status
- Pilih departemen dari dropdown untuk filter berdasarkan divisi
- Klik header kolom tabel untuk mengurutkan data (klik lagi untuk membalik urutan)

---

## Manajemen Data (Export & Import JSON)

Karena aplikasi berjalan sepenuhnya di browser tanpa backend, data dikelola melalui dua mekanisme:

### LocalStorage (Penyimpanan Otomatis)
Data tersimpan otomatis di LocalStorage browser setiap kali ada perubahan. Data akan tetap ada selama:
- Browser tidak di-*clear* data / cache
- Tidak membuka file di browser yang berbeda

> ⚠️ **Penting:** LocalStorage bersifat per-browser dan per-perangkat. Jika membuka `index.html` di browser atau komputer lain, data tidak akan otomatis terbawa.

### Export JSON
Digunakan untuk membuat backup data atau memindahkan data ke perangkat lain:

1. Klik tombol **`Export JSON`** di header aplikasi
2. Browser akan mengunduh file **`loker-data.json`**
3. Simpan file ini di folder yang sama dengan `index.html` agar mudah ditemukan

> 💡 Disarankan untuk melakukan export secara berkala sebagai backup.

### Import JSON
Digunakan untuk memuat data dari file backup:

1. Klik tombol **`Import JSON`** di header aplikasi
2. Pilih file **`loker-data.json`** yang sebelumnya sudah di-export
3. Aplikasi akan memvalidasi struktur file secara otomatis
4. Jika valid, data langsung dimuat dan tersimpan ke LocalStorage
5. Semua data lama akan digantikan dengan data dari file JSON

> ⚠️ Import akan **menggantikan** seluruh data yang ada. Pastikan sudah backup terlebih dahulu sebelum import.

---

## Alur Kerja yang Disarankan

```
Hari Pertama
     │
     ▼
Buka index.html → Tambah data loker satu per satu
     │
     ▼
Selesai input → Klik Export JSON → Simpan loker-data.json
     │
     ▼
Simpan loker-data.json di folder yang sama dengan index.html


Hari Berikutnya
     │
     ▼
Buka index.html → Data sudah ada (dari LocalStorage)
     │
     ├── Jika data masih ada → Langsung gunakan
     │
     └── Jika data hilang (browser baru/clear cache)
              │
              ▼
         Import JSON → Pilih loker-data.json → Data kembali


Setiap Ada Perubahan
     │
     ▼
Lakukan CRUD → Klik Export JSON → Timpa loker-data.json lama
```

---

## Tampilan & UI

### Tema & Desain
- Tema **dark mode** modern dengan palet warna gelap
- Font display **Syne** untuk judul dan elemen UI
- Font body **DM Sans** untuk teks konten
- Animasi transisi halus pada baris tabel dan modal

### Kode Warna Status
| Warna | Makna |
|---|---|
| 🟢 Hijau | Loker **TERISI** / Data baru dibuat |
| 🔴 Merah | Loker **KOSONG** |
| 🟡 Kuning | Data pernah **diperbarui** / Aksen utama UI |
| 🔵 Biru | Karyawan **Laki-laki** |
| 🩷 Pink | Karyawan **Perempuan** |

### Indikator Baris Tabel
Setiap baris tabel memiliki garis warna di sisi kiri:
- **Garis hijau** — loker berstatus TERISI
- **Garis merah** — loker berstatus KOSONG

### Responsif
Tampilan tabel mendukung horizontal scroll di layar kecil sehingga tetap dapat digunakan pada perangkat mobile maupun tablet.

---

## Teknologi yang Digunakan

| Teknologi | Versi | Fungsi |
|---|---|---|
| HTML5 | — | Struktur halaman |
| Tailwind CSS | CDN | Styling dan layout |
| JavaScript (ES6+) | — | Logika aplikasi & CRUD |
| LocalStorage API | — | Penyimpanan data persisten |
| Web File API | — | Export & Import JSON |
| Google Fonts | CDN | Font Syne & DM Sans |

---

## Catatan Teknis

### Penyimpanan
- Data disimpan di `localStorage` dengan key `lockervault_data`
- Format penyimpanan: Array of Object (JSON)
- Kapasitas LocalStorage umumnya **5–10 MB** per domain/file — lebih dari cukup untuk ribuan data loker

### Kompatibilitas Browser
Aplikasi kompatibel dengan semua browser modern:
- ✅ Google Chrome 90+
- ✅ Mozilla Firefox 88+
- ✅ Microsoft Edge 90+
- ✅ Safari 14+

### Keamanan Data
- Seluruh data hanya tersimpan **lokal di perangkat pengguna**
- Tidak ada data yang dikirim ke server manapun
- Tidak ada pelacakan, analytics, atau koneksi pihak ketiga (kecuali CDN font dan Tailwind untuk load pertama)

### Backward Compatibility
Data JSON yang diimpor tanpa field `createdAt` / `updatedAt` (dari versi lama) akan otomatis diisi dengan waktu saat import dilakukan, sehingga tidak terjadi error.

---

## 📁 Struktur File

```
📂 Folder Aplikasi/
├── 📄 index.html          ← Aplikasi utama (semua-dalam-satu)
├── 📄 loker-data.json     ← File backup data (hasil Export)
└── 📄 README.md           ← Dokumentasi ini
```

---

<div align="center">

**LockerVault** — Dibuat dengan ❤️ untuk kemudahan administrasi loker karyawan

*Seluruh data tersimpan lokal di perangkat Anda. Privasi terjaga.*

</div>
