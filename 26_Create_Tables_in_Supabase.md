# 🗄️ Tutorial Supabase: Membuat Tabel dengan Relasi Foreign Key

## 📋 Ringkasan Tutorial

Dalam tutorial komprehensif ini, Anda akan belajar cara membuat tabel di Supabase dengan relasi foreign key yang tepat. Kita akan membangun sistem profil pengguna dengan postingan, mendemonstrasikan konsep database penting seperti pemisahan schema, foreign key, dan cascade action.

## 🎯 Apa yang Akan Anda Bangun

### Arsitektur Database:

- **Tabel 1:** user - Profil pengguna publik
- **Tabel 2:** userPost - Postingan yang dibuat pengguna
- **Relasi:** Tabel yang terhubung dengan referential integrity

## 🚀 Memulai

### Langkah 1: Navigasi ke Table Editor

1. Buka dashboard proyek Supabase Anda
2. Klik **Table Editor** di sidebar sebelah kiri
3. Anda akan melihat schema yang berbeda di bagian atas:
   - **auth** - Berisi tabel autentikasi (users, sessions, dll.)
   - **public** - Di mana Anda akan membuat sebagian besar tabel kustom

## Memahami Schema

### 🔐 Schema Auth:

- Berisi data autentikasi sensitif
- Termasuk password terenkripsi, token auth
- Tabel users bawaan dengan kolom seperti:
  - `id` (uuid)
  - `email` (text)
  - `encrypted_password` (text)
  - `created_at` (timestamp)

### 🌐 Schema Public:

- Untuk data yang ingin Anda bagikan secara publik
- Informasi profil, postingan, komentar, dll.
- Di mana kita akan membuat tabel kustom

## 📊 Tabel 1: Membuat Tabel Profil Pengguna

### Langkah 2: Buat Tabel User

**Navigasi ke Schema Public**

1. Klik tab schema public
2. Klik "Create a new table"

**Setup Tabel Dasar**
- **Nama Tabel:** user
- **Deskripsi:** Informasi profil pengguna publik

**Konfigurasi Pengaturan Keamanan**

- **Enable Row Level Security (RLS):** ✅ Direkomendasikan
- Ini membatasi akses dan memerlukan kebijakan untuk query data
- Untuk tujuan pembelajaran, Anda bisa menonaktifkannya dulu

### Langkah 3: Definisikan Kolom Tabel User

Konfigurasi kolom-kolom berikut:

| Nama Kolom | Tipe | Nilai Default | Properti |
|------------|------|---------------|----------|
| user_id | uuid | NULL | Primary Key ✅ |
| created_at | timestamp | now() | Auto-timestamp |
| name | text | NULL | Nullable ✅ |
| email | text | NULL | Nullable ✅ |
| profilePic | text | NULL | Nullable ✅ |

**Detail Kolom:**

- **user_id:** Identifier unik yang akan terhubung ke auth.users
- **created_at:** Otomatis diatur saat record dibuat
- **name:** Nama tampilan pengguna
- **email:** Email publik (bisa berbeda dari email auth)
- **profilePic:** URL ke gambar profil (disimpan sebagai text)

### Langkah 4: Setup Relasi Foreign Key

#### Mengapa Foreign Key?
Foreign key menghubungkan tabel user publik Anda ke sistem autentikasi, memastikan konsistensi data.

#### Konfigurasi:

1. Klik "Add foreign key relation"
2. Pilih Schema: **auth**
3. Pilih Tabel: **users**
4. **Mapping Kolom:**
   - `public.user.user_id` → `auth.users.id`

5. **Aksi Referensial:**
   - On Update: No action
   - On Delete: Cascade ✅

**Arti Cascade:**
Ketika pengguna dihapus dari auth.users, profil mereka di public.user akan otomatis terhapus juga.

### Langkah 5: Simpan Tabel User

- Klik "Save" untuk membuat tabel
- Sistem akan otomatis memperbarui tipe user_id agar sesuai dengan auth.users.id (uuid)

## 📝 Tabel 2: Membuat Tabel Postingan Pengguna

### Langkah 6: Buat Tabel UserPost

**Buat Tabel Baru**
- **Nama Tabel:** userPost
- **Deskripsi:** Postingan dan konten yang dibuat pengguna

**Nonaktifkan RLS untuk Tutorial**

- Hapus centang "Enable Row Level Security"
- Ini membuat tabel dapat dibaca/ditulis secara publik untuk pembelajaran
- **Catatan Produksi:** Selalu aktifkan RLS di aplikasi nyata

### Langkah 7: Definisikan Kolom Tabel UserPost

Konfigurasi kolom-kolom berikut:

