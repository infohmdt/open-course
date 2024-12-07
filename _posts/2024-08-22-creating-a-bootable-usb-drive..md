---
title: Creating a bootable USB drive
description: Langkah-langkah untuk membuat USB drive yang dapat digunakan untuk instalasi atau booting.
categories: [Linux]
tags: [linux, open source]
author: rical
---

## Create
Untuk membuat *usb bootable* menggunakan Linux, ikuti langkah-langkah berikut:

### Persyaratan
- USB flash drive.
- File ISO yang sudah diunduh.

### Langkah-langkah

1. Sambungkan *usb drive* ke komputer.
2. Buka terminal dan jalankan perintah berikut untuk mengidentifikasi nama USB:
   ```bash
   lsblk
   ```
   Temukan nama perangkat USB (misalnya, `/dev/sdx`). 
   
   > Pastikan tidak salah memilih perangkat, karena semua data di perangkat tersebut akan terhapus.
   {: .prompt-warning}

3. Jika *usb drive* terpasang, `unmount` terlebih dahulu dengan perintah:
   ```bash
   sudo umount /dev/sdx
   ```
   Gantilah `sdx` dengan nama partisi USB (misalnya, `/dev/sdb1`).

4. Gunakan perintah `dd` untuk menulis file ISO ke *usb drive*. Pastikan untuk mengganti `/path/to/linux.iso` dengan path ke file ISO yang telah diunduh dan `/dev/sdx` dengan nama perangkat USB (tanpa angka di belakangnya):
   ```bash
   sudo dd if=/path/to/kali-linux.iso of=/dev/sdX bs=4M status=progress
   ```
   Contoh:
   ```bash
   sudo dd if=/home/user/Downloads/kali-linux.iso of=/dev/sdb bs=4M status=progress
   ```

5. Proses ini mungkin memakan waktu beberapa menit. Tunggu hingga selesai.

6. Setelah proses selesai, jalankan perintah berikut untuk memastikan semua data ditulis ke USB:
   ```bash
   sync
   ```
   Kemudian, kita dapat mengeluarkan *usb drive* dengan aman:
   ```bash
   sudo eject /dev/sdx
   ```

> Pastikan untuk melakukan backup data penting di *usb drive* sebelum melakukan langkah-langkah ini, karena semua data di *usb drive* akan terhapus.
{: .prompt-info}

Setelah selesai, kita dapat menggunakan *usb drive* tersebut untuk *booting* ke sistem operasi yang akan digunakan.

## Delete

### Langkah-langkah

1. Pastikan *usb flash drive* terhubung ke komputer.

2. Buka terminal dan jalankan perintah berikut untuk mengidentifikasi nama perangkat USB:
   ```bash
   lsblk
   ```
   Temukan nama perangkat USB (misalnya, `/dev/sdx`). Pastikan untuk mencatat nama perangkat yang benar.

3. Jika *usb drive* terpasang, `unmount` terlebih dahulu dengan perintah:
   ```bash
   sudo umount /dev/sdx
   ```
   Gantilah `sdx` dengan nama partisi USB (misalnya, `/dev/sdb1`).

4. Gunakan perintah `mkfs` untuk memformat *usb drive*. Berikut adalah contoh untuk memformat *usb drive* ke sistem file FAT32:
   ```bash
   sudo mkfs.vfat -I /dev/sdx
   ```
   Gantilah `sdx` dengan nama perangkat USB (tanpa angka di belakangnya).

   Jika ingin memformat ke sistem file ext4, gunakan:
   ```bash
   sudo mkfs.ext4 /dev/sdx
   ```

5. Setelah proses format selesai, keluarkan *usb drive* dengan aman:
   ```bash
   sudo eject /dev/sdx
   ```

> Pastikan untuk melakukan *backup* data penting di *usb drive* sebelum melakukan langkah-langkah ini, karena semua data di *usb drive*e akan terhapus.
{: .prompt-info}

## Referensi 
- [ricalWiki](https://risnandapascal.github.io/ricalwiki.html)