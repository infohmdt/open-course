---
title: DynamicArchive
description: Arsipkan folder menjadi file dengan enkripsi untuk meningkatkan keamanan backup menggunakan DynamicArchive.
categories: [Cybersecurity,  rical_net, Linux, Privacy]
tags: [cybersecurity, rical_net, privacy, linux, open source]
author: rical
---

DynamicArchive berfungsi untuk mengarsipkan folder menjadi file terkompresi dengan fitur enkripsi, serta mengekstrak file terkompresi yang telah dienkripsi. Alat ini dirancang untuk memberikan kemudahan dalam pengelolaan arsip, sambil menambahkan lapisan keamanan melalui [*symmetric encryption*](https://ricaldocs.github.io/posts/gnu-privacy-guard/#asymmetric--symmetric).

## Dukungan Format
- [x] [Tar](https://id.wikipedia.org/wiki/Tar_(komputasi))
- [x] [ZIP](https://id.wikipedia.org/wiki/ZIP_(format_berkas))
- [x] [7-Zip](https://id.wikipedia.org/wiki/7-Zip)
- [x] gz

## Fitur

1. Mengarsipkan folder menjadi file yang terenskripsi dengan [GnuPG](https://ricaldocs.github.io/posts/gnu-privacy-guard/).
2. Mengekstrak file yang terenskripsi.

## Prasyarat

- Bash or Zsh

## Penggunaan

Untuk menjalankan alat ini, cukup jalankan perintah berikut di terminal:

```bash
git clone https://github.com/risnandapascal/DynamicArchive.git && cd DynamicArchive
```

```bash
sudo ./requirements.sh
```

```bash
./dynamic_archive.sh
```

## Menu Pilihan
Ikuti petunjuk di layar untuk memilih metode penggunaan.
```
==================================================================
      DynamicArchive          
      https://github.com/risnandapascal/DynamicArchive
==================================================================

========== TAR =========
1) Archive 📦🔒
2) Extract 📥🔒
========================

========== ZIP =========
3) Archive 📦🔒
4) Extract 📥🔒
========================

========== 7z ==========
5) Archive 📦🔒
6) Extract 📥🔒
========================

========== GZ ==========
7) Archive 📦🔒
8) Extract 📥🔒
========================

==================================================================
Enter your choice (1, 2, 3, 4, 5, 6, 7, or 8): 1
Enter the path of the folder you want to archive: /home/user/folder
```

Pilih opsi untuk mengarsipkan folder menjadi file (*encrypted*):
- Masukkan jalur folder yang ingin diarsipkan (misal: `/home/user/backup`).
- Masukkan nama file *output* (misal: `backup.tar`).
- Skrip akan membuat file dan mengenkripsinya menggunakan [GnuPG](https://ricaldocs.github.io/posts/gnu-privacy-guard/) yang akan menghasilkan *output* `backup.tar.gpg`.

Pilih opsi untuk mengekstrak file yang terenskripsi:
- Masukkan nama file yang terenskripsi (misal: `backup.tar.gpg`).
- Skrip akan mendekripsi dan mengekstrak file tersebut.

> DynamicArchive akan melakukan validasi pada nama file *output* untuk memastikan hanya karakter alfanumerik, titik, garis bawah, dan tanda hubung yang diperbolehkan.
{: .prompt-info}

> Alat ini juga dilengkapi dengan penanganan kesalahan yang memberikan umpan balik kepada pengguna jika terjadi kesalahan, seperti folder tidak ditemukan atau gagal dalam proses enkripsi/dekripsi.
{: .prompt-info}

## Lisensi
Proyek ini bersifat *open-source* dan tersedia di bawah [MIT License](https://github.com/risnandapascal/DynamicArchive/blob/main/LICENSE.md).

## Source Code
[rical_net](https://github.com/risnandapascal/DynamicArchive)







