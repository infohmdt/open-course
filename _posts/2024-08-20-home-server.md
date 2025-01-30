---
title: Home Server
description: Bangun home server untuk mengoptimalkan keamanan dan privasi data pribadi. Dengan cara ini, kita dapat mengendalikan sepenuhnya penyimpanan dan akses informasi tanpa harus bergantung pada layanan cloud pihak ketiga yang dapat menjadi titik lemah.
categories: [Cybersecurity, Linux, rical_net, Privacy]
tags: [linux, rical_net, privacy, open source]
author: rical
---

## Persiapan
---

Membangun infrastruktur data pribadi yang aman dan terkontrol merupakan tindakan proaktif yang krusial. Ini adalah langkah berani untuk melindungi informasi pribadi dari pengawasan luar dan memastikan bahwa hak digital tetap terjaga dengan baik.

### Memperbarui Sistem
---

Perbarui sistem dengan menjalankan perintah berikut:
```bash
sudo apt update && sudo apt upgrade -y
```

### Instalasi LAMPP
---

Instal dan konfigurasi LAMPP (Linux, Apache, MySQL, PHP), karena Nextcloud memerlukan server web dan basis data. Jalankan perintah berikut:
```bash
sudo apt install apache2 mariadb-server php php-curl php-cli php-mysql php-gd php-common php-xml php-json php-intl php-pear php-imagick php-dev php-common php-mbstring php-zip php-soap php-bz2 php-bcmath php-gmp php-apcu libmagickcore-dev php-redis php-memcached
```

Unduh Nextcloud menggunakan `wget`:
```bash
wget https://download.nextcloud.com/server/releases/latest.zip
```

Ekstrak file yang telah diunduh dan pindahkan ke direktori `/var/www/html`{: .filepath}:
```bash
sudo unzip latest.zip -d /var/www/html
```

Akses direktori Nextcloud:
```bash
cd /var/www/html
```

Ubah kepemilikan direktori Nextcloud:
```bash
sudo chown -R www-data:www-data nextcloud
```

## Konfigurasi MySQL
---

Atur kata sandi root untuk basis data dengan menjalankan:
```bash
sudo mysql_secure_installation
```

Login ke MySQL menggunakan perintah berikut:
```bash
mysql -u root -p
```

### Membuat Basis Data dan Pengguna
---

Gantilah `username` dan `password` sesuai kebutuhan:
```sql
CREATE DATABASE home_server;
```
```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

Izinkan pengguna untuk mengakses basis data `home_server`:
```sql
GRANT ALL PRIVILEGES ON home_server.* TO 'username'@'localhost';
```
```sql
FLUSH PRIVILEGES;
```
```sql
exit
```

## Konfigurasi Virtual Host
---

Buat konfigurasi virtual host dengan perintah berikut:
```bash
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

Isi berkas dengan konfigurasi berikut:
```
<VirtualHost *:80>
    ServerName localhost

    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/nextcloud

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    <Directory /var/www/html/nextcloud/>
        Options +FollowSymlinks
        AllowOverride All

        <IfModule mod_dav.c>
            Dav off
        </IfModule>

        SetEnv HOME /var/www/html/nextcloud
        SetEnv HTTP_HOME /var/www/html/nextcloud
    </Directory>
</VirtualHost>
```

Simpan berkas dan aktifkan konfigurasi:
```bash
sudo a2ensite nextcloud.conf && sudo systemctl restart apache2
```

## Konfigurasi Nextcloud
---

Buka browser dan akses [http://localhost/nextcloud](http://localhost/nextcloud).

> Petunjuk instalasi Nextcloud akan muncul. Selama proses instalasi, atur basis data MariaDB, akun admin, dan direktori penyimpanan data. Ikuti instruksi yang diberikan.
{: .prompt-tip}

Selesai. Sekarang, unduh aplikasi Nextcloud ke perangkat dan mulai mengunggah serta mengelola file secara mandiri.

> Selain untuk home server, [Nextcloud](https://nextcloud.com) juga menjadi fondasi utama untuk pengembangan [NextCrow](https://risnandapascal.github.io/nextcrow.html) berkat sifatnya yang *open source*, memberikan kontrol penuh atas data, serta fitur keamanan tingkat tinggi.
{: .prompt-info}

Selanjutnya, jalankan perintah berikut untuk membuat crontab baru yang akan digunakan untuk menjalankan skrip crontab Nextcloud:
```bash
sudo crontab -u www-data -e
```

Parameter `-u www-data` digunakan karena server web Apache2 berjalan di atas pengguna tersebut.

Tambahkan konfigurasi berikut ke file crontab:
```bash
*/5  *  *  *  * php -f /var/www/html/nextcloud/cron.php
```
Simpan dan keluar dari file setelah selesai.

## Mengganti Alamat IP
---

Ubah `trusted domain` di berkas `config.php`{: .filepath}:
```bash
sudo nano /var/www/html/nextcloud/config/config.php
```
Isi dari berkas tersebut akan menampilkan seperti ini:
```php
$CONFIG = array (
    'instanceid' => 'ocfwe8edkz4v',
    'passwordsalt' => 'kf0eOXdbetRdsrobORxjkHefQoa/SJ',
    'secret' => 'nl6PNO/1Yhd1ZSefWBiPBLRhucTZLXuq7fqTn1FhCixufSqm',
    'trusted_domains' =>
    array (
        0 => 'masukkan alamat ip atau domain di sini',
    ),
);
```

Ubah `Virtual Host` dengan memasukkan perintah:
```bash
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

Pada bagian:
```
ServerName *masukkan ip address atau domain di sini*
```

Simpan berkas dan aktifkan konfigurasi:
```bash
sudo a2ensite nextcloud.conf && sudo systemctl restart apache2
```

## Pranala Menarik
---

- [Perjalanan ke Dunia Open Source](https://ricaldocs.github.io/posts/perjalanan-ke-dunia-open-source-copy/)
- [Membangun VoIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/)

## Referensi
---

- [ricalWiki: Home Server](https://risnandapascal.github.io/ricalwiki.html)