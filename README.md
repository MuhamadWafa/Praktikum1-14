# Laporan Praktikum Pemograman Web2
# Muhamad Wafa Mufida Zulfi
# 312410334
# I241D
# Ujian Akhir Semester
# Pemograman Web 2
# Agung Nugroho, S.Kom., M.Kom.


# 1. Deskripsi proyek
Aplikasi Sistem Manajemen Inventaris (E-Inventory) ini dibuat untuk memenuhi tugas UAS mata kuliah Pemrograman Web 2, dengan fokus pada pengelolaan data barang, kategori, supplier, dan stok.

Arsitektur yang digunakan adalah Decoupled Architecture, memisahkan backend dan frontend.
Backend: Menggunakan CodeIgniter 4 sebagai penyedia RESTful API.

Frontend: Menggunakan VueJS 3 (CDN), Vue Router, Axios, dan TailwindCSS untuk membangun antarmuka Single Page Application (SPA).

# Tema Studi Kasus
Tema: Sistem Manajemen Inventaris Barang (E-Inventory) dengan saya kasih nama PeyimpananXX

Cakupan & Fitur Utama Aplikasi:

- Login administrator
- Logout administrator
- Dashboard admin
- Menampilkan data barang
- Menambahkan data barang
- Mengedit data barang
- Menghapus data barang
- Menampilkan data kategori
- Menampilkan data supplier
- Proteksi endpoint API menggunakan Bearer Token
- Validasi akses halaman menggunakan Vue Router Navigation Guard
- Penyimpanan token login menggunakan localStorage
- Pengiriman token otomatis menggunakan Axios Interceptor

# Teknologi yang di gunakan
Backend
- PHP 8.2
- CodeIgniter 4
- RESTful API
- MySQL / MariaDB
- CodeIgniter Filter
- Bearer Token Authentication
- CORS Filter
- Frontend
HTML
- VueJS 3 CDN
- Vue Router CDN
- Axios CDN
- TailwindCSS CDN
- JavaScript Modular Component
Tools
XAMPP
- phpMyAdmin
- Visual Studio Code
- Browser
- PowerShell / CMD
- Git dan GitHub
# 4. Arsitekur Aplikasi
Aplikasi ini menggunakan arsitektur terpisah antara backend dan frontend
```
Frontend VueJS SPA
        |
        | Axios HTTP Request
        |
Backend CodeIgniter 4 RESTful API
        |
        | Query Database
        |
Database MySQL / MariaDB
```
Alamat Akses Sistem (URL)
Backend API: 🖥️
```
http://localhost:8080
```
Frontend : 🖥️
```
http://localhost:8080/frontend-spa/#/login
```
# 📂 5. Struktur Direktori Proyek
```
PENYIMPANANXX/ (Root Directory)
├── 🗄️ backend-api/                  # Server RESTful API (CodeIgniter 4)
│   ├── 📁 app/
│   │   ├── ⚙️ Config/
│   │   ├── 🎮 Controllers/
│   │   ├── 🛢️ Database/
│   │   ├── 🛡️ Filters/
│   │   ├── 🛠️ Helpers/
│   │   ├── 🗣️ Language/
│   │   ├── 📚 Libraries/
│   │   ├── 📊 Models/
│   │   ├── 📦 ThirdParty/
│   │   └── 🎨 Views/
│   ├── 🌐 public/                   # Folder Publik Akses Server
│   │   ├── 🎨 frontend-spa/          # Build/Salinan Frontend di Sisi Public Server
│   │   │   ├── 🖼️ views/
│   │   │   │   ├── 📄 Barang.js
│   │   │   │   ├── 📄 Dashboard.js
│   │   │   │   └── 📄 Login.js
│   │   │   └── 🌐 index.html
│   │   ├── 🛠️ .htaccess
│   │   ├── 🌟 favicon.ico
│   │   ├── ⚙️ index.php
│   │   └── 🤖 robots.txt
│   ├── ⚙️ system/                     # Core Framework CodeIgniter 4
│   ├── 🧪 tests/                      # Pengujian Aplikasi
│   ├── 📝 writable/                   # Folder Cache & Logs Server
│   ├── ⚙️ .env                        # Konfigurasi Environment & Database
│   ├── 📦 composer.json               # Dependensi Backend
│   ├── 💾 e_inventory.sql            # Backup Database MySQL
│   ├── 📄 LICENSE
│   ├── ⚙️ phpunit.dist.xml
│   ├── 🚀 preload.php
│   ├── 📄 README.md
│   └── ⚡ spark                        # CLI CodeIgniter 4
│
├── 🎨 frontend-spa/                 # Aplikasi Utama Frontend (VueJS 3 SPA)
│   ├── 📁 components/
│   └── 🌐 index.html
│
├── 🛠️ .htaccess
└── 📄 README.md                     # Dokumentasi Utama Proyek
```
# 🛢️ 6. Arsitektur Database & Relasi

```
├── e-inventory (Database)
│   ├── users (Tabel Data Pengguna/Admin)
│   │   ├── id (INT, Primary Key, Auto Increment)
│   │   ├── username (VARCHAR)
│   │   ├── password (VARCHAR)
│   │   ├── token (VARCHAR, Nullable)
│   │   └── created_at (TIMESTAMP)
│   │
│   ├── kategori (Tabel Kategori Barang)
│   │   ├── id (INT, Primary Key, Auto Increment)
│   │   ├── nama_kategori (VARCHAR)
│   │   └── created_at (TIMESTAMP)
│   │
│   ├── supplier (Tabel Pemasok Barang)
│   │   ├── id (INT, Primary Key, Auto Increment)
│   │   ├── nama_supplier (VARCHAR)
│   │   ├── kontak (VARCHAR)
│   │   ├── alamat (TEXT)
│   │   └── created_at (TIMESTAMP)
│   │
│   ├── barang (Tabel Data Inventaris Barang)
│   │   ├── id (INT, Primary Key, Auto Increment)
│   │   ├── kategori_id (INT, Foreign Key -> kategori.id)
│   │   ├── supplier_id (INT, Foreign Key -> supplier.id)
│   │   ├── user_id (INT, Foreign Key -> users.id)
│   │   ├── kode_barang (VARCHAR)
│   │   ├── nama_barang (VARCHAR)
│   │   ├── stok (INT)
│   │   └── harga (INT)
│   │
│   └── histori_stok (Tabel Riwayat Transaksi Stok)
│       ├── id (INT, Primary Key, Auto Increment)
│       ├── barang_id (INT, Foreign Key -> barang.id)
│       ├── jenis_transaksi (ENUM: 'masuk', 'keluar')
│       ├── jumlah (INT)
│       ├── keterangan (TEXT)
│       └── tanggal (TIMESTAMP)
```
# 🔐 7. Kredensial & Autentikasi Admin
```
Username: 🧑‍💻 admin
Password: 🔑 admin123
```
# 🔌 8. Pemetaan Endpoint API
Base URL 
```
http://localhost:8080
```

Data Master (Items, Categories, Suppliers): 📋
```
GET (Semua / Detail) ➔ 🔓 Akses Publik (Tanpa Token)
POST / PUT / DELETE ➔ 🔒 Akses Terproteksi (Wajib Bearer Token)
```
