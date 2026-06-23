# 🎨 ExcaliDash - Self-Hosted Collaborative Whiteboard

ExcaliDash adalah platform *whiteboarding* kolaboratif berbasis [Excalidraw](https://excalidraw.com/) yang di-*host* secara mandiri (*self-hosted*). Platform ini dilengkapi dengan *dashboard* manajemen untuk menyimpan, mengatur, dan berkolaborasi pada diagram atau sketsa secara *real-time* dengan aman di dalam infrastruktur sendiri.

🌐 **Akses Aplikasi:** [https://excalidraw.niandev.com](https://excalidraw.niandev.com)

## ✨ Fitur Utama

* **Penyimpanan Permanen (Persistent Storage):** Semua hasil gambar dan diagram disimpan secara aman di dalam *database* lokal (SQLite), tidak akan hilang saat sesi peramban ditutup.
* **Kolaborasi Real-Time:** Mendukung kolaborasi multi-pengguna secara langsung tanpa hambatan (*lag-free*) melalui koneksi WebSockets.
* **Dashboard Manajemen:** Antarmuka pengguna (*frontend*) untuk mengatur kumpulan diagram, pencarian cepat, dan manajemen koleksi (*drag-and-drop*).
* **Autentikasi Pengguna:** Dilengkapi dengan sistem *login* (mode lokal) untuk menjaga privasi dokumen dan membatasi akses hanya kepada tim yang memiliki kredensial.
* **Impor & Ekspor:** Kompatibel penuh dengan format `.excalidraw` standar.

## 🏗️ Arsitektur & Teknologi

Layanan ini di-*deploy* menggunakan ekosistem *container* dengan spesifikasi berikut:

* **Frontend:** Nginx (merutekan trafik internal API dan WebSockets ke backend).
* **Backend:** Node.js / Prisma.
* **Database:** SQLite.
* **Reverse Proxy:** Traefik (menangani *routing* domain publik, SSL/TLS Let's Encrypt secara otomatis).
* **Orkestrasi:** Docker Compose.

## 🚀 Panduan Deployment

### Persyaratan Sistem
* Docker & Docker Compose terinstal.
* Jaringan Traefik (eksternal) sudah dikonfigurasi dan berjalan.
* Domain yang sudah diarahkan ke IP Server.

### Langkah Instalasi

1. **Kloning Repository:**
   Siapkan direktori proyek dan pastikan terdapat dua file utama: `docker-compose.yml` dan `nginx.conf`.

2. **Atur Variabel Lingkungan (Environment Variables):**
   Buka file `docker-compose.yml` dan pastikan Anda telah mengganti nilai `JWT_SECRET` dan `CSRF_SECRET` dengan string acak kriptografis (misal: menggunakan `openssl rand -hex 32`).

3. **Jalankan Layanan:**
   Eksekusi perintah berikut di terminal:
   ```bash
   docker compose up -d
