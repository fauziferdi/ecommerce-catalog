# Ecommerce Catalog

Aplikasi web Vue.js untuk menampilkan katalog produk ecommerce dengan navigasi produk yang interaktif. Aplikasi ini mengambil data produk dari [FakeStore API](https://fakestoreapi.com) dan menampilkannya dengan antarmuka yang modern dan responsif.

## 📋 Fitur

- **Tampilan Produk**: Menampilkan detail produk termasuk gambar, judul, harga, kategori, dan deskripsi
- **Navigasi Produk**: Navigasi antara produk dengan tombol Previous dan Next (siklus 1-20)
- **Kategori Produk**: 
  - Menampilkan produk dengan kategori "men's clothing" dan "women's clothing"
  - Styling berbeda untuk setiap kategori (biru untuk men's, pink untuk women's)
  - Menampilkan pesan khusus untuk produk dengan kategori lain

## 🛠️ Teknologi yang Digunakan

- **Vue.js 3.2.13** - Framework JavaScript
- **Vue CLI 5.0** - Build tools dan development server
- **Babel** - JavaScript compiler
- **ESLint** - Code linting
- **CSS Variables** - Untuk theming dan styling dinamis

## 📁 Struktur Folder

```
ecommerce-catalog/
│
├── public/                    # File publik
│   ├── favicon.ico           # Favicon aplikasi
│   └── index.html            # Template HTML utama
│
├── src/                       # Source code aplikasi
│   ├── assets/               # Asset statis
│   │   └── logo.png          # Logo aplikasi
│   │
│   ├── components/           # Komponen Vue
│   │   ├── AppHeader.vue     # Komponen header/navbar
│   │   ├── AppFooter.vue     # Komponen footer
│   │   └── ProductCard.vue   # Komponen card produk
│   │
│   ├── App.vue               # Komponen utama aplikasi
│   ├── main.js               # Entry point aplikasi
│   └── style.css             # Global styles dan CSS variables
│
├── babel.config.js           # Konfigurasi Babel
├── jsconfig.json             # Konfigurasi JavaScript
├── vue.config.js             # Konfigurasi Vue CLI
├── package.json              # Dependencies dan scripts
├── package-lock.json         # Lock file untuk dependencies
└── README.md                 # Dokumentasi proyek (file ini)

```

## 🚀 Instalasi

Pastikan Anda telah menginstall [Node.js](https://nodejs.org/) (versi 14 atau lebih baru) dan [npm](https://www.npmjs.com/).

1. **Clone repository** atau download proyek ini
   ```bash
   cd ecommerce-catalog
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

## 💻 Penggunaan

### Development Server

Jalankan development server dengan hot-reload:

```bash
npm run serve
```

Aplikasi akan berjalan di `http://localhost:8080` (atau port lainnya jika 8080 sudah digunakan).

### Build untuk Production

Buat build production yang dioptimasi:

```bash
npm run build
```

File build akan tersimpan di folder `dist/`.

### Linting

Jalankan ESLint untuk memeriksa kode:

```bash
npm run lint
```

## 🎨 Komponen Aplikasi

### App.vue
Komponen utama yang mengelola state aplikasi, fetching data produk dari API, dan navigasi antar produk.

### AppHeader.vue
Header dengan navbar yang menampilkan:
- Brand name "Ecommerce Catalog"
- Link Home/Reset untuk kembali ke produk pertama
- Kategori produk saat ini

### ProductCard.vue
Komponen untuk menampilkan detail produk:
- Informasi produk (judul, kategori, harga, deskripsi)
- Gambar produk
- Styling dinamis berdasarkan kategori
- Pesan khusus untuk produk yang tidak tersedia

### AppFooter.vue
Footer yang menampilkan copyright dan ID produk saat ini.

## 📡 API

Aplikasi menggunakan [FakeStore API](https://fakestoreapi.com) untuk mengambil data produk:

```
GET https://fakestoreapi.com/products/{id}
```

Aplikasi mengambil produk dengan ID 1-20 secara berurutan.

## 🎨 Styling

Aplikasi menggunakan CSS Variables untuk theming:

- **Men's Clothing**: Biru (`#0077B6`)
- **Women's Clothing**: Pink (`#E91E63`)
- **Unavailable**: Orange (`#FF5722`)

## 📝 Scripts Tersedia

- `npm run serve` - Menjalankan development server
- `npm run build` - Build aplikasi untuk production
- `npm run lint` - Menjalankan ESLint untuk code checking

## 👤 Author

Fauzi Ferdiansyah

## 📄 License

Proyek ini adalah proyek Untuk 

---

**Catatan**: Aplikasi ini dibuat untuk pembelajaran dan demonstrasi penggunaan Vue.js dengan komponen yang reusable dan state management sederhana.

