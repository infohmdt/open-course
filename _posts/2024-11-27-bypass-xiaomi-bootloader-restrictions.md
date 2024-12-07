---
title: Bypass Xiaomi Bootloader Restrictions
description: Unlock bootloader HyperOS tanpa menggunakan Mi Community.
categories: [Android, Tools & Fix]
tags: [android]
author: rical
---

> File dan alat yang digunakan BUKAN dibuat oleh saya, melainkan oleh beberapa pengembang cerdas. Saya tidak bertanggung jawab atas apa pun yang terjadi pada perangkat Anda (*brick*, kartu SD mati, dll.).
{: .prompt-danger}

> Panduan ini menggunakan sistem operasi Windows dan hanya perangkat Xiaomi GLOBAL yang didukung!
{: .prompt-info}

# Panduan Unlock Bootloader Xiaomi

Sebelum mulai, silakan periksa [persyaratan pembukaan kunci](https://github.com/MlgmXyysd/Xiaomi-HyperOS-BootLoader-Bypass/#-Unlocking-requirements).

## Konfigurasi pengaturan Xiaomi

- Buka pengaturan di ponsel Xiaomi.
- Pergi ke: **My phone** > **OS version** dan ketuk berulang kali sampai muncul pesan "you are a developer".
- Pergi ke **Additional settings** > **Developer Options**.
- Di **Developer Options**, aktifkan: **OEM Unlocking**, **USB Debugging**, dan **USB Debugging (Security Settings)**.
- Sekarang masuk dengan akun Xiaomi yang valid.

## Instalasi php

- [Unduh file PHP ini](/assets/posts/php.zip).
- Ekstrak ke `C:\php`.

## Instalasi aplikasi pengaturan

- Unduh [Settings.apk](https://drive.proton.me/urls/X4189HG8H0#XiHXwaww6p3k) ini.
- Instal di perangkat melalui pengelola file.

## Eksekusi

- Hubungkan ponsel ke PC melalui kabel.
- Di `C:\php`, jalankan `Bypass.cmd`.
- Di ponsel, centang `always allow USB debugging from this computer` dan ketuk OK.
- Tunggu dan ikuti petunjuk skrip.
- Setelah `successful binding`, unduh [Official Unlock Tool](https://en.miui.com/unlock/index.html) dan lakukan proses *unlock bootloader* seperti biasa.

Saya pribadi berhasil membuka kunci bootloader tanpa menggunakan `Mi Community` dan tanpa waktu tunggu `168 hours`.
