---
title: Docker on AWS
description: Melakukan percobaan NGINX di dalam Docker dengan memanfaatkan AWS Sandbox Environment.
categories: [Cloud Computing, AWS]
tags: [cloud, aws, linux, docker]
author: rical
---

## Pendahuluan
---

[Docker](https://en.wikipedia.org/wiki/Docker_(software)) adalah platform yang memungkinkan pengembang untuk membuat, mengirim, dan menjalankan aplikasi dalam bentuk kontainer. Kontainer ini merupakan unit standar perangkat lunak yang mengemas kode beserta semua dependensinya, sehingga aplikasi dapat berjalan dengan konsisten di berbagai lingkungan, baik itu di komputer pengembang, server, maupun cloud.

Docker mempermudah pengelolaan aplikasi dengan memberikan isolasi yang lebih baik, efisiensi sumber daya, serta kemudahan dalam pengujian dan penyebaran. Dengan menggunakan Docker, tim pengembang dapat bekerja lebih cepat dan efisien, sekaligus mengurangi masalah yang sering muncul akibat perbedaan lingkungan.

## Setup Instance
---

Di halaman dashboard AWS, cari **EC2** dan buat instance dengan memilih opsi **Instances** di panel kiri, kemudian klik **Launch Instance**.

Pada bagian **Application and OS Images**, pilih **Ubuntu**.

![AMI](/assets/img/posts/cloud/2024-11-15-docker-on-aws/ami.png){: width="972" height="589" }

Selanjutnya, pada bagian **Instance Type**, silakan pilih **t2.small**.

![Instances type](/assets/img/posts/cloud/2024-11-15-docker-on-aws/instances-type.png){: width="972" height="589" }

Di bagian **Create key pair**, klik **Create key pair**.

> Jika menggunakan Linux atau [OpenSSH](https://ricaldocs.github.io/posts/openssh/#menggunakan-kunci-ssh), pilih tipe `.pem`. Jika menggunakan PuTTY, pilih tipe `.ppk`. Setelah itu, klik **Create key pair**.
{: .prompt-tip}

![Create key pair](/assets/img/posts/cloud/2024-11-15-docker-on-aws/create-key-pair.png){: width="972" height="589" }

Pada bagian **Network settings**, silakan pilih **Create security group** dan centang opsi SSH, HTTP dan HTTPS untuk memberikan izin pada port 22, 80 dan 443. Setelah itu, klik **Launch instance**.

![Network settings](/assets/img/posts/cloud/2024-11-15-docker-on-aws/network-settings.png){: width="972" height="589" }

> Kita dapat mengakses instance jarak jauh menggunakan key pair yang telah diunduh tadi, atau kita juga bisa langsung terhubung melalui opsi **Connect** dari instance tersebut.
{: .prompt-info}

## Konfigurasi Docker
---

### Setup Docker's repository
---

Dalam OpenSSH atau PuTTY, silakan masukkan perintah berikut:

```bash
sudo apt-get update && sudo apt-get install ca-certificates curl && sudo install -m 0755 -d /etc/apt/keyrings && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc && sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt-get update
```
### Instalasi Docker
---

Masukkan perintah berikut ke terminal untuk memasang versi terakhir dari Docker:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
docker --version
```

Setelah itu, silakan instal image dengan menggunakan perintah berikut:
```bash
docker pull nginx
```

Periksa images dengan mengetikkan perintah berikut:
```bash
docker images
```

Setelah image selesai dibuat, selanjutnya buatlah kontainer menggunakan image tersebut dengan mengetik:
```bash
docker container create --name nginx -p 80:80 nginx
```

Cek kontainer:
```bash
docker ps -a
```

## Menggunakan NGINX
---

Status di sini belum aktif. Untuk menjalankannya, silakan ketik:
```bash
docker container start nginx
```

Silakan ubah data indeks dengan cara keluar dari direktori file. Pertama, buatlah folder bernama `docker`{: .filepath}.
```bash
mkdir docker
```

Kemudian, buat file `index.html`{: .filepath}
```bash
cd docker && nano index.html
```

Masukkan kode html berikut:
```html
<html>
    <body>
        <h1>Hello Friends</h1>
    </body>
</html>
```

Klik `ctrl+x` dan ketik `y` untuk keluar dari `nano`. Selanjutnya, cek ip public AWS di browser.

Ketikkan perintah berikut untuk menyalin file HTML ke direktori `/usr/share/nginx/html`{: .filepath} pada kontainer Nginx.
```bash
docker cp index.html nginx:/usr/share/nginx/html
```

## Skenario 2: Membuat kontainer dan mengimpor data web melalui volume.
---

Hapus container yang telah dibuat sebelumnya. Namun, sebelum itu, pastikan untuk menghentikan container yang masih berjalan dengan perintah: 
```bash
docker container stop nginx 
```

Setelah itu, kita dapat menghapusnya dengan perintah:
```bash
docker container rm nginx
```

Buat volume baru dengan menjalankan perintah berikut:
```bash
docker container create --name nginxx -p 80:80 -v /home/ubuntu/docker/web/:/usr/share/nginx/html nginx
```

> Perintah di atas akan membuat kontainer baru dengan nama **nginxx**, memetakan port 80, dan menghubungkan direktori lokal ke direktori di dalam kontainer.
{: .prompt-info}

Jalankan kontainer dengan mengetik `docker container start nginxx` dan periksa apakah kontainer tersebut sudah berjalan dengan mengetik `docker ps -a`.

Selanjutnya, masuk ke direktori `web`{: .filepath} dan buat file `index.html`{: .filepath} dengan mengetik:
```bash
cd web && nano index.html
```

Kemudian, masukkan kode berikut:
```html
<html>
    <body>
        <h1>Hello Volume</h1>
    </body>
</html>
```

Klik `ctrl+x` dan ketik `y` untuk keluar dari `nano`. Selanjutnya, cek ip public AWS di browser.

## Skenario 3: Dockerfile
---

```bash
nano Dockerfile
```

Masukkan teks:
```
FROM nginx 

COPY /web/ /usr/share/nginx/html
```

Klik `ctrl+x` dan ketik `y` untuk keluar dari `nano`.

Salin file Dockerfile dengan menggunakan perintah:
```bash
cp Dockerfile ../
```

Selanjutnya, keluar dari folder web dengan mengetikkan perintah: 
```bash
cd ../
``` 

Lihat image yang telah dibuat dengan mengetikkan perintah:
```bash
docker images
```

Buat image dengan mengetikkan perintah:
```bash
docker build --tag nginxww .
```

Setelah itu, coba periksa kembali dengan mengetik:
```bash
docker images
```

Hapus kontainer yang ada di **Skenario 2** dengan mengetikkan perintah:
```bash
docker container stop nginxx && docker container rm nginxx && docker ps -a
```

Buat container menggunakan image yang telah dibuat dengan perintah berikut:
```bash
docker container create --name nginx -p 80:80 nginxww
```

Pastikan untuk mengganti **nginxww** dengan nama image yang sesuai jika diperlukan.

Terakhir, gunakan perintah berikut:
```bash
docker container start nginx && cat Dockerfile
```

## Pranala Menarik
---

- [Docker Compose](https://ricaldocs.github.io/posts/docker-compose/)

## Referensi 
---

[Telecommunication Network Laboratory: Cloud Computing](https://www.instagram.com/telnetlab)
