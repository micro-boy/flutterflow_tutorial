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

## Langkah 5: Mendapatkan API Keys

### 5.1 Project Setup

Setelah project dibuat, Supabase akan melakukan provisioning:

- **"Setting up project"** - Status akan ditampilkan
- **"We are provisioning your database and API endpoints"**
- **"This may take a few minutes"**

### 5.2 Sambil Menunggu

Selama proses setup, Anda bisa:

- **Browse Supabase documentation** 
- **Try refreshing after a couple of minutes**
- **Contact support team** jika ada masalah

### 5.3 Project API Keys

Setelah setup selesai, Anda akan mendapatkan:

#### 5.3.1 Public API Key (anon/public)
```javascript
// Contoh format (jangan gunakan key ini)
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSI...
```

**Kegunaan:**
- Aman untuk digunakan di browser
- Untuk Row Level Security pada tabel
- Sesuai dengan kebijakan yang dikonfigurasi

#### 5.3.2 Service Role Key (secret)
```javascript
// Key ini memiliki kemampuan bypass Row Level Security
**** **** **** ****
```

**⚠️ Peringatan:**
- **Jangan bagikan key ini secara publik**
- **Memiliki kemampuan bypass Row Level Security**
- Gunakan hanya di server-side

### 5.4 Client Documentation

Klik **"Client Docs"** untuk melihat dokumentasi penggunaan API.

## Troubleshooting

### Masalah Umum

1. **Project tidak terbuat setelah beberapa menit**
   - Coba refresh halaman
   - Periksa koneksi internet
   - Contact support jika masalah berlanjut

2. **Lupa Database Password**
   - Anda bisa reset password di project settings
   - Generate password baru jika diperlukan

3. **API Key tidak muncul**
   - Tunggu hingga provisioning selesai
   - Refresh halaman
   - Periksa di tab "Settings" > "API"

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
