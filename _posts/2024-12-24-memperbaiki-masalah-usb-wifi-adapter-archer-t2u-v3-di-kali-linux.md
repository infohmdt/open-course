---
title: Memperbaiki Masalah USB WiFi Adapter Archer T2U V3 di Kali Linux
description: Menjelaskan cara memperbaiki adaptor WiFi USB Archer T2U V3 di Kali Linux dengan menghapus driver lama, menginstal driver baru, dan melakukan reboot sistem.
categories: [Cybersecurity, Linux]
tags: [cybersecurity, linux]
author: rical
---

Gambaran umum
---

Dokumentasi ini membahas langkah-langkah untuk mengatasi masalah yang mungkin terjadi pada adaptor WiFi USB Archer T2U V3 di sistem operasi Kali Linux. Pengguna sering mengalami kendala setelah melakukan pembaruan sistem, yang dapat menyebabkan adaptor WiFi tidak berfungsi dengan baik. Berikut adalah panduan untuk menyelesaikan masalah ini dengan menginstal driver yang sesuai.

## Langkah 1: Menghapus Driver Lama yang Tidak Berfungsi
---

Langkah pertama dalam proses pemecahan masalah adalah mengidentifikasi dan menghapus driver lama yang mungkin tidak berfungsi dengan baik.

1. **Periksa Status Driver yang Terpasang:**

   Untuk memeriksa status driver yang terpasang, gunakan perintah berikut:

   ```bash
   sudo dkms status
   ```

2. **Hapus Driver Lama:**

   Setelah mengidentifikasi driver yang tidak berfungsi, hapus driver tersebut dengan mengganti `old-driver-name` dengan nama driver yang sesuai.

   ```bash
   sudo dkms remove -m old-driver-name --all
   ```

## Langkah 2: Menginstal Driver yang Lebih Baru
---

Setelah menghapus driver lama, langkah selanjutnya adalah menginstal driver yang lebih baru yang mendukung adaptor WiFi USB.

1. **Kloning Repositori Driver:**

   Gunakan perintah berikut untuk mengkloning repositori driver yang diperlukan:

   ```bash
   git clone https://github.com/morrownr/8821au-20210708.git
   ```

2. **Arahkan ke Direktori Repositori:**

   Masuk ke direktori repositori yang telah dikloning:

   ```bash
   cd 8821au-20210708
   ```

3. **Instal Driver:**

   Jalankan skrip instalasi driver dengan perintah berikut:

   ```bash
   sudo ./install-driver.sh
   ```

   > Selama proses instalasi, mungkin akan diminta untuk memodifikasi konfigurasi. Namun, disarankan untuk tidak mengubah pengaturan *default*. Setelah menyelesaikan instalasi, sistem akan meminta untuk melakukan *reboot*.
   {: .prompt-info}

## Langkah 3: Melakukan Reboot
---

Setelah instalasi driver selesai, *reboot* sistem untuk menerapkan perubahan yang telah dilakukan.

Dengan mengikuti langkah-langkah di atas, diharapkan masalah yang dialami dengan adaptor WiFi USB Archer T2U V3 di Kali Linux dapat teratasi. Jika masalah masih berlanjut, pertimbangkan untuk mencari dukungan lebih lanjut dari [komunitas pengguna Kali Linux](https://forums.kali.org/).

## Pranala Menarik
---

- [Securing Kali Linux System](https://ricaldocs.github.io/posts/securing-kali-linux-system/)
- [Enabling and Disabling Monitor Mode in Kali Linux](https://ricaldocs.github.io/posts/enabling-and-disabling-monitor-mode-kali-linux/)