| Nama Kolom | Tipe | Nilai Default | Properti |
|------------|------|---------------|----------|
| post_id | int8 | NULL | Primary Key ✅ |
| created_at | timestamp | now() | Auto-timestamp |
| user_id | uuid | NULL | Foreign Key |
| postPic | text | NULL | Nullable ✅ |
| description | text | NULL | Nullable ✅ |

**Detail Kolom:**

- **post_id:** Identifier unik untuk setiap postingan
- **created_at:** Kapan postingan dibuat
- **user_id:** Terhubung ke pengguna yang membuat postingan
- **postPic:** URL ke gambar postingan
- **description:** Konten/caption postingan

### Langkah 8: Buat Foreign Key ke Tabel User

**Hubungkan Postingan ke Pengguna:**

1. Klik "Add foreign key relation"
2. Pilih Schema: **public**
3. Pilih Tabel: **user**
4. **Mapping Kolom:**
   - `public.userPost.user_id` → `public.user.user_id`

5. **Aksi Referensial:**
   - On Update: No action
   - On Delete: Cascade ✅

**Hasil:**
Ketika pengguna dihapus, semua postingan mereka akan otomatis terhapus juga.

### Langkah 9: Simpan Tabel UserPost

- Klik "Save" untuk membuat tabel
- Database Anda sekarang memiliki dua tabel yang terhubung!

## 🔗 Schema Database Final

### Struktur Tabel Lengkap

#### 🔐 auth.users (Bawaan)
```sql
├── id (uuid, PK)
├── email (text)
├── encrypted_password (text)
└── created_at (timestamp)
```

#### 👤 public.user
```sql
├── user_id (uuid, PK, FK → auth.users.id)
├── created_at (timestamp, default: now())
├── name (text, nullable)
├── email (text, nullable)
└── profilePic (text, nullable)
```

#### 📝 public.userPost
```sql
├── post_id (int8, PK)
├── created_at (timestamp, default: now())
├── user_id (uuid, FK → public.user.user_id)
├── postPic (text, nullable)
└── description (text, nullable)
```

### Alur Relasi
```
auth.users.id ←→ public.user.user_id ←→ public.userPost.user_id
```

## ✅ Tutorial Selesai!

### Apa yang Telah Anda Capai

#### 🏗️ Arsitektur Database:

- ✅ Membuat profil pengguna yang terhubung dengan autentikasi aman
- ✅ Membangun sistem konten yang dibuat pengguna
- ✅ Mengimplementasikan relasi foreign key yang tepat
- ✅ Menyiapkan penghapusan cascade untuk integritas data

#### 💡 Konsep Kunci yang Dipelajari:

- **Pemisahan Schema:** Data pribadi vs publik
- **Foreign Key:** Menghubungkan tabel terkait
- **Aksi Cascade:** Pembersihan otomatis
- **Tipe Data:** UUID untuk ID, text untuk konten
- **Row Level Security:** Kontrol akses

## 🎯 Langkah Selanjutnya

Berdasarkan roadmap pembelajaran, langkah berikutnya adalah:

### 📚 Tahap 3: User Authentication (Lanjutan)
- ✅ **26. Membuat Tabel di Supabase** - SELESAI

### 🔄 Tahap Berikutnya:

#### 27. 🔗 Menghubungkan FlutterFlow ke Supabase (2 menit)

- Konfigurasi koneksi antara FlutterFlow dan database Supabase
- Setup API keys dan environment variables
- Testing koneksi database

#### 28. 📝 Registrasi Pengguna (6 menit)

- Membuat form registrasi pengguna
- Implementasi sign-up functionality
- Validasi input dan error handling

#### 29. 🔐 Setup Login & Logout (2 menit)

- Membuat halaman login
- Implementasi fungsi logout
- Manajemen session pengguna

## 🚀 Persiapan untuk Tahap Berikutnya

Sebelum melanjutkan, pastikan:

- ✅ Database Supabase sudah terbuat dengan 2 tabel
- ✅ Foreign key relationships sudah dikonfigurasi
- ✅ Anda memiliki akses ke Supabase dashboard
- ✅ Project keys Supabase sudah dicatat

---

## 🎉 Selamat!

Anda telah berhasil membuat struktur database lengkap dengan relasi yang tepat. Database Supabase Anda sekarang siap untuk membangun aplikasi full-stack dengan profil pengguna dan manajemen konten!

### 💡 Tips: 
Simpan tutorial ini sebagai referensi saat melanjutkan ke tahap berikutnya. Struktur database yang solid adalah fondasi penting untuk fitur autentikasi dan manajemen pengguna yang akan kita bangun selanjutnya.
