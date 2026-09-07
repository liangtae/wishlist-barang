# wishlist-barang
🌸 Sakura-gan (桜願) — Wishlist Ku  Catatan keinginan &amp; incaran belanja bergaya Jepang, langsung di browser kamu.

<div align="center">

# 🌸 Sakura-gan (桜願) — Wishlist Ku

**Catatan keinginan & incaran belanja bergaya Jepang, langsung di browser kamu.**

Single-file web app untuk mencatat barang yang ingin dibeli — lengkap dengan harga, link toko, kategori, tag, dan thumbnail — dibungkus tema washi & kelopak sakura, tanpa server, tanpa instalasi.

[![Made with HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](#)
[![Made with CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)](#)
[![Made with JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![No Build Step](https://img.shields.io/badge/build-none%20needed-brightgreen)](#)

</div>

---

## 📖 Daftar isi

- [Tentang](#-tentang)
- [Cuplikan tampilan](#-cuplikan-tampilan)
- [Fitur](#-fitur)
- [Teknologi](#-teknologi)
- [Cara menjalankan](#-cara-menjalankan)
- [Struktur data](#-struktur-data)
- [Struktur proyek](#-struktur-proyek)
- [Kustomisasi](#-kustomisasi)
- [Batasan yang perlu diketahui](#-batasan-yang-perlu-diketahui)
- [Roadmap](#-roadmap)
- [Kontribusi](#-kontribusi)
- [Lisensi](#-lisensi)

## 🎴 Tentang

**Sakura-gan** adalah aplikasi pencatat wishlist belanja yang berjalan sepenuhnya di sisi klien (*client-side*) — satu file HTML tunggal berisi HTML5, CSS3, dan JavaScript murni tanpa framework maupun proses build. Semua data disimpan di `localStorage` milik browser, sehingga privat dan tidak memerlukan backend, akun, atau koneksi internet untuk pemakaian sehari-hari (koneksi hanya dibutuhkan saat mengekspor ke Excel/PDF, karena pustaka tersebut dimuat dari CDN).

Cocok untuk siapa saja yang ingin melacak barang incaran — gadget, fashion, buku, mainan, apa saja — lengkap dengan harga, link toko, kategori, dan catatan pribadi, tanpa perlu daftar aplikasi pihak ketiga.

## 🖼 Cuplikan tampilan

> Tambahkan tangkapan layar aplikasi di sini setelah repo dibuat, misalnya:
>
> ```md
> ![Tampilan mode terang](./docs/screenshot-light.png)
> ![Tampilan mode gelap](./docs/screenshot-dark.png)
> ```

## ✨ Fitur

**Manajemen barang**
- CRUD penuh (tambah, lihat, ubah, hapus) dengan modal form
- Kolom lengkap: nama, harga, kategori, tag, link pembelian, catatan, thumbnail, status favorit
- Validasi form (nama, harga, kategori wajib; format link diverifikasi)
- Soft delete — barang terhapus masuk ke "Sampah", bisa dipulihkan atau dihapus permanen
- Auto-increment nomor urut + UUID unik di setiap barang
- Unggah thumbnail dengan kompresi otomatis (disimpan sebagai base64)

**Navigasi & pencarian**
- Pencarian teks bebas (nama, catatan, tag)
- Filter kategori, tag, dan favorit
- Sortir (terbaru, terlama, harga, nama, favorit)
- Tampilan grid & daftar
- Paginasi dengan rentang tampilan dan pilihan jumlah item per halaman

**Produktivitas**
- Pilih banyak (bulk select) + aksi massal: favoritkan, hapus, pulihkan, hapus permanen
- Ekspor data ke CSV, Excel (.xlsx), dan PDF
- Impor data dari CSV/Excel dengan pemetaan kolom otomatis
- Riwayat aktivitas (audit trail) untuk semua aksi penting
- Reset data, reset pengaturan, atau reset semuanya — masing-masing dengan modal konfirmasi
- Notifikasi toast untuk setiap aksi

**Tampilan & nuansa**
- Tema terang & gelap (mode washi siang / indigo malam)
- Palet warna & tipografi bernuansa Jepang (Shippori Mincho + Zen Maru Gothic)
- Animasi kelopak sakura berguguran di latar (bisa dimatikan di pengaturan)
- Animasi loading bergaya gerbang torii saat aplikasi pertama dibuka
- Responsif untuk layar mobile, mendukung `prefers-reduced-motion`

## 🛠 Teknologi

| Bagian | Teknologi |
|---|---|
| Struktur & markup | HTML5 |
| Tampilan | CSS3 (custom properties, tanpa framework CSS) |
| Logika | JavaScript (vanilla, ES6+) |
| Penyimpanan | `localStorage` browser |
| Font | Google Fonts — Shippori Mincho, Zen Maru Gothic |
| Ekspor/impor Excel | [SheetJS (xlsx)](https://cdnjs.com/libraries/xlsx) via CDN |
| Ekspor PDF | [jsPDF](https://cdnjs.com/libraries/jspdf) + [jsPDF-AutoTable](https://cdnjs.com/libraries/jspdf-autotable) via CDN |

Tidak ada dependensi npm, tidak ada langkah build — cukup satu file `.html`.

## 🚀 Cara menjalankan

### Opsi 1 — buka langsung
1. Unduh atau clone repo ini.
2. Klik dua kali `wishlist.html`, atau buka lewat menu *File > Open* di browser.

```bash
git clone https://github.com/<username>/<nama-repo>.git
cd <nama-repo>
```

### Opsi 2 — jalankan lewat server lokal (opsional, disarankan untuk fitur upload gambar di beberapa browser)
```bash
# Python 3
python3 -m http.server 8080

# atau Node.js
npx serve .
```
Lalu buka `http://localhost:8080/wishlist.html` di browser.

### Opsi 3 — GitHub Pages
Aktifkan GitHub Pages dari `Settings > Pages`, pilih branch `main` dan folder root, lalu akses melalui:
```
https://<username>.github.io/<nama-repo>/wishlist.html
```

## 🗂 Struktur data

Data disimpan di `localStorage` browser dengan kunci berikut:

| Kunci | Isi |
|---|---|
| `wku_items` | Array seluruh barang wishlist (aktif & sampah) |
| `wku_activity` | Riwayat aktivitas (maksimum 300 entri terakhir) |
| `wku_settings` | Preferensi pengguna: tema, jumlah item per halaman, status animasi sakura, penomoran otomatis |

Contoh satu entri barang:
```json
{
  "id": "b3f1c2...-uuid",
  "seq": 12,
  "name": "Kamera Fujifilm X100VI",
  "price": 25000000,
  "category": "Elektronik",
  "tags": ["kamera", "impian"],
  "link": "https://contoh-toko.com/produk",
  "notes": "Warna hitam, tunggu diskon akhir tahun",
  "favorite": true,
  "thumbnail": "data:image/jpeg;base64,...",
  "status": "active",
  "createdAt": "2026-01-01T00:00:00.000Z",
  "updatedAt": "2026-01-01T00:00:00.000Z",
  "deletedAt": null
}
```

> Karena data tersimpan per-browser/per-perangkat, gunakan fitur **Ekspor** secara berkala sebagai cadangan, atau **Impor** untuk memindahkan data ke perangkat lain.

## 📁 Struktur proyek

```
.
├── wishlist.html     # Seluruh aplikasi (HTML + CSS + JS dalam satu file)
├── README.md         # Dokumen ini
├── LICENSE           # Lisensi MIT
└── CHANGELOG.md      # Catatan perubahan versi
```

## 🎨 Kustomisasi

Semua token desain berada di bagian `:root` dan `[data-theme="dark"]` pada blok `<style>` di `wishlist.html`, contoh:

```css
:root{
  --sakura:#E4A0B7;   /* warna aksen utama */
  --aka:#BC4A3C;       /* warna aksi/tombol utama */
  --matsu:#5F8566;      /* warna sukses/sekunder */
  --font-display:'Shippori Mincho', serif;
  --font-body:'Zen Maru Gothic', sans-serif;
}
```

Ubah nilai variabel ini untuk mengganti palet warna atau tipografi tanpa menyentuh logika JavaScript.

## ⚠️ Batasan yang perlu diketahui

- Data tersimpan lokal per browser — tidak otomatis tersinkron antar perangkat.
- Ekspor ke Excel dan PDF membutuhkan koneksi internet (memuat pustaka dari CDN).
- Kapasitas `localStorage` terbatas (umumnya 5–10MB); thumbnail dikompresi otomatis, namun koleksi wishlist yang sangat besar dengan banyak gambar tetap bisa mendekati batas ini.
- Tidak ada autentikasi/login — siapa pun yang memakai browser/perangkat yang sama dapat melihat dan mengubah data.

## 🗺 Roadmap

- [ ] Sinkronisasi opsional ke penyimpanan cloud (mis. Google Drive)
- [ ] Mode multi-wishlist / folder
- [ ] Pengingat harga (price tracking) otomatis
- [ ] Progressive Web App (PWA) agar bisa dipasang sebagai aplikasi

## 🤝 Kontribusi

Kontribusi, laporan bug, dan ide fitur dipersilakan lewat [Issues](../../issues) atau [Pull Request](../../pulls). Lihat [CONTRIBUTING.md](./CONTRIBUTING.md) untuk panduan lebih lengkap.

## 📄 Lisensi

Proyek ini dilisensikan di bawah [Lisensi MIT](./LICENSE) — bebas digunakan, dimodifikasi, dan didistribusikan ulang.

---

<div align="center">

Dibuat dengan 🌸 nuansa washi & sakura.

</div>
