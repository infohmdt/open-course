---
title: Kesalahan dalam Instalasi Cisco Packet Tracer di Kali Linux
description: Solusi untuk masalah instalasi Cisco Packet Tracer di Kali Linux.
categories: [Cisco Packet Tracer]
tags: [linux, cisco packet tracer]
author: rical
---

## Masalah Instalasi Cisco Packet Tracer di Kali Linux
---

Pengguna mengalami kesulitan dalam menginstal Cisco Packet Tracer setelah melakukan instalasi Kali Linux pada mesin baru. Sebelumnya, aplikasi ini berfungsi dengan baik pada versi Debian yang lebih lama. Namun, saat ini, pengguna menghadapi kesalahan yang konsisten selama proses instalasi.

### Ketergantungan yang Dihadapi
---

Dua ketergantungan yang tidak dapat diinstal adalah sebagai berikut:

1. **libxcb-xinerama0-dev**
2. **libgl1-mesa-glx**

### Langkah-Langkah Penyelesaian
---

#### 1. Instalasi `libxcb-xinerama0-dev`
---

Untuk menginstal ketergantungan pertama, pengguna dapat membuka terminal dan menjalankan perintah berikut:

```bash
sudo apt install libxcb-xinerama0-dev
```

Proses ini berhasil dan ketergantungan pertama terinstal.

#### 2. Instalasi `libgl1-mesa-glx`
---

Untuk ketergantungan kedua, yaitu `libgl1-mesa-glx`, pengguna perlu mengunduh file secara manual. File dapat diunduh dari [situs paket Debian](https://packages.debian.org/bookworm/amd64/libgl1-mesa-glx/download).

- Pilih arsitektur yang sesuai, dan klik pada tautan tersebut.
- Di halaman berikutnya, pilih salah satu tautan mirror untuk memulai unduhan (file dalam format `.deb`).

#### 3. Instalasi File yang Diunduh
---

Setelah unduhan selesai, buka terminal dan ketik perintah berikut, mengganti `dependency_name.deb` dengan nama file yang diunduh:

```bash
sudo dpkg -i dependency_name.deb
```

Sebagai alternatif, pengguna dapat menggunakan penginstal paket untuk menginstalnya.

#### 4. Instalasi Cisco Packet Tracer
---

Setelah semua ketergantungan terinstal, pengguna dapat mencoba menginstal Cisco Packet Tracer dengan mengetik perintah berikut, mengganti `packet_tracer.deb` dengan nama file instalasi Packet Tracer:

```bash
sudo dpkg -i packet_tracer.deb
```

## Pranala Menarik
---

- [Konfigurasi VPN Menggunakan Router di Cisco Packet Tracer](https://ricaldocs.github.io/posts/konfigurasi-vpn-menggunakan-router-di-cisco-packet-tracer/)
- [Perencanaan Jaringan DWDM Menggunakan Cisco Packet Tracer](https://ricaldocs.github.io/posts/qos-cisco-packet-tracer/)
- [Konfigurasi QoS di Cisco Packet Tracer](https://ricaldocs.github.io/posts/qos-cisco-packet-tracer/)

Dengan mengikuti langkah-langkah di atas, pengguna seharusnya dapat menginstal Cisco Packet Tracer di Kali Linux tanpa masalah. Diharapkan solusi ini dapat membantu pengguna lain yang mengalami masalah serupa.

