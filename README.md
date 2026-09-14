# 🚀 Cara Hosting Master TraderBot AI di Vercel

Aplikasi **Master TraderBot AI** siap dihosting secara instan dan 100% gratis di Vercel, lengkap dengan database serverless Postgres dan Cron Jobs otomatis agar robot trading AI Anda bisa terus aktif mengevaluasi pasar 24/7!

---

## 🛠️ Langkah 1: Persiapan Database PostgreSQL
Aplikasi ini membutuhkan database PostgreSQL. Anda bisa menggunakan layanan gratis yang ramah serverless:
1. **Supabase** (supabase.com) atau **Neon** (neon.tech).
2. Buat database baru dan salin **Connection String** database Anda (`DATABASE_URL`). Formatnya seperti berikut:
   ```env
   postgres://username:password@your-database-host.neon.tech/neondb?sslmode=require
   ```

---

## 📦 Langkah 2: Deploy ke Vercel (Cara Cepat)

1. Pastikan kode Anda sudah berada di repositori **GitHub**.
2. Masuk ke **Vercel** (vercel.com) dan hubungkan akun GitHub Anda.
3. Klik **Add New** -> **Project** lalu pilih repositori proyek ini.
4. Di bagian **Environment Variables**, tambahkan variabel berikut:
   - `DATABASE_URL`: Masukkan connection string database PostgreSQL Anda dari Langkah 1.
5. Klik **Deploy**! Vercel akan otomatis mengompilasi, mem-build, dan merilis aplikasi Anda.

---

## ⚙️ Langkah 3: Menjalankan Migrasi Database di Produksi
Setelah deploy selesai, database PostgreSQL Anda perlu diisi dengan skema tabel Master TraderBot AI.
1. Jalankan perintah migrasi langsung lewat terminal komputer Anda (dengan menyetel `.env` lokal ke URL database produksi Anda) atau gunakan Vercel Serverless Function Console:
   ```bash
   npx drizzle-kit push
   ```
2. Atau Anda bisa melakukan verifikasi instan dengan memicu endpoint `/api/health` setelah deploy untuk memastikan serverless function Next.js terhubung dengan lancar ke database.

---

## ⏰ Langkah 4: Aktifkan Bot Trading 24/7 dengan Vercel Cron
Agar robot trading AI Anda bisa otomatis mengevaluasi sinyal buy/sell dan melakukan order setiap menit, kita mengintegrasikan fitur **Vercel Cron Jobs**!

1. Berkas `vercel.json` di proyek ini sudah dikonfigurasi untuk memicu endpoint tick otomatis:
   ```json
   {
     "crons": [
       {
         "path": "/api/bots/tick",
         "schedule": "*/1 * * * *"
       }
     ]
   }
   ```
2. **Cara Mengaktifkannya di Vercel**:
   - Buka dashboard proyek Anda di Vercel.
   - Pergi ke tab **Settings** -> **Cron Jobs**.
   - Vercel akan membaca konfigurasi `vercel.json` dan Anda tinggal menekan tombol **Enable** / **Create** untuk menyetujuinya.
   - Mulai sekarang, Vercel akan memanggil `/api/bots/tick` secara otomatis setiap 1 menit untuk menggerakkan seluruh robot trading aktif Anda!

---

## 🔑 Environment Variables Terpenting di Vercel

| Nama Variabel | Wajib/Opsional | Deskripsi |
|---|---|---|
| `DATABASE_URL` | **Wajib** | Connection String PostgreSQL (mis. Neon / Supabase / Vercel Postgres) |

---

## ✨ Keunggulan Arsitektur di Vercel
- **Zero-Cold Start & Fast Loading**: Next.js App Router dibuild secara optimal menjadi serverless edge functions.
- **Singapore Region (SIN1)**: Berkas `vercel.json` sudah dikonfigurasikan di region Singapura agar latensi data ke Binance API sangat dekat dan cepat.
- **100% Gratis**: Batas gratis Vercel + database serverless Postgres gratis (seperti Neon) sudah sangat lebih dari cukup untuk menjalankan 10 bot trading Master TraderBot AI Anda!
