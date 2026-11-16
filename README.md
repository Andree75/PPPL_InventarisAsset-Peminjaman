# 🏫 CampusAsset
### Sistem Manajemen Inventory & Asset Lifecycle Kampus

> ⚠️ **Ini adalah lingkungan simulasi untuk keperluan pendidikan. Bukan sistem resmi UISI.**

![Status](https://img.shields.io/badge/status-in%20development-yellow)
![Mata Kuliah](https://img.shields.io/badge/matkul-IF13PP13-blue)
![Versi](https://img.shields.io/badge/versi-0.1--draft-lightgrey)

---

## 📌 Tentang Proyek

**CampusAsset** adalah aplikasi web untuk mengelola siklus hidup aset kampus secara terpusat — mulai dari registrasi, penempatan, mutasi, peminjaman, pemeliharaan, hingga penghapusan — dilengkapi jejak audit lengkap dan akses berbasis peran (RBAC).

Proyek ini dikembangkan sebagai studi kasus pendidikan untuk mata kuliah **IF13PP13 – Proyek Pengembangan Perangkat Lunak** di **UISI**.

### 🎯 Tujuan Produk
- Menyediakan **satu sumber data aset** yang konsisten dan dapat ditelusuri
- Mencegah **konflik peminjaman** aset secara otomatis
- Memastikan setiap perubahan status aset **tercatat di audit log** tanpa celah

---

## ✨ Fitur Utama (MVP)

| Kode | Fitur | Deskripsi |
|------|-------|-----------|
| M1 | **Master Aset & Lokasi** | Registrasi aset dengan nomor unik, kategori, lokasi, unit, dan penanggung jawab |
| M2 | **Peminjaman & Pengembalian** | Alur ajukan → setujui → serah terima → kembali, dengan pencegahan bentrok otomatis |
| M3 | **Riwayat Mutasi & Status** | Setiap perubahan lokasi/status aset tercatat lengkap dengan pelaku dan waktu |
| M4 | **RBAC & Audit Log** | Hak akses per peran, audit log immutable untuk seluruh aksi penting |
| M5 | **Laporan, Impor-Ekspor & Rekonsiliasi** | Laporan status aset, impor/ekspor CSV, laporan selisih rekonsiliasi fisik |

---

## 👥 Peran Pengguna

| Peran | Kemampuan Utama |
|-------|----------------|
| **Petugas Inventaris** | Registrasi aset, ubah lokasi/status, mutasi, rekonsiliasi, impor-ekspor |
| **Unit Peminjam** | Cari aset tersedia, ajukan peminjaman, lihat status, kembalikan aset |
| **Penanggung Jawab Fasilitas** | Setujui/tolak peminjaman, lihat laporan unit, tandai kondisi aset |
| **Admin Sistem** | Kelola akun dummy & peran, lihat audit log (read-only) |

> Semua peran disimulasikan menggunakan akun dummy. Bukan representasi struktur organisasi UISI.

---

## 🚀 Cara Menjalankan

### Prasyarat
- [Docker](https://www.docker.com/) & Docker Compose
- Git

### Langkah

```bash
# 1. Clone repository
git clone https://github.com/<org>/campusasset.git
cd campusasset

# 2. Salin dan sesuaikan konfigurasi environment
cp .env.example .env

# 3. Jalankan aplikasi (satu perintah)
docker compose up --build

# 4. Jalankan seed data sintetis
docker compose exec app npm run seed   # atau perintah seed sesuai stack

# 5. Akses aplikasi
# → http://localhost:3000
```

> Seluruh data yang digunakan adalah **data sintetis** yang dibangkitkan otomatis. Tidak ada data nyata kampus yang digunakan.

---

## 🧪 Menjalankan Pengujian

```bash
# Unit test & integrasi
docker compose exec app npm run test

# Laporan cakupan uji
docker compose exec app npm run test:coverage

# Uji lint
docker compose exec app npm run lint
```

---

## 🗂️ Struktur Folder

```
campusasset/
├── backend/          # Logika server, API, domain
│   ├── src/
│   │   ├── domain/   # State machine, aturan bisnis, pencegahan bentrok
│   │   ├── api/      # Route & controller per fitur
│   │   ├── middleware/  # Auth, RBAC, error handler
│   │   └── db/       # Migrasi & seed
│   └── tests/        # Unit test, integrasi, uji konkurensi
├── frontend/         # Antarmuka per peran
│   └── src/
│       ├── pages/
│       └── components/
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 🔐 Catatan Keamanan & Etika

- ✅ Tidak ada secret/kunci tersimpan di repository — konfigurasi lewat variabel lingkungan
- ✅ Seluruh data pengguna dan aset adalah **data fiktif** (sintetis)
- ✅ Data kuesioner dikumpulkan secara sukarela, anonim, tanpa data identitas sensitif
- ✅ Penggunaan AI diperbolehkan untuk brainstorm & prototyping — seluruh output diverifikasi tim
- ❌ Tidak mengklaim integrasi resmi ke ERP, SSO, atau sistem produksi UISI

---

## 📋 Status Pengembangan

Lihat progress lengkap di **[GitHub Projects Board](https://github.com/users/Andree75/projects/2)**.

Alur kolom: `Backlog` → `Ready` → `In Progress` → `In Review` → `Done`

---

## 👨‍💻 Tim

| Peran Kerja | Tanggung Jawab |
|-------------|---------------|
| Product Owner / Analis | Telaah literatur, kuesioner, acceptance criteria, uji pengguna |
| Backend & Domain | State machine, pencegahan bentrok, audit log, RBAC |
| Frontend & UX | Antarmuka per peran, alur tugas, usability |
| QA & DevOps | Uji otomatis, CI, kontainer, deployment |

> Kelompok: **IF13PP13** · Mata Kuliah: Proyek Pengembangan Perangkat Lunak · **UISI**
