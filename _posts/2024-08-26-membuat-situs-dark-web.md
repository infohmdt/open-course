---
title: Membuat Situs Dark Web 
description: Situs Dark Web menggunakan ekstensi domain `.onion`. Pertanyaan yang sering muncul adalah, apakah kita dapat membuat situs web sendiri di Dark Web menggunakan sistem Kali Linux? Jawabannya adalah ya, dengan mudah, tanpa perlu melakukan port forwarding atau mengeluarkan biaya untuk membeli nama domain.
categories: [Cybersecurity, Privacy, Linux]
tags: [cybersecurity, privacy, linux, open source]
author: rical
---

## Instalasi dan Konfigurasi TOR
Untuk memulai, lakukan pembaruan dan instalasi TOR dengan perintah berikut:

```bash
sudo apt update && sudo apt install -y tor
```

Selanjutnya, buka file konfigurasi TOR:

```bash
sudo gedit /etc/tor/torrc
```

Temukan dua baris berikut dan hapus tanda `#` dari kedua baris tersebut, kemudian simpan file. Setelah disunting, tampilan file akan seperti berikut:

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:80
```

Setelah itu, mulai ulang layanan TOR dengan perintah:

```bash
sudo systemctl restart tor
```

## Membuat dan Menghosting Situs Dark Web
Buat file `index.html` di Desktop dengan perintah:

```bash
cd ~/Desktop && touch index.html
```

> `index.html` di sini merujuk pada konten file website yang akan dihosting.
{: .prompt-info}

File ini terletak di Desktop, sehingga kita perlu memulai server lokal berbasis PHP di Desktop dengan perintah berikut:

```bash
php -S 127.0.0.1:8080
```

Server pengembangan PHP kini akan berjalan. Untuk memeriksa situs web localhost yang dihosting, navigasikan ke [127.0.0.1:8080](http://127.0.0.1:8080) melalui browser.

> Kita telah memulai server localhost menggunakan PHP pada port 8080. Kita juga dapat menggunakan port 80 (jika belum digunakan), namun ini memerlukan izin root (`sudo php -S 127.0.0.1:80`). Selain itu, kita dapat menggunakan server Python, Apache, atau server web lokal lainnya untuk menghosting situs web localhost.
{: .prompt-info}

### Terhubung ke Layanan TOR
Biarkan jendela terminal ini tetap terbuka (karena server localhost sedang berjalan). Buka terminal lain dan ketik perintah berikut:

```bash
sudo -u debian-tor tor
```

Tunggu beberapa saat hingga konfigurasi selesai 100%. Proses ini akan membangun sirkuit TOR, yang mungkin memerlukan beberapa menit tergantung pada kinerja sistem dan kecepatan internet.

Setelah semua siap, situs *dark web* kita sudah dihosting. Namun, di mana tautan `.onion`-nya?

Tautan `.onion` dihasilkan secara acak. Untuk melihat alamat `.onion` dari situs Dark Web yang dihosting, buka jendela terminal lain (terminal ketiga, karena kita tidak dapat menutup atau menggunakan terminal yang ada, jika tidak koneksi akan hilang) dan ketik perintah berikut untuk melihat alamatnya:

```bash
sudo cat /var/lib/tor/hidden_service/hostname
```

Sekarang kita dapat mengakses situs `.onion` ini menggunakan browser TOR dari mana saja dan perangkat apa saja.

> Ini adalah situs demo untuk tujuan pendidikan. Namun, kita dapat menghosting berbagai jenis situs web di `.onion` selama tidak melanggar hukum. Jangan menyalahgunakan ini untuk menghosting situs web ilegal. Tindakan tersebut akan dianggap sebagai kejahatan dan penulis tidak bertanggung jawab atasnya.
{: .prompt-danger}

## Referensi
- [ricalWiki: Membuat Situs Dark Web](https://ricalnet.github.io/ricalwiki.html)