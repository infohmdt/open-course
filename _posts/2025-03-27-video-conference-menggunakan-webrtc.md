---
title: Video Conference Menggunakan WebRTC
description: Mengatur konferensi video menggunakan WebRTC (Web Real-Time Communication) di server Ubuntu.
categories: [Cybersecurity, Linux]
tags: [linux]
author: rical
---

WebRTC adalah teknologi yang memungkinkan komunikasi audio, video, dan data secara langsung antara browser tanpa memerlukan plugin tambahan. Dalam panduan ini, ngrok digunakan untuk membuat tunneling ke server lokal agar dapat diakses dari internet.

## Langkah-langkah Pengaturan
### 1. Mendapatkan Authtoken Ngrok
Langkah pertama melibatkan kunjungan ke [halaman resmi ngrok](https://ngrok.com/) untuk mendapatkan Authtoken. 

> Authtoken ini diperlukan untuk mengautentikasi sesi tunneling yang akan dibuat. 
{: .prompt-info}

Ngrok menyediakan layanan tunneling yang memungkinkan akses ke server lokal dari internet, yang sangat berguna untuk pengembangan aplikasi yang memerlukan akses jarak jauh.

![Ngrok - Your Authtoken](assets/img/posts/2025-03-27-video-conference-menggunakan-webrtc/ngrok-token.png)

### 2. Mengakses Server Ubuntu
Akses server Ubuntu yang berjalan di VirtualBox menggunakan [SSH](https://ricaldocs.github.io/posts/openssh/). Buka terminal dan masukkan perintah berikut:

```bash
ssh username@hostname
```

[SSH (Secure Shell)](https://ricaldocs.github.io/posts/openssh/) adalah protokol jaringan yang memungkinkan akses aman ke komputer lain. 

> Pastikan untuk mengganti `username` dan `hostname` dengan informasi yang sesuai.
{: .prompt-tip}

![SSH Login](assets/img/posts/2025-03-27-video-conference-menggunakan-webrtc/ssh-login.png)

### 3. Memperbarui Repositori Ubuntu
Perbarui repositori paket Ubuntu untuk memastikan versi terbaru dari semua paket yang tersedia. Jalankan perintah berikut:

```bash
sudo apt update -y
```

> Memperbarui repositori secara berkala penting untuk menjaga sistem tetap aman dan mendapatkan fitur terbaru dari perangkat lunak yang digunakan.
{: .prompt-tip}

### 4. Memasang Snapd
Instal `snapd`, sistem manajemen paket untuk distribusi Linux, dengan perintah berikut:

```bash
sudo apt install -y snapd 
```

Setelah itu, instal `snap core`:

```bash
sudo snap install core
```

Kemudian, instal ngrok melalui snap:

```bash
sudo snap install ngrok
```

> Snapd memungkinkan instalasi dan pengelolaan aplikasi dalam format snap, yang menyediakan isolasi dan kemudahan dalam pembaruan.
{: .prompt-info}

### 5. Mengkloning Repositori WebRTC
Klon repositori WebRTC dari GitHub dan masuk ke direktori yang baru saja dikloning dengan perintah berikut:

```bash
git clone https://github.com/ricalnet/WebRTC.git && cd WebRTC
```

> Mengkloning repositori memungkinkan akses ke kode sumber aplikasi WebRTC yang akan digunakan untuk konferensi video.
{: .prompt-info}

### 6. Memasang NPM
Instal `npm` (Node Package Manager) yang diperlukan untuk mengelola paket JavaScript dengan perintah:

```bash
sudo apt install -y npm
```

> Jika muncul popup pada terminal, tekan `tab` dan pilih `Ok` pada keyboard lalu tekan enter.
{: .prompt-tip}

> NPM adalah alat penting dalam ekosistem JavaScript yang memungkinkan pengelolaan dependensi dan paket yang diperlukan untuk pengembangan aplikasi.
{: .prompt-info}

### 7. Menambahkan Authtoken Ngrok
Salin [token ngrok yang didapatkan sebelumnya](https://ricaldocs.github.io/posts/video-conference-menggunakan-webrtc/#1-mendapatkan-authtoken-ngrok) dan masukkan perintah berikut untuk menambahkannya ke konfigurasi ngrok:

```bash
ngrok config add-authtoken $YOUR_AUTHTOKEN
```

Output yang diharapkan:

```
Authtoken saved to configuration file: /home/ubuntu/snap/ngrok/260/.config/ngrok/ngrok.yml
```

> Menambahkan Authtoken ke konfigurasi ngrok memungkinkan penggunaan fitur premium dan meningkatkan keamanan sesi tunneling.
{: .prompt-info}

### 8. Menginstal Nodemon
Instal `nodemon`, alat yang membantu dalam pengembangan aplikasi Node.js dengan secara otomatis me-restart aplikasi ketika file berubah:

```bash
npm install nodemon --save-dev
```

> Nodemon sangat berguna dalam pengembangan, karena mengurangi waktu yang diperlukan untuk memulai ulang aplikasi secara manual setiap kali ada perubahan pada kode.
{: .prompt-tip}

### 9. Menjalankan Aplikasi
Jalankan aplikasi WebRTC menggunakan perintah berikut:

```bash
npm run dev
```

> Perintah ini akan memulai server pengembangan yang memungkinkan pengujian aplikasi secara lokal.
{: .prompt-info}

### 10. Membuat Tunneling dengan Ngrok
Buka terminal Ubuntu baru dan jalankan perintah `ngrok` untuk membuat tunneling ke server lokal, sehingga dapat diakses dari internet:

```bash
ngrok http http://localhost:4300
```

> Perintah ini akan memberikan URL publik yang dapat digunakan untuk mengakses aplikasi WebRTC dari browser lain, memungkinkan pengujian dan demonstrasi aplikasi secara langsung.
![Ngrok - Forwarding](assets/img/posts/2025-03-27-video-conference-menggunakan-webrtc/ngrok-forwarding.png)
![Ngrok - Visit Site](assets/img/posts/2025-03-27-video-conference-menggunakan-webrtc/ngrok-page.png)
{: .prompt-info}

## Pranala Menarik
- [Home Server](https://ricaldocs.github.io/posts/home-server/)
- [Membangun VoIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/)
- [OpenSSH](https://ricaldocs.github.io/posts/openssh/)

## Referensi
- [ricalWiki: WebRTC](https://ricalnet.github.io/ricalwiki.html)
- [Telecommunication Network Laboratory](https://telnetlab.github.io)
