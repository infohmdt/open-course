---
title: CalDownloader
description: CalDownloader adalah skrip Python sederhana yang memungkinkan pengguna untuk mengunduh video dari YouTube dan konten dari Instagram, termasuk postingan dan reels
categories: [Cybersecurity, rical_net, Linux]
tags: [rical_net, python, android, linux]
author: rical
---

CalDownloader menggunakan *library* `yt-dlp` untuk mengunduh video dari YouTube dan `instaloader`untuk mengambil dan menyimpan konten dari profil Instagram publik.

## Fitur 🌟

| Aplikasi | Fitur | Status |
| --- | --- | --- |
| YT Downloader | Unduh Video (mendukung unduhan playlist) | ✅ |
| YT Downloader | Unduh MP3 (mendukung unduhan playlist) | ✅ |
|  |  |  |
| InstaBackup | Unduh dengan username (lengkap) | ✅ |
| InstaBackup | Unduh melalui URL postingan | ✅ |
| InstaBackup | Unduh melalui URL reel | ✅ |

## Kompatibel 👍
- Linux
- Android (via Termux). Silakan merujuk ke panduan [ini](https://ricaldocs.github.io/posts/python-virtual-environment/#android-venv).
- Windows
- macOS? Jangan ragu untuk mengujinya sendiri.

## Prasyarat 📋

- Python 3.x
- `yt-dlp` dan `instaloader` library
- [FFmpeg](https://ffmpeg.org/download.html) (`sudo apt install -y ffmpeg` untuk linux. `pkg install -y ffmpeg` untuk Termux)

```bash
pip install yt-dlp instaloader
```

## Penggunaan 🚀

1. Clone repository atau unduh skripnya.

    ```bash
    git clone https://github.com/risnandapascal/CalDownloader.git
    ```

2. Jalankan skrip menggunakan Python:
   ```bash
   python main.py
   ```

## Menu Pilihan 💻
Ikuti instruksi pada layar untuk memilih metode unduhan:
   - **YT Downloader**: Pilih untuk mengunduh video atau audio dari YouTube.
   - **InstaBackup**: Pilih untuk mengunduh konten dari Instagram.
   - **Exit**: Keluar dari aplikasi.

### Contoh
```
===============================
          CalDownloader          
===============================
Choose an option:
1. YouTube Downloader
2. InstaBackup
3. Exit
Enter your choice (1/2/3): 1
===============================
          YT Downloader          
===============================
Choose a download method (supporting playlist downloads):
1. Download Video
2. Download MP3
3. Exit
Enter your choice (1/2/3): 1
🔗 Enter the link: https://www.youtube.com/watch?v=example
```

```
==============================
          InstaBackup          
==============================
Choose a download method:
1. Download by username (full)
2. Download by post URL
3. Download by reel URL
4. Exit
Enter your choice (1/2/3/4): 1
Enter the Instagram username (public account): rical_net
```

## Lisensi 📄

Proyek ini bersifat *open-source* dan tersedia di bawah [MIT License](https://github.com/risnandapascal/CalDownloader/blob/main/LICENSE.md). 

## Source Code
[rical_net](https://github.com/risnandapascal/CalDownloader)
