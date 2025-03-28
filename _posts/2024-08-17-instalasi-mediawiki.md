---
title: MediaWiki
description: Menggunakan MediaWiki untuk tujuan kolaborasi dan dokumentasi proyek.
categories: [Linux]
tags: [linux, wiki, open source]
author: rical
---

Dokumentasi ini menjelaskan cara menggunakan MediaWiki untuk tujuan kolaborasi dan dokumentasi proyek. MediaWiki adalah perangkat lunak wiki *open source* yang banyak digunakan, terutama oleh proyek-proyek Wikimedia.

## Instalasi
### Persyaratan Sistem
Disarankan untuk menggunakan sistem operasi Ubuntu atau Debian untuk meminimalisir potensi masalah saat menginstal MediaWiki.

### Memperbarui Sistem
Sebelum memulai instalasi, perbarui sistem dengan menjalankan perintah berikut:

```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y && sudo apt clean -y
```

### Instalasi LAMPP
Instal paket-paket yang diperlukan untuk menjalankan MediaWiki dengan perintah berikut:

```bash
sudo apt-get install apache2 mariadb-server php php-mysql libapache2-mod-php php-xml php-mbstring
```

> Sebagai alternatif, dapat menggunakan perintah yang sama. Paket tambahan yang mungkin berguna, tergantung pada kebutuhan instalasi, adalah:
```bash
sudo apt-get install php-apcu php-intl imagemagick inkscape php-gd php-cli php-curl php-bcmath git
```
{: .prompt-info}

## Mengunduh MediaWiki
Pindah ke direktori `/var/www/html`{: .filepath}:

```bash
cd /var/www/html
```

Unduh MediaWiki menggunakan `wget` atau kunjungi situs resmi [MediaWiki](https://www.mediawiki.org/wiki/Download):

```bash
wget https://releases.wikimedia.org/mediawiki/1.41/mediawiki-1.41.1.tar.gz
```

Ekstrak file yang diunduh dengan perintah:

```bash
tar -xvzf /tmp/mediawiki-*.tar.gz && cd /tmp
```

Buat folder baru dengan nama `wiki` di dalam direktori `/var/www/html`{: .filepath}:

```bash
mkdir /var/www/html/wiki
```

Pindahkan semua file yang telah diekstrak ke dalam folder `wiki`:

```bash
mv mediawiki-*/* /var/www/html/wiki
```

## Konfigurasi MySQL
### Membuat Pengguna Baru
Masuk ke MySQL sebagai pengguna root:

```bash
sudo mysql -u root -p
```

Buat pengguna baru dengan perintah berikut:

```sql
CREATE USER 'mysql_username'@'localhost' IDENTIFIED BY 'masukkanpassword';
```

Keluar dari MySQL:

```sql
quit;
```

### Membuat Database Baru
Masuk kembali ke MySQL:

```bash
sudo mysql -u root -p
```

Buat basis data baru untuk MediaWiki:

```sql
CREATE DATABASE my_wiki;
```

Pilih basis data yang baru dibuat:

```sql
USE my_wiki;
```

### Memberikan Akses Pengguna ke Database
Izinkan pengguna yang telah dibuat untuk mengakses database:

```sql
GRANT ALL PRIVILEGES ON my_wiki.* TO 'mysql_username'@'localhost';
FLUSH PRIVILEGES;
exit;
```

## Konfigurasi MediaWiki
Arahkan browser ke [http://localhost/wiki](http://localhost/wiki) dan ikuti prosedur yang diberikan.

Jika muncul keluhan bahwa ekstensi PHP seperti `mbstring` dan `xml` hilang, aktifkan secara manual dengan perintah berikut:

```bash
sudo phpenmod mbstring && sudo phpenmod xml && sudo systemctl restart apache2.service
```

### Pengaturan Konfigurasi
> Di halaman web, ikuti langkah-langkah berikut:
1. Klik "Please set up the wiki first."
2. Pilih bahasa.
3. Klik "Continue."
4. Sesuaikan konfigurasi untuk terhubung ke database dengan informasi berikut:
   - Database host: `localhost`
   - Database name: `my_wiki`
   - Database table prefix: `wiki_`
   - Database username: `mysql_username`
   - Database password: `masukkanpassword`
{: .prompt-tip}

Setelah konfigurasi selesai, unduh file `LocalSettings.php` dan pindahkan ke direktori `wiki`:

```bash
cd ~/Downloads && mv LocalSettings.php /var/www/html/wiki/
```

MediaWiki kini telah terkonfigurasi dan dapat diakses di [http://localhost/wiki](http://localhost/wiki).

## Referensi
- [ricalWiki: Instalasi MediaWiki](https://ricalnet.github.io/ricalwiki.html)
- [Manual: Running MediaWiki on Debian or Ubuntu](https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Debian_or_Ubuntu)