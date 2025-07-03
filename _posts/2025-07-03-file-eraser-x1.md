---
title: File Eraser (x1)
description: Penghapusan file dengan 7-pass overwrite, metadata destruction, dan secure deletion.
categories: [Cybersecurity, Linux, ricalNet]
tags: [cybersecurity, privacy, ricalNet]
author: rical
---

[File Eraser (x1)](https://github.com/ricalnet/file-eraser-x1) 🔥 adalah senjata pamungkas untuk penghancuran file permanen! Alat ini mengimplementasikan teknik penghancuran data dengan 7-pass overwrite, penghancuran metadata, dan teknik anti-forensik untuk memastikan file Anda **benar-benar hancur tak tersisa** 💥.

## 🌟 Fitur Utama

- ✅ **7-pass overwrite** - Kombinasi standar DoD + pola khusus
- 🔥 **Metadata destruction** - Penghapusan timestamp, multiple rename, permission lock
- 🛡️ **Secure deletion** - Teknik OS-specific untuk penghapusan akhir
- 🤖 **SSD detection** - Peringatan otomatis untuk media penyimpanan modern
- 📊 **Verifikasi real-time** - Pemeriksaan integritas setiap pass
- 🚀 **Optimasi performa** - Chunking 1MB untuk file besar
- 🌐 **Cross-platform** - Dukungan penuh Linux, Windows, macOS
- 📜 **Logging** - Audit trail lengkap dengan timestamp

## ⚙️ Prasyarat

- 🐍 Python 3.8 atau lebih baru
- 💻 Sistem operasi:
  - 🐧 Linux (direkomendasikan)
  - 🪟 Windows 10/11
  - 🍎 macOS 10.15+
- 🔑 Izin administrator untuk file sistem

## 📥 Instalasi

1. Clone repository atau download script:
    ```bash
    git clone https://github.com/ricalnet/file-eraser-x1 && cd file-eraser-x1
    ```

2. Berikan izin eksekusi:
    ```bash
    chmod +x main_x1.py
    ```

3. (Opsional) Instal ke PATH sistem:
    ```bash
    sudo cp main_x1.py /usr/local/bin/fileeraserx1
    ```

## 🚀 Penggunaan

### Penghancuran File Tunggal
```bash
./main_x1.py rahasia.txt
```

### Penghancuran Direktori (rekursif)
```bash
./main_x1.py folder_sensitif/ --yes
```

### Opsi Lanjutan
```bash
./main_x1.py [PATH] [OPTIONS]

🔥 Opsi Destruksi:
  --gutmann        Mode ekstrim 35-pass (sangat lambat) 🐢
  --dod            Standar DoD 3-pass (lebih cepat) ⚡
  --passes N       Custom pass count (default: 7) 🔢

⚙️ Opsi Tambahan:
  --no-verify      Nonaktifkan verifikasi overwrite 🚫
  --no-metadata    Nonaktifkan metadata destruction 📛
  -v, --verbose    Mode verbose (detail proses) 📣
  -y, --yes        Eksekusi tanpa konfirmasi 🤖
  -h, --help       Tampilkan bantuan ❓
```

## 🔥 Algoritma Penghancuran

[File Eraser (x1)](https://github.com/ricalnet/file-eraser-x1) menggunakan teknik berlapis untuk memastikan kehancuran total:

### 1. ⚡ 7-Pass Overwrite

   | Pass | Pola               | Keterangan                     |
   |------|--------------------|--------------------------------|
   | 1   | `3a7f1c8b`         | Random 4-byte block            |
   | 2   | `00000000`         | Null bytes                     |
   | 3   | `ff34d9a1`         | Random integer                 |
   | 4   | `55555555`         | Binary 01010101                |
   | 5   | `AAAAAAAA`         | Binary 10101010                |
   | 6   | `924924...`        | Random pattern 1               |
   | 7   | `492492...`        | Random pattern 2               |

### 2. 💥 Metadata Destruction
   - 7x random rename 🔀
   - Penghapusan semua timestamp ⏳
   - Set permission ke 000 (no access) 🔐
   - Hapus extended attributes 🧹

### 3. 🧨 Secure Deletion
   - Linux/macOS: Gunakan `shred` atau `srm` 🔧
   - Windows: System call langsung 💻
   - Force filesystem sync 🌀

## 📋 Contoh Output

```
2025-07-03 14:30:02 [INFO] 🔥 Memulai shredding shredding (x1): rahasia.txt
2025-07-03 14:30:02 [DEBUG] ⚙️ PASS 1: Pola 3a7f1c8b
2025-07-03 14:30:05 [INFO] ✅ Verifikasi PASS 1 berhasil
2025-07-03 14:30:07 [DEBUG] ⚙️ PASS 2: Pola 00000000
2025-07-03 14:30:09 [INFO] ✅ Verifikasi PASS 2 berhasil
2025-07-03 14:31:15 [INFO] 🔀 Metadata dihancurkan: 7x rename
2025-07-03 14:31:16 [INFO] 🧨 Secure deletion dengan system call
2025-07-03 14:31:17 [INFO] 💥 File dihancurkan secara permanen: /tmp/a3d8e7c5b2f4019e
```

## ❓ FAQ

### ❔ Apakah file benar-benar tidak bisa dipulihkan?
> ✅ Ya, pada HDD tradisional. Untuk SSD, gunakan full-disk encryption sejak awal. Alat ini akan memberikan peringatan otomatis jika mendeteksi SSD.

### ⏱️ Berapa lama proses penghancuran?
> ⏱️ Waktu tergantung ukuran file dan spesifikasi hardware. Perkiraan kasar:
> - File 1GB: 2-5 menit (7-pass)
> - File 10GB: 20-50 menit
> - Gunakan `--dod` untuk versi lebih cepat (3-pass)

### 🛡️ Bagaimana dengan file system journaling?
> 🔒 Untuk proteksi maksimal, hapus seluruh partisi:
> ```bash
> ./main_x1.py /dev/sdX --passes 35
> ```
> Atau gunakan full-disk encryption sejak awal.

### 💾 Dapatkah digunakan untuk USB drive?
> ✅ Ya, tapi pastikan:
> 1. Tidak dalam mode read-only
> 2. Bukan media write-protected
> 3. Format filesystem mendukung overwrite

## ⚠️ Batasan Teknis

1. **Media Modern**:
   - 💾 SSD/NVMe mungkin masih menyimpan data di block fisik
   - Solusi: Aktifkan TRIM + full-disk encryption

2. **File System**:
   - 📁 Copy-on-Write (ZFS/Btrfs) mungkin menyimpan snapshot
   - Solusi: Disable CoW untuk direktori sensitif

3. **File Besar**:
   - 🐢 Performa menurun untuk file >100GB
   - Solusi: Gunakan `--no-verify --no-metadata`

## 🚀 Rekomendasi Penggunaan

| Skenario                      | Rekomendasi Opsi               |
|-------------------------------|--------------------------------|
| File kecil (<1GB)             | `./main_x1.py file`    |
| File besar (>10GB)            | `--dod --no-verify`            |
| Data sangat sensitif          | `--gutmann -v`                 |
| Media SSD                     | Full-disk encryption + alat ini|
| Direktori rekursif            | `-y --passes 7`                |

---

> Alat ini dirancang untuk tujuan keamanan yang sah. Pengguna bertanggung jawab penuh atas penggunaan alat ini. Penghancuran data mungkin melanggar hukum tertentu. Konsultasikan dengan ahli hukum sebelum penggunaan. 🚨
{: .prompt-warning}

> Setelah file dihancurkan dengan alat ini, **TIDAK ADA** cara untuk memulihkannya! Gunakan dengan tanggung jawab penuh! 🔥
{: .prompt-danger}