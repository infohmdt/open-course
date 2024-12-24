---
title: Prabu Incognito
description: Prabu Incognito (raja yang menyamar) adalah kumpulan alat yang berfokus pada privasi, dirancang untuk meningkatkan keamanan dan anonimitas.
categories: [Cybersecurity, rical_net, Linux, Privacy, ]
tags: [cybersecurity, rical_net, linux, privacy, open source]
author: rical
---

Prabu Incognito dikembangkan menggunakan kode Bash dan bertujuan untuk menghindari pelacakan serta melakukan pemantauan keamanan. Proyek ini dikembangkan oleh [rical_net](https://risnandapascal.github.io) dan ditujukan untuk pengguna yang ingin melindungi data pribadi mereka dari pelacakan dan pemantauan. Alat ini menyediakan dua kategori utama fitur: *privacy tools* dan *security tools*.

```bash
***************************************************************
*                       ____    _______                       *
*                      /    \  |       \                      *
*                     |  ()  | | PRIVACY!                     *
*                      \____/  |_______/                      *
*                                                             *
*              PRABU INCOGNITO - Author by rical              *
*                    Powered by Bismillah                     *
*                                                             *
*      https://github.com/risnandapascal/prabu-incognito/     *
*                                                             *
***************************************************************

[!] 'All human beings have three lives: public, private, and secret' [!]

[1] Privacy Tools
[2] Security Tools
[3] Exit
[?] Enter your choice:
```

## Fitur

### Privacy Tools

| Fitur                  | Deskripsi 	    |
| :--------------------- | :--------------- |
| Set Default DNS        | Mengganti server DNS bawaan pada sistem dengan server DNS yang berbasis privasi (dihasilkan oleh whoami-project). |
| Change Hostname        | Mengganti nama host dengan nama acak untuk bersembunyi. |
| Change Timezone 	 | Mengubah zona waktu untuk menghindari kebocoran lokasi dari jam sistem. |
| Mac Changer		 | Mengubah alamat MAC secara acak pada ANTARMUKA jaringan yang ditentukan dan me-reset alamat MAC ke default. |
| Shadow Service 	 | Menginstal, memeriksa status, memulai, menghentikan, atau me-restart layanan TOR. Fitur ini berdasarkan [Nipe](https://github.com/htrgouvea/nipe). |
| Riseup VPN 		 | Menjalankan Riseup VPN. |
| Manage Metadata	 | Menghapus dan membaca metadata file. |                                                                  

### Security Tools

| Fitur                  	| Deskripsi       |
| :--------------------------- 	| :--------------- |
| Firewall			| Mengkonfigurasi *firewall* sistem untuk memblokir lalu lintas masuk, kecuali untuk SSH, dan memberikan informasi tentang aturan yang diterapkan. |
| Monitor Network Traffic	| Memantau untuk mendeteksi aktivitas yang mencurigakan atau memahami lalu lintas jaringan yang sedang berlangsung. |
| Check File Integrity		| Memeriksa integritas file sistem untuk mendeteksi perubahan yang tidak sah. |
| Generate Strong Password	| Membuat kata sandi yang kuat dan acak secara otomatis. |
| Run Rootkit Hunter	 	| Memeriksa sistem untuk mendeteksi kemungkinan adanya rootkit dan *malware*. |
| System Monitor	 	| Melihat aplikasi-aplikasi yang sedang aktif. |

## Prasyarat

- Sistem operasi berbasis Debian (Kali Linux direkomendasikan)
- Bash atau Zsh

## Penggunaan

1. **Clone repository dan masuk ke direktori**
   ```bash
   git clone https://github.com/risnandapascal/prabu-incognito/ && cd prabu-incognito
   ```
2. **Ubah perizinan:**
   ```bash
   chmod +x install.sh
   ```
   ```bash
   chmod +x prabu.sh
   ```
3. **Instal dependensi:**
   ```bash
   sudo ./install.sh
   ```
4. **Jalankan:**
   ```bash
   sudo ./prabu.sh
   ```

   > Jangan gunakan `sudo` untuk Riseup VPN.
   {: .prompt-warning}

### Instruksi untuk layanan Shadow
   ```bash
   help
   ```
   ```bash
   install
   ```
   ```bash
   status
   ```
   ```bash
   start
   ```
   ```bash
   stop
   ```
   ```bash
   status
   ```

## Lisensi

Proyek ini bersifat *open-source* dan tersedia di bawah [MIT License](https://github.com/risnandapascal/prabu-incognito/blob/main/LICENSE.md).

## Kode Sumber

Sumber kode proyek ini dapat diakses melalui [rical_net](https://github.com/risnandapascal/prabu-incognito).