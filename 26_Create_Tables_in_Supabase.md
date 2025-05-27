# Tutorial Supabase: Membuat Tabel dengan Relasi Foreign Key

## 📋 Daftar Isi
- [Pengenalan](#pengenalan)
- [Langkah 1: Navigasi ke Table Editor](#langkah-1-navigasi-ke-table-editor)
- [Langkah 2: Memahami Schema](#langkah-2-memahami-schema)
- [Langkah 3: Membuat Tabel User](#langkah-3-membuat-tabel-user)
- [Langkah 4: Setup Foreign Key ke Auth](#langkah-4-setup-foreign-key-ke-auth)
- [Langkah 5: Membuat Tabel UserPost](#langkah-5-membuat-tabel-userpost)
- [Langkah 6: Setup Foreign Key antar Tabel](#langkah-6-setup-foreign-key-antar-tabel)
- [Langkah 7: Schema Database Final](#langkah-7-schema-database-final)
- [Troubleshooting](#troubleshooting)
- [Selanjutnya](#selanjutnya)

## Pengenalan

Dalam tutorial komprehensif ini, Anda akan belajar cara membuat tabel di Supabase dengan relasi foreign key yang tepat. Kita akan membangun sistem profil pengguna dengan postingan, mendemonstrasikan konsep database penting seperti pemisahan schema, foreign key, dan cascade action.

> **💡 Tip:** Tutorial ini mengasumsikan Anda sudah memiliki project Supabase yang aktif. Jika belum, ikuti tutorial setup Supabase terlebih dahulu.

### 🎯 Apa yang Akan Anda Bangun

**Arsitektur Database:**
- **Tabel 1:** `user` - Profil pengguna publik
- **Tabel 2:** `userPost` - Postingan yang dibuat pengguna
- **Relasi:** Tabel yang terhubung dengan referential integrity

## Langkah 1: Navigasi ke Table Editor

### 1.1 Akses Table Editor

1. Buka dashboard proyek Supabase Anda
2. Klik **Table Editor** di sidebar sebelah kiri
3. Anda akan melihat schema yang berbeda di bagian atas:
   - **auth** - Berisi tabel autentikasi (users, sessions, dll.)
   - **public** - Di mana Anda akan membuat sebagian besar tabel kustom

> **📌 Catatan:** Pastikan Anda berada di project yang benar sebelum membuat tabel.

## Langkah 2: Memahami Schema

### 2.1 Schema Auth 🔐

**Karakteristik:**
- Berisi data autentikasi sensitif
- Termasuk password terenkripsi, token auth
- **Tabel users bawaan** dengan kolom:
  ```sql
  ├── id (uuid, Primary Key)
  ├── email (text)
  ├── encrypted_password (text)
  └── created_at (timestamp)
  ```

### 2.2 Schema Public 🌐

**Karakteristik:**
- Untuk data yang ingin Anda bagikan secara publik
- Informasi profil, postingan, komentar, dll.
- **Di sini kita akan membuat tabel kustom**

> **⚠️ Penting:** Jangan menyimpan data sensitif di schema public tanpa Row Level Security (RLS).

## Langkah 3: Membuat Tabel User

### 3.1 Setup Tabel Dasar

1. **Navigasi ke Schema Public**
   - Klik tab schema **public**
   - Klik **"Create a new table"**

2. **Informasi Tabel**
   - **Nama Tabel:** `user`
   - **Deskripsi:** `Public user profile information

<div align="center">
   <img src="https://github.com/user-attachments/assets/98989b5d-13a8-487e-9b5c-458e8c8db890" width="600">
</div>

### 3.2 Konfigurasi Keamanan

**Enable Row Level Security (RLS):**
- ❌ **Jangan dicentang** untuk tutorial ini
- Biarkan checkbox kosong agar tabel dapat diakses secara publik
- Sistem akan menampilkan peringatan: *"You are allowing anonymous access to your table"*
- Peringatan ini normal untuk keperluan pembelajaran

**Enable Realtime:**
- ❌ **Jangan dicentang** untuk tutorial ini
- Fitur realtime tidak diperlukan untuk pembelajaran dasar
- Dapat diaktifkan nanti jika dibutuhkan

**Pesan Peringatan yang Muncul:**
```
⚠️ You are allowing anonymous access to your table
The table user will be publicly writable and readable
```

> **⚠️ Penting:** Untuk tutorial ini, RLS sengaja dinonaktifkan agar mudah diakses. Di aplikasi production, selalu aktifkan RLS untuk keamanan data.

### 3.3 Definisi Kolom Tabel User

Konfigurasi kolom-kolom berikut:

| Nama Kolom | Tipe | Nilai Default | Properti |
|------------|------|---------------|----------|
| `user_id` | `int8` | `NULL` | Primary Key ✅ |
| `created_at` | `timestamp` | `now()` | Auto-timestamp |
| `name` | `text` | `NULL` | Nullable ✅ |
| `email` | `text` | `NULL` | Nullable ✅ |
| `profilePic` | `text` | `NULL` | Nullable ✅ |

**Penjelasan Kolom:**

1. **user_id:** Identifier unik bertipe integer (int8) sebagai Primary Key
2. **created_at:** Otomatis diatur saat record dibuat dengan fungsi now()
3. **name:** Nama tampilan pengguna (nullable)
4. **email:** Email publik pengguna (nullable)
5. **profilePic:** URL ke gambar profil disimpan sebagai text (nullable)

<div align="center">
   <img src="https://github.com/user-attachments/assets/bae488b8-6717-49a1-b315-f30c0fdcc56b" width="600">
</div>

## Langkah 4: Setup Foreign Key ke Auth

### 4.1 Mengapa Foreign Key?

Foreign key menghubungkan tabel user publik Anda ke sistem autentikasi, memastikan:
- **Konsistensi data** antara auth dan public schema
- **Referential integrity** - tidak ada user publik tanpa auth
- **Automatic cleanup** saat user dihapus

### 4.2 Konfigurasi Foreign Key

1. **Tambah Relasi**
   - Klik **"Add foreign key relation"**
   - Pilih Schema: **`auth`**
   - Pilih Tabel: **`users`**

2. **Mapping Kolom:**
   ```
   public.user.user_id → auth.users.id
   ```
<div align="center">
   <img src="https://github.com/user-attachments/assets/216e72a0-6402-4335-9c8a-e13db00c82f7" width="400">
</div>

3. **Aksi Referensial:**
   - **On Update:** No action
   - **On Delete:** Cascade ✅

<div align="center">
   <img src="https://github.com/user-attachments/assets/c6c68bb5-f873-4f43-8ce7-0a060b5552bb" width="400">
</div>

> **⚠️ Cascade Delete:** Ketika pengguna dihapus dari `auth.users`, profil mereka di `public.user` akan otomatis terhapus juga.

### 4.3 Simpan Tabel User

1. Klik **"Save"** untuk membuat tabel
2. Sistem akan otomatis memperbarui tipe `user_id` agar sesuai dengan `auth.users.id` (uuid)

## Langkah 5: Membuat Tabel UserPost

### 5.1 Setup Tabel Dasar

**Informasi Tabel:**
- **Nama Tabel:** `userPost`
- **Deskripsi:** `Postingan dan konten yang dibuat pengguna`

<div align="center">
   <img src="https://github.com/user-attachments/assets/7ceccd35-1fdc-44fe-82aa-fc4abf2393d7" width="600">
</div>

**Pengaturan Keamanan:**
- ❌ **Jangan centang "Enable Row Level Security"**
- ❌ **Jangan centang "Enable Realtime"**
- Biarkan kedua checkbox kosong (sama seperti tabel user sebelumnya)
- Ini membuat tabel dapat dibaca/ditulis secara publik untuk pembelajaran
- Sistem akan menampilkan peringatan yang sama tentang anonymous access

> **⚠️ Catatan Produksi:** Selalu aktifkan RLS di aplikasi nyata.

### 5.2 Definisi Kolom Tabel UserPost

Konfigurasi kolom-kolom berikut:

| Nama Kolom | Tipe | Nilai Default | Properti |
|------------|------|---------------|----------|
| `post_id` | `int8` | `NULL` | Primary Key ✅ |
| `created_at` | `timestamp` | `now()` | Auto-timestamp |
| `user_id` | `uuid` | `NULL` | Nullable ✅ |
| `postPic` | `text` | `NULL` | Nullable ✅ |
| `description` | `text` | `NULL` | Nullable ✅ |

**Penjelasan Kolom:**

1. **post_id:** Identifier unik untuk setiap postingan
2. **created_at:** Kapan postingan dibuat
3. **user_id:** Terhubung ke pengguna yang membuat postingan
4. **postPic:** URL ke gambar postingan
5. **description:** Konten/caption postingan

## Langkah 6: Setup Foreign Key antar Tabel

### 6.1 Hubungkan Postingan ke User

1. **Tambah Relasi**
   - Klik **"Add foreign key relation"**
   - Pilih Schema: **`public`**
   - Pilih Tabel: **`user`**

2. **Mapping Kolom:**
   ```
   public.userPost.user_id → public.user.user_id
   ```

3. **Aksi Referensial:**
   - **On Update:** No action
   - **On Delete:** Cascade ✅

**Hasil Cascade:**
- Ketika pengguna dihapus, semua postingan mereka akan otomatis terhapus juga
- Menjaga konsistensi data dan mencegah orphaned records

### 6.2 Simpan Tabel UserPost

1. Klik **"Save"** untuk membuat tabel
2. **Database Anda sekarang memiliki dua tabel yang terhubung!**

## Langkah 7: Schema Database Final

### 7.1 Struktur Tabel Lengkap

#### 🔐 auth.users (Bawaan Supabase)
```sql
├── id (uuid, PK)
├── email (text)
├── encrypted_password (text)
└── created_at (timestamp)
```

#### 👤 public.user (Dibuat Manual)
```sql
├── user_id (uuid, PK, FK → auth.users.id)
├── created_at (timestamp, default: now())
├── name (text, nullable)
├── email (text, nullable)
└── profilePic (text, nullable)
```

#### 📝 public.userPost (Dibuat Manual)
```sql
├── post_id (int8, PK)
├── created_at (timestamp, default: now())
├── user_id (uuid, FK → public.user.user_id)
├── postPic (text, nullable)
└── description (text, nullable)
```

### 7.2 Alur Relasi Database
```
auth.users.id ←→ public.user.user_id ←→ public.userPost.user_id
```

### 7.3 Konsep Kunci yang Dipelajari

- **Pemisahan Schema:** Data pribadi vs publik
- **Foreign Key:** Menghubungkan tabel terkait
- **Aksi Cascade:** Pembersihan otomatis
- **Tipe Data:** UUID untuk ID, text untuk konten
- **Row Level Security:** Kontrol akses

## Troubleshooting

### Masalah Umum

1. **Tabel tidak terbuat atau error saat save**
   - Periksa nama kolom tidak menggunakan reserved keywords
   - Pastikan tipe data sesuai dengan foreign key reference
   - Refresh halaman dan coba lagi

2. **Foreign Key gagal dibuat**
   - Pastikan tipe data kolom sama (uuid ke uuid)
   - Periksa apakah tabel reference sudah ada
   - Cek apakah nama schema dan tabel sudah benar

3. **Error saat mengakses tabel**
   - Periksa pengaturan Row Level Security
   - Pastikan API keys sudah benar
   - Cek policy jika RLS diaktifkan

4. **Data tidak sinkron antar tabel**
   - Periksa apakah cascade action sudah dikonfigurasi
   - Test dengan menghapus data dari tabel parent
   - Pastikan foreign key constraint aktif

### Debug Steps

1. **Cek struktur tabel di SQL Editor:**
   ```sql
   -- Lihat struktur tabel
   \d public.user
   \d public.userPost
   
   -- Cek foreign key constraints
   SELECT * FROM information_schema.table_constraints 
   WHERE table_name IN ('user', 'userPost');
   ```

2. **Test relasi dengan query:**
   ```sql
   -- Test join antar tabel
   SELECT u.name, p.description 
   FROM public.user u 
   JOIN public.userPost p ON u.user_id = p.user_id;
   ```

## Selanjutnya

### 🎯 Langkah Berikutnya dalam Roadmap

Berdasarkan roadmap pembelajaran:

#### ✅ **26. Membuat Tabel di Supabase** - SELESAI

#### 🔄 Tahap Berikutnya:

**27. 🔗 Menghubungkan FlutterFlow ke Supabase (2 menit)**
- Konfigurasi koneksi antara FlutterFlow dan database Supabase
- Setup API keys dan environment variables
- Testing koneksi database

**28. 📝 Registrasi Pengguna (6 menit)**
- Membuat form registrasi pengguna
- Implementasi sign-up functionality
- Validasi input dan error handling

**29. 🔐 Setup Login & Logout (2 menit)**
- Membuat halaman login
- Implementasi fungsi logout
- Manajemen session pengguna

### 🚀 Persiapan untuk Tutorial Berikutnya

Pastikan Anda sudah memiliki:

- ✅ Database Supabase dengan 2 tabel (`user` dan `userPost`)
- ✅ Foreign key relationships sudah dikonfigurasi
- ✅ Akses ke Supabase dashboard
- ✅ Project URL dan API keys sudah dicatat

### Yang Perlu Disiapkan

Untuk tutorial selanjutnya, siapkan:

- **Supabase Project URL** - Dari dashboard Settings > API
- **Supabase Anon Key** - Untuk koneksi client-side
- **FlutterFlow Account** - Platform untuk membuat aplikasi
- **Screenshot/dokumentasi** - Untuk mengikuti tutorial

### Resources Berguna

- 📖 [Supabase Table Editor Guide](https://supabase.com/docs/guides/database)
- 🔗 [Foreign Key Documentation](https://supabase.com/docs/guides/database/tables#foreign-key-constraints)
- 🛡️ [Row Level Security Guide](https://supabase.com/docs/guides/auth/row-level-security)
- 💬 [Community Discord](https://discord.supabase.com)

---

## 🎉 Selamat!

Anda telah berhasil membuat struktur database lengkap dengan relasi yang tepat. Database Supabase Anda sekarang siap untuk membangun aplikasi full-stack dengan profil pengguna dan manajemen konten!

> **💡 Tips:** Simpan tutorial ini sebagai referensi saat melanjutkan ke tahap berikutnya. Struktur database yang solid adalah fondasi penting untuk fitur autentikasi dan manajemen pengguna yang akan kita bangun selanjutnya.

---

**📝 Catatan Tutorial:**
- Tutorial ini berdasarkan Supabase versi terbaru
- Interface mungkin sedikit berbeda di masa mendatang
- Selalu rujuk ke dokumentasi resmi untuk update terbaru
