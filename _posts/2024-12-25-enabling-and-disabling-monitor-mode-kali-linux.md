---
title: Enabling and Disabling Monitor Mode in Kali Linux
description: Menjelaskan cara mengaktifkan dan mematikan monitor mode pada antarmuka WLAN di Kali Linux.
categories: [Cybersecurity, Linux, Privacy]
tags: [cybersecurity, linux, privacy]
author: rical
---

## Mengaktifkan Monitor Mode

### Langkah-langkah
1. Akses terminal di Kali Linux.
   
2. Periksa nama *interface* WLAN dengan perintah:
   ```bash
   iwconfig
   ```
   Temukan *interface* yang sesuai (misalnya wlan1).

3. Sebelum mengaktifkan monitor mode, matikan *interface* dengan perintah:
   ```bash
   sudo ip link set wlan1 down
   ```

4. Setelah *interface* dimatikan, aktifkan monitor mode dengan perintah:
   ```bash
   sudo iw dev wlan1 set type monitor
   ```

5. Nyalakan kembali *interface* dengan perintah:
   ```bash
   sudo ip link set wlan1 up
   ```

6. Verifikasi bahwa *interface* sekarang dalam mode monitor dengan perintah:
   ```bash
   iwconfig
   ```
   Pastikan wlan1 terdaftar sebagai `Mode:Monitor`.

> Setelah langkah-langkah ini, pengguna dapat menggunakan wlan1 dalam mode monitor untuk menangkap paket dan melakukan analisis jaringan. Pastikan untuk memiliki izin yang sesuai, karena menangkap paket tanpa izin dapat melanggar hukum.
{: .prompt-warning}

## Mematikan Monitor Mode

### Langkah-langkah
1. Pastikan terminal di Kali Linux terbuka.

2. Matikan *interface* WLAN yang sedang dalam mode monitor dengan perintah:
   ```bash
   sudo ip link set wlan1 down
   ```

3. Setelah *interface* dimatikan, setel kembali *interface* ke `Mode:Managed` dengan perintah:
   ```bash
   sudo iw dev wlan1 set type managed
   ```

4. Nyalakan kembali *interface* dengan perintah:
   ```bash
   sudo ip link set wlan1 up
   ```

5. Verifikasi bahwa *interface* sekarang dalam `Mode:Managed` dengan perintah:
   ```bash
   iwconfig
   ```
   Pastikan wlan1 terdaftar sebagai `Mode:Managed`.

## Referensi
- [ricalWiki](https://risnandapascal.github.io/ricalwiki.html)