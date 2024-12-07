---
title: Membangun Keamanan Jaringan di Cloud
description: Konfigurasi VPC, Subnet, dan Bastion Host di AWS.
categories: [Cloud Computing, AWS]
tags: [cloud, aws, cybersecurity, linux]
author: rical
---

## VPC
Silakan cari VPC dan buat VPC baru dengan menggunakan opsi **Create VPC** di halaman AWS.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/vpc-settings.png)

## Subnet
Silakan buat empat subnet, terdiri dari dua subnet publik dan dua subnet privat. Untuk **VPC ID**, silakan pilih VPC yang telah dibuat sebelumnya. 
- `public_subnet_1` dan `private_subnet_1`, pilih `us-east-1a`.
- `public_subnet_2` dan `private_subnet_2`, pilih `us-east-1b`.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-subnet.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/public_subnet_1.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/public_subnet_2.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/private_subnet_1.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/private_subnet_2.png)

> - **Availibility Zone** untuk memberikan redundansi dan meningkatkan ketersediaan layanan. Jika satu Availability Zone mengalami gangguan, layanan yang berjalan di Availability Zone lain dalam region yang sama tetap dapat beroperasi.
- **IPv4 CIDR Block** merupakan metode untuk mengalokasikan dan mengidentifikasi alamat IP. IPv4 CIDR block adalah cara untuk mendefinisikan rentang alamat IPv4 dengan menggunakan notasi CIDR. Notasi ini biasanya ditulis dalam format `x.x.x.x/n,` di mana `x.x.x.x` adalah alamat IP dan `n` adalah jumlah bit yang digunakan untuk subnet mask. Misalnya, `192.168.1.0/24` menunjukkan bahwa 24 bit pertama digunakan untuk jaringan, dan sisanya untuk host.
- **IPv4 Subnet CIDR block** adalah bagian dari CIDR yang lebih spesifik, yang digunakan untuk membagi jaringan menjadi subnet yang lebih kecil. Ini memungkinkan pengelolaan alamat IP yang lebih efisien dan meningkatkan keamanan serta kinerja jaringan. Misalnya, jika kita memiliki jaringan `192.168.1.0/24`, kita dapat membagi jaringan ini menjadi beberapa subnet, seperti `192.168.1.0/26` untuk satu subnet dan `192.168.1.64/26` untuk subnet lainnya.
{: .prompt-info}

Selanjutnya, klik kanan pada `public_subnet_1` dan pilih **edit subnet settings**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/edit-subnet-settings.png)

Lakukan konfigurasi ini pada semua subnet publik dan privat. Pastikan untuk mencentang opsi `Enable auto-assign public IPv4 address` dan gulir ke bawah untuk menyimpan pengaturan.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/auto-assign-ip.png)

Selanjutnya, buka **VPC dashboard** dan cari bagian **Internet Gateways**. Kemudian, klik `Create internet gateway`.

> **Internet Gateway** di AWS merupakan komponen yang memungkinkan komunikasi antara instance di dalam Virtual Private Cloud (VPC) dan internet. 
{: .prompt-info}

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-igw.png)

Di halaman `my-igw`, silakan pilih opsi **Actions** dan kemudian pilih **Attach to VPC**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/attach-to-vpc.png)

Pilih VPC yang telah dibuat sebelumnya, kemudian **Attach internet gateway**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/attach-to-vpc-2.png)

## Route Tables

Untuk konfigurasi **Route Tables** buka **VPC dashboard** dan cari bagian **Route Tables**. Kemudian, ``Create route table``.

> Route table adalah sekumpulan aturan yang digunakan untuk menentukan arah lalu lintas jaringan dalam VPC. Setiap route table berisi rute yang mengarahkan paket data ke tujuan tertentu, baik itu ke subnet lain dalam VPC, ke internet, atau ke jaringan eksternal.
{: .prompt-info}

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-route-table.png)

Pilih **Edit routes**:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/edit-routes.png)

Pilih **Internet Gateway** yang telah dibuat sebelumnya.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/edit-routes2.png)

Buka bagian **Subnet associations** dan pilih opsi **Edit subnet associations**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/edit-subnet-associations.png)

Pilih public subnet 1 dan 2.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/edit-subnet-associations2.png)

> Lakukan hal yang sama untuk konfigurasi **PrivateRouteTable**.
{: .prompt-tip}

## Security Group
Pergi ke panel kiri di **VPC dashboard** dan pilih **Security groups**. Klik **Create security group**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-sg.png)

Di bagian `Inbound rules`, atur ke SSH. Setelah itu, gulir ke bawah dan klik **Create security group**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/inbound-rules.png)

## EC2
### `my-host` instance
Buka halaman Amazon EC2, lihat di panel kiri, klik **Instances**, lalu pilih **Launch instances**.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/setup-instance.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/key-pair.png)

Di bagian **Network settings**, silakan konfigurasikan seperti berikut:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/network-settings.png)

Selanjutnya, klik **Launch instance**. Tunggu hingga `Status check` menunjukkan `2/2 checks passed`. Setelah itu, klik **Connect**, gulir ke bawah, dan klik **Connect** lagi.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/checks-passed.png)

Setelah terhubung, periksa instance dengan menjalankan perintah:
```bash 
sudo apt update && sudo apt install -y neofetch
```

```bash 
neofetch
```

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/neofetch.png)

## Bastion Host
Di sini, kita akan membuat instance privat yang terhubung dengan `my-host` yang telah dibuat sebelumnya.

Buka **Instances** di dashboard EC2, pilih **Launch instances**, dan beri nama `private_instances`. Pilih Ubuntu. Untuk `Key pair (login)`, pilih **create new key pair**. Isi nama kunci privat dan simpan dalam format `.pem`.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-key-pair.png)

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/create-key-pair2.png)

Ini akan mengunduh sebuah kunci privat dengan nama `private_key` dalam format `.pem`.

### Network Settings
Di bagian **Network settings**, silakan sesuaikan konfigurasinya seperti berikut:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/private-network-settings.png)

Di bagian security group, atur seperti berikut:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/private-sg.png)

Klik **Launch instance**. Perhatikan bahwa IP public kosong dan hanya terdapat IP private.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/private-instance.png)

Kita tidak dapat terhubung dengan instance ini. Ketika mencoba untuk terhubung, akan muncul tampilan seperti ini:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/error-private-instance.png)

Tenang, ini adalah hal yang wajar karena kita tidak menyetel IP publik. Lalu, bagaimana cara terhubung ke instance ini? Kita akan *remote* menggunakan `my-host`.

Kembali ke terminal `my-host` tadi, dan masukkan perintah berikut:

```bash
nano key.pem
```

Layar akan menampilkan kosong. Salin isi key pair yang sudah diunduh tadi dan tempelkan. Kemudian, tekan `Ctrl + X`, lalu tekan `Y`, dan tekan `Enter`. Gunakan perintah:
```bash
cat key.pm
```

Perintah `cat` akan menampilkan isi file:

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/key.png)

Selanjutnya, masuk ke `private_instance` dengan menggunakan kunci tersebut. Gunakan perintah:

```bash
chmod 4000 key.pem
```

```bash
ssh -i key.pem username@ip_private_instance
```
Gambar berikut menunjukkan bahwa kita berhasil masuk ke **private_instance**. Di sini, kita mencoba melakukan ping ke Google, tetapi terjebak, karena kita hanya berada di **private_instance** tanpa IP public yang disetel.

![img](/assets/img/posts/cloud/2024-11-20-tugas-cloud-computing/ping-private-instance.png)

## Referensi 
- [ricalWiki](https://risnandapascal.github.io/ricalwiki.html)