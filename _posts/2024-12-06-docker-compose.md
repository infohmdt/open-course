---
title: Docker Compose
description: Melakukan eksperimen Docker Compose di AWS.
categories: [Cloud Computing, AWS]
tags: [cloud, aws, linux, docker]
author: rical
---

Docker Compose adalah sebuah file dalam [Docker](https://en.wikipedia.org/wiki/Docker_(software)) yang memungkinkan kita untuk menjalankan dan mengonfigurasi beberapa kontainer sekaligus. Intinya, dengan menggunakan Docker Compose, kita dapat mengatur konfigurasi berbagai kontainer serta menentukan urutan kontainer dan image mana yang harus dijalankan terlebih dahulu.

## Instance & Docker configuration
- Lihat konfigurasi Instance [di sini](https://ricaldocs.github.io/posts/docker-on-aws/#setup-instance).
- Lihat konfigurasi Docker [di sini](https://ricaldocs.github.io/posts/docker-on-aws/#konfigurasi-docker).

## Membuat Folder dan File Docker Compose
Silakan ketik perintah 
```bash
mkdir nama_folder && cd nama_folder
``` 

```bash
nano docker-compose.yml
```

> Penamaan file ini bersifat sensitif; jika salah penamaan, file tidak akan terbaca. Gunakan huruf kecil dan tanda `-` dalam penamaannya, contohnya seperti `docker-compose.yml`.
{: .prompt-tip}

Selanjutnya, masukkan kode berikut:
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

Klik `ctrl+x` dan ketik `y` untuk keluar dari `nano`.

> - **Version**: Ini merujuk pada versi Docker Compose yang digunakan, yaitu versi 3.7.
- **Service**: Ini adalah deklarasi untuk menjalankan container yang diperlukan. Dalam kode ini, terdapat dua container, yaitu container untuk web dan PHP. Container PHP tidak membuka port apa pun karena fungsinya hanya sebagai pendukung agar web dapat menjalankan PHP.
- **Container Web**: Di dalam container web, terdapat kode “${NGINX_VERSION}” yang merupakan variabel lingkungan (environment variable). Penggunaan variabel lingkungan ini penting untuk meningkatkan keamanan dalam sebuah container. Hal ini karena Docker Compose terkadang dapat memiliki kerentanan yang berpotensi mengakibatkan kebocoran data pribadi pengguna. Oleh karena itu, menggunakan variabel lingkungan adalah langkah yang lebih aman.
{: .prompt-info}

Masukkan perintah berikut untuk membuat file `.env`:
```bash
nano .env
```

Kemudian masukkan kode di bawah ini:

```yml
NGINX_VERSION=latest
PORT_NGINX=80
PHP_VERSION=7.2-fpm
```

Klik `ctrl+x` dan ketik `y` untuk keluar dari `nano`.

File `.env` adalah file tersembunyi secara bawaan. Untuk memeriksa file `.env`, gunakan perintah:

```bash
ls -a
```

Perintah ini akan menampilkan semua file, termasuk yang tersembunyi, di direktori saat ini.

Untuk membuat file `site.conf`, gunakan perintah berikut:

```
git clone https://github.com/sendiahmadhidayat8/site-conf.git
```

Perintah ini akan mengunduh repositori yang berisi file `site.conf` ke dalam direktori `site-conf`.

## Menjalankan Docker Compose
Untuk menjalankan Docker Compose, ketik perintah berikut:

```bash
docker compose up -d
```

Setelah itu, masuk ke direktori `html` dengan perintah:

```bash
cd html/
```

Kemudian, buat file `index.php`, `about.php`, `contact.php`, dan `style.css`.

```bash
touch index.php about.php contact.php style.css
```

Masukkan kode berikut ke dalam file `index.php`:

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

Masukkan kode berikut ke dalam file `about.php`:
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

Masukkan kode berikut ke dalam file `contact.php`:
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

Masukkan kode berikut ke dalam file `style.css`:
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

Setelah semua selesai, cek *ip public* AWS di browser.

## Referensi 
[Telecommunication Network Laboratory](https://www.instagram.com/telnetlab)