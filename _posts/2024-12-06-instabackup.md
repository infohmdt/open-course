---
title: InstaBackup
description: InstaBackup adalah skrip Python sederhana yang memungkinkan pengguna untuk mengunduh postingan dan Reels Instagram baik berdasarkan nama pengguna maupun URL postingan/Reel.
categories: [Cybersecurity, rical_net]
tags: [rical_net, python]
author: rical
---

## Fitur

- Unduh semua postingan dari profil Instagram publik.
- Unduh postingan atau Reel tertentu menggunakan URL.
- Antarmuka baris perintah yang ramah pengguna.

## Prasyarat

- Python 3.x
- Pustaka `instaloader`

```bash
pip install instaloader
```

## Penggunaan

1. Clone repository atau unduh skripnya.

    ```bash
    git clone https://github.com/risnandapascal/InstaBackup
    ```

2. Jalankan skrip menggunakan Python:

   ```bash
   python instabackup.py
   ```

## Menu Pilihan
Ikuti petunjuk di layar untuk memilih metode unduhan:
   - **Download by username (full)**: Masukkan *username* Instagram publik untuk mengunduh semua postingan.
   - **Download by post URL**: Masukkan URL postingan Instagram yang valid untuk mengunduh postingan tertentu.
   - **Download by reel URL**: Masukkan URL Reel Instagram yang valid untuk mengunduh Reel tertentu.
   - **Exit**: Keluar dari InstaBackup.

### Contoh
```bash
===================================
            InstaBackup            
===================================
Choose a download method:
1. Download by username (full)
2. Download by post URL
3. Download by reel URL
4. Exit
Enter your choice (1/2/3/4): 1
Enter the Instagram username (public account): rical_net
```

## Lisensi

Proyek ini bersifat *open-source* dan tersedia di bawah [MIT License](https://github.com/risnandapascal/InstaBackup/blob/main/LICENSE.md). 

## Source Code
[rical_net](https://github.com/risnandapascal/InstaBackup)
