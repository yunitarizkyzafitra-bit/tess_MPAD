# M-PAD CIKASDA — Executive Dashboard

Aplikasi dashboard manajemen Pendapatan Asli Daerah (PAD) untuk Dinas Cipta Karya dan Sumber Daya Air, Provinsi Sulawesi Tengah. Aplikasi ini adalah **single-page application** berbasis HTML/JS murni (tanpa proses build) yang mengambil dan menulis data ke Google Sheets melalui Google Apps Script.

## Struktur Proyek

```
.
├── index.html          # Seluruh aplikasi (markup, style, dan logika JS)
├── assets/
│   ├── 73773_2.jpg     # Foto gedung (tampil di header/sidebar)
│   └── logo_sulteng.png# Logo Pemprov Sulteng (tampil di kop surat cetak)
└── README.md
```

> **Penting:** `index.html` saat ini mereferensikan gambar dengan nama file `73773_2.jpg` dan `logo_sulteng.png` di root. Letakkan kedua gambar Anda di folder `assets/` lalu perbarui path-nya di `index.html` (cari `src="73773_2.jpg"` dan `src="logo_sulteng.png"`, ganti menjadi `src="assets/73773_2.jpg"` dan `src="assets/logo_sulteng.png"`), atau letakkan langsung di root repo bila ingin path tetap sama.

## Menjalankan Secara Lokal

Karena murni HTML/JS, tidak perlu instalasi apa pun:

1. Clone repo ini.
2. Buka `index.html` langsung di browser, **atau** jalankan server lokal ringan agar `fetch()` ke Apps Script tidak terblokir kebijakan `file://`:
   ```bash
   # Python 3
   python3 -m http.server 8000
   # lalu buka http://localhost:8000
   ```

## Menghubungkan ke Sumber Data (Google Apps Script)

Cari konstanta berikut di bagian `<script>` paling bawah pada `index.html`:

```js
const APPS_SCRIPT_URL = "https://script.google.com/macros/s/XXXX/exec";
```

Ganti dengan URL Web App Apps Script Anda sendiri (Deploy → New deployment → Web app, akses "Anyone").

## Bagian yang Bisa Anda Ubah

| Ingin mengubah... | Cari di kode... |
|---|---|
| Warna & tema | `tailwind.config` di bagian `<head>` (palet `cikasda`) |
| Target PAD tahunan default | variabel `targetPADTahun` |
| Katalog objek sewa default | array `daftarObjekSewa` |
| Biodata Kepala Dinas default | objek `biodataKadis` |
| Menu sidebar | elemen `<nav>` di dalam `<aside id="sidebar">` dan `<aside id="sidebar-mobile">`, plus fungsi `switchView()` |
| Kop surat & format cetak PDF | blok `<div id="area-cetak-dokumen">` dan fungsi `cetakLaporanResmiPDF()` |

## Deploy Gratis via GitHub Pages

1. Push repo ini ke GitHub (lihat langkah di percakapan/README bagian bawah).
2. Buka **Settings → Pages** di repo GitHub Anda.
3. Pada **Source**, pilih branch `main` dan folder `/root`, lalu **Save**.
4. Setelah beberapa menit, aplikasi akan tersedia di `https://<username>.github.io/<nama-repo>/`.

## Lisensi Internal

Kode ini dibuat untuk kebutuhan internal Dinas CIKASDA Provinsi Sulawesi Tengah. Silakan sesuaikan sepenuhnya.
