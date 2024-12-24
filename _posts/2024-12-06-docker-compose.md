---
title: Docker Compose
description: Melakukan eksperimen Docker Compose di AWS.
categories: [Cloud Computing, AWS]
tags: [cloud, aws, linux, docker]
author: rical
---

Docker Compose adalah alat yang digunakan dalam [Docker](https://en.wikipedia.org/wiki/Docker_(software)) untuk menjalankan dan mengonfigurasi beberapa kontainer secara bersamaan. Dengan Docker Compose, pengguna dapat mengatur konfigurasi berbagai kontainer serta menentukan urutan kontainer dan *image* yang harus dijalankan terlebih dahulu.

## Konfigurasi Instance dan Docker
- Untuk informasi lebih lanjut mengenai konfigurasi Instance, silakan lihat [di sini](https://ricaldocs.github.io/posts/docker-on-aws/#setup-instance).
- Untuk informasi lebih lanjut mengenai konfigurasi Docker, silakan lihat [di sini](https://ricaldocs.github.io/posts/docker-on-aws/#konfigurasi-docker).

## Membuat Folder dan File Docker Compose
Untuk membuat folder dan berpindah ke dalamnya, ketik perintah berikut:
```bash
mkdir nama_folder && cd nama_folder
```

Kemudian, buat file `docker-compose.yml` dengan perintah:
```bash
nano docker-compose.yml
```

> Penamaan file ini bersifat sensitif; jika salah penamaan, file tidak akan terbaca. Gunakan huruf kecil dan tanda `-` dalam penamaannya, contohnya seperti `docker-compose.yml`.
{: .prompt-tip}

Selanjutnya, masukkan kode berikut ke dalam file `docker-compose.yml`{: .filepath}:
```yml
version: '3.7'
services:
  web:
    image: nginx:${NGINX_VERSION}
    ports:
      - "${PORT_NGINX}:80"
    volumes:
      - ./html:/html
      - ./site-conf/site.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - php

  php:
    image: php:${PHP_VERSION}
    volumes:
      - ./html:/html
```

Setelah selesai, tekan `ctrl+x` dan ketik `y` untuk menyimpan dan keluar dari `nano`.

> - **Version:** Menunjukkan versi Docker Compose yang digunakan, yaitu versi 3.7.
- **Service:** Deklarasi untuk menjalankan kontainer yang diperlukan. Dalam kode ini, terdapat dua kontainer, yaitu kontainer untuk web dan PHP. Kontainer PHP tidak membuka port karena berfungsi sebagai pendukung untuk menjalankan PHP di web.
- **Container Web:** Dalam kontainer web, terdapat kode **${NGINX_VERSION}** yang merupakan variabel lingkungan. Penggunaan variabel lingkungan ini penting untuk meningkatkan keamanan dalam kontainer, mengingat Docker Compose dapat memiliki kerentanan yang berpotensi mengakibatkan kebocoran data pribadi pengguna.
{: .prompt-info}

Untuk membuat file `.env`, gunakan perintah berikut:
```bash
nano .env
```

Kemudian masukkan kode berikut:
```yml
NGINX_VERSION=latest
PORT_NGINX=80
PHP_VERSION=7.2-fpm
```

Setelah selesai, tekan `ctrl+x` dan ketik `y` untuk menyimpan dan keluar dari `nano`.

File `.env`{: .filepath} adalah file tersembunyi secara bawaan. Untuk memeriksa file `.env`{: .filepath}, gunakan perintah:
```bash
ls -a
```
Perintah ini akan menampilkan semua file, termasuk yang tersembunyi, di direktori saat ini.

Untuk membuat file `site.conf`, gunakan perintah berikut:
```bash
git clone https://github.com/sendiahmadhidayat8/site-conf.git
```
Perintah ini akan mengunduh repositori yang berisi file `site.conf`{: .filepath} ke dalam direktori `site-conf`{: .filepath}.

## Menjalankan Docker Compose
Untuk menjalankan Docker Compose, ketik perintah berikut:
```bash
docker compose up -d
```

Setelah itu, masuk ke direktori `html`{: .filepath} dengan perintah:
```bash
cd html/
```

Kemudian, buat file `index.php`, `about.php`, `contact.php`, dan `style.css` dengan perintah:
```bash
touch index.php about.php contact.php style.css
```

### Kode untuk File
Masukkan kode berikut ke dalam file `index.php`{: .filepath}:
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Welcome to My Website</h1>
        <nav>
            <a href="index.php">Home</a>
            <a href="about.php">About</a>
            <a href="contact.php">Contact</a>
        </nav>
    </header>
    <main>
        <h2>Home Page</h2>
        <p>This is the homepage of the website. Enjoy exploring!</p>
    </main>
    <footer>
        <p>&copy; 2024 My Website</p>
    </footer>
</body>
</html>
```

Masukkan kode berikut ke dalam file `about.php`{: .filepath}:
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Us</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>About Us</h1>
    <nav>
      <a href="index.php">Home</a>
      <a href="about.php">About</a>
      <a href="contact.php">Contact</a>
    </nav>
  </header>
  <main>
    <h2>About Us</h2>
    <p>This page contains information about our website and team.</p>
  </main>
  <footer>
    <p>&copy; 2024 My Website</p>
  </footer>
</body>
</html>
```

Masukkan kode berikut ke dalam file `contact.php`{: .filepath}:
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Us</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Contact Us</h1>
    <nav>
      <a href="index.php">Home</a>
      <a href="about.php">About</a>
      <a href="contact.php">Contact</a>
    </nav>
  </header>
  <main>
    <h2>Contact Information</h2>
    <form action="#" method="POST">
      <label for="name">Name:</label>
      <input type="text" id="name" name="name" required>
      <br><br>
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" required>
      <br><br>
      <label for="message">Message:</label>
      <textarea id="message" name="message" rows="5" required></textarea>
      <br><br>
      <button type="submit">Submit</button>
    </form>
  </main>
  <footer>
    <p>&copy; 2024 My Website</p>
  </footer>
</body>
</html>
```

Masukkan kode berikut ke dalam file `style.css`{: .filepath}:
```css
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.6;
  color: #333;
  background-color: #f4f4f4;
}

header {
  background: #333;
  color: #fff;
  padding: 1rem 0;
  text-align: center;
}

header nav a {
  color: #fff;
  text-decoration: none;
  margin: 0 10px;
}

header nav a:hover {
  text-decoration: underline;
}

main {
  padding: 20px;
  background: #fff;
  margin: 20px auto;
  max-width: 800px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

footer {
  text-align: center;
  padding: 10px 0;
  background: #333;
  color: #fff;
  position: relative;
  bottom: 0;
  width: 100%;
}
```

## Verifikasi
Setelah semua file selesai dibuat dan disimpan, periksa IP publik AWS di browser untuk memastikan bahwa aplikasi web berjalan dengan baik.

## Referensi
- [Telecommunication Network Laboratory](https://www.instagram.com/telnetlab)