# Tutorial Setup Supabase - Panduan Lengkap

## 📋 Daftar Isi
- [Pengenalan](#pengenalan)
- [Langkah 1: Membuat Akun Supabase](#langkah-1-membuat-akun-supabase)
- [Langkah 2: Sign In ke Akun](#langkah-2-sign-in-ke-akun)
- [Langkah 3: Membuat Project Baru](#langkah-3-membuat-project-baru)
- [Langkah 4: Konfigurasi Project](#langkah-4-konfigurasi-project)
- [Langkah 5: Mendapatkan API Keys](#langkah-5-mendapatkan-api-keys)
- [Troubleshooting](#troubleshooting)
- [Selanjutnya](#selanjutnya)

## Pengenalan

Supabase adalah platform Backend-as-a-Service (BaaS) yang menyediakan database PostgreSQL, authentication, real-time subscriptions, dan edge functions. Tutorial ini akan memandu Anda untuk melakukan setup awal Supabase.

> **💡 Tip:** Supabase menggunakan PostgreSQL sebagai database utama dan menyediakan API yang mudah digunakan.

## Langkah 1: Membuat Akun Supabase

### 1.1 Akses Website Supabase

1. Buka browser dan pergi ke [supabase.com](https://supabase.com)
2. Klik tombol **"Get started"** atau **"Sign Up"**

### 1.2 Pilih Metode Registrasi

Anda memiliki beberapa opsi untuk membuat akun:

- **Continue with GitHub** (Recommended)
- **Continue with SSO** 
- **Email dan Password**

### 1.3 Registrasi dengan Email

Jika memilih registrasi dengan email:

1. **Email**: Masukkan alamat email valid
   ```
   Contoh: flutterflowroutorial@gmail.com
   ```

2. **Password**: Buat password yang kuat
   - Minimal 8 karakter
   - Kombinasi huruf besar, kecil, angka, dan simbol
   - Contoh persyaratan yang ditampilkan:
     - ✅ Uppercase letter
     - ✅ Lowercase letter  
     - ✅ Number
     - ✅ Special character (e.g. !?@#$%)
     - ✅ 8 characters or more

3. Klik tombol **"Sign Up"**

## Langkah 2: Sign In ke Akun

### 2.1 Halaman Welcome Back

Setelah berhasil registrasi, Anda akan melihat halaman **"Welcome back"** untuk sign in.

### 2.2 Login ke Akun

1. **Email**: Masukkan email yang sudah didaftarkan
2. **Password**: Masukkan password Anda
3. Klik **"Sign In"**

> **⚠️ Catatan:** Jika Anda lupa password, klik link **"Forgot Password?"**

## Langkah 3: Membuat Project Baru

### 3.1 Halaman Create New Project

Setelah berhasil login, Anda akan diarahkan ke halaman pembuatan project baru.

### 3.2 Informasi Project

Anda akan melihat penjelasan tentang project:

- **Project akan memiliki instance PostgreSQL dedicated**
- **API akan di-setup otomatis** untuk interaksi dengan database
- **Full Postgres database** tersedia

## Langkah 4: Konfigurasi Project

### 4.1 Organization

1. **Organization**: Pilih atau buat organization
   ```
   Contoh: FlutterflowTutorial
   ```

### 4.2 Project Name

1. **Project name**: Berikan nama untuk project Anda
   ```
   Contoh: FlutterflowTutorial
   ```
   
> **💡 Tip:** Anda bisa menggunakan nama yang sama dengan organization atau nama yang lebih spesifik.

### 4.3 Database Password

1. **Database Password**: Password ini akan digunakan untuk akses database
   - Password akan ter-generate otomatis
   - Status: **"This password is strong"**
   - Anda bisa klik **"Generate a password"** untuk password baru
   - Klik tombol **"Copy"** untuk menyalin password

> **⚠️ Penting:** Simpan password ini dengan aman, Anda akan membutuhkannya nanti.

### 4.4 Region

1. **Region**: Pilih region terdekat dengan pengguna Anda
   ```
   Contoh: 🇩🇪 Central EU (Frankfurt)
   ```
   
2. **Rekomendasi**: "Select the region closest to your users for the best performance"

> **💡 Tip:** Untuk pengguna di Indonesia, region Singapore atau Tokyo biasanya memberikan performa terbaik.

### 4.5 Security Options

Klik **"SECURITY OPTIONS"** untuk konfigurasi tambahan (opsional untuk pemula).

### 4.6 Finalisasi Project

1. Review semua konfigurasi
2. Klik tombol **"Create new project"**

## Langkah 5: Mengakses API Keys

### 5.1 Project Setup Selesai

Setelah project berhasil dibuat, Supabase akan otomatis menyediakan:

- **Database PostgreSQL** yang siap digunakan
- **API endpoints** untuk akses data
- **API Keys** yang sudah ter-generate otomatis

### 5.2 Mengakses API Settings

1. Dari dashboard project, klik **Settings** di sidebar kiri (ikon gear)
2. Di section **"CONFIGURATION"**, pilih **API**
3. Anda akan melihat halaman **"API Settings"** dengan semua informasi yang diperlukan

**💡 Sidebar Navigation yang tersedia:**
- **PROJECT SETTINGS:** General, Compute and Disk, Infrastructure, Integrations, Add Ons, Vault
- **CONFIGURATION:** Database, Data API, Authentication, Storage, Edge Functions, Log Drains  
- **BILLING:** Subscription, Usage

### 5.3 Project URL

Di halaman API Settings, Anda akan menemukan:

**Project URL:**
```
https://[project-id].supabase.co
```
- URL ini adalah RESTful endpoint untuk query dan manage database
- Klik tombol **"Copy"** untuk menyalin URL

### 5.4 API Keys (Sudah Tersedia Otomatis)

⚠️ **Catatan Penting:** API Keys sudah otomatis ter-generate, tidak perlu dibuat manual.

#### 5.4.1 Anon/Public Key
```javascript
anon | public
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSI...
```

**Kegunaan:**
- ✅ Aman untuk digunakan di browser/aplikasi client
- ✅ Bekerja dengan Row Level Security 
- ✅ Mengikuti kebijakan keamanan yang dikonfigurasi
- Klik **"Copy"** untuk menyalin key

#### 5.4.2 Service Role Key (Secret)
```javascript
service_role | secret
**** **** **** ****
```

**⚠️ Peringatan Keamanan:**
- 🚫 **JANGAN bagikan key ini secara publik**
- 🚫 **Memiliki kemampuan bypass Row Level Security**
- ✅ Gunakan hanya di server-side/backend
- ✅ Jika bocor, segera generate JWT secret baru
- Klik **"Reveal"** untuk melihat key lengkap

### 5.5 Upcoming Changes (Q2 2025)

📢 **Info Penting:**
- `anon` dan `service_role` API keys akan berubah menjadi `publishable` dan `secret`
- Fungsionalitas tetap sama, hanya nama yang berubah
- Klik **"Read the announcement"** untuk detail lengkap

### 5.6 Copy API Keys

1. **Public Key:** Klik tombol **"Copy"** di sebelah anon key
2. **Secret Key:** Klik **"Reveal"** terlebih dahulu, lalu **"Copy"**
3. Simpan kedua keys ini dengan aman untuk digunakan di aplikasi

### 5.7 Menggunakan API Keys

**Di Aplikasi Frontend (React, Flutter, etc):**
```javascript
// Gunakan anon/public key
const supabaseUrl = 'https://your-project.supabase.co'
const supabaseAnonKey = 'your-anon-key'
```

**Di Backend/Server:**
```javascript
// Gunakan service_role/secret key (hati-hati!)
const supabaseUrl = 'https://your-project.supabase.co'  
const supabaseServiceKey = 'your-service-role-key'
```

## Troubleshooting

### Masalah Umum

1. **Project tidak terbuat setelah beberapa menit**
   - Coba refresh halaman
   - Periksa koneksi internet
   - Contact support jika masalah berlanjut

2. **Lupa Database Password**
   - Pergi ke Settings > Database
   - Reset password database jika diperlukan
   - Generate password baru

3. **Tidak bisa mengakses API Settings**
   - Pastikan project sudah selesai ter-setup
   - Refresh halaman dashboard
   - Periksa di sidebar Settings > API

4. **API Key tidak berfungsi**
   - Pastikan menggunakan anon key untuk client-side
   - Pastikan menggunakan service_role key untuk server-side
   - Periksa konfigurasi Row Level Security di tabel

## Selanjutnya

Setelah setup berhasil, Anda bisa:

1. **Membuat tabel database** pertama
2. **Setup authentication** untuk aplikasi
3. **Mengintegrasikan dengan aplikasi** (React, Flutter, dll)
4. **Menggunakan real-time features**

### Resources Berguna

- 📖 [Supabase Documentation](https://supabase.com/docs)
- 🎯 [Quick Start Guide](https://supabase.com/docs/guides/getting-started)
- 💬 [Community Discord](https://discord.supabase.com)
- 🎥 [Video Tutorials](https://supabase.com/docs/guides/getting-started#video-guide)

---

## 🎉 Selamat!

Anda telah berhasil melakukan setup Supabase. Project Anda siap digunakan untuk membangun aplikasi dengan backend yang powerful!

> **Next Step:** Mulai membuat tabel database dan implementasi authentication untuk aplikasi Anda.

---

**📝 Catatan Tutorial:**
- Tutorial ini berdasarkan Supabase versi terbaru
- Screenshot dan interface mungkin sedikit berbeda di masa mendatang
- Selalu rujuk ke dokumentasi resmi untuk update terbaru
