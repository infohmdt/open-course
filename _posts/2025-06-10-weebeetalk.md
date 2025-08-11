---
title: WeeBeeTalk
description: A Privacy-Preserving Hybrid Telecommunication Architecture for Enterprise Conferencing Using Open-Source Stack Integration
categories: [Cloud Computing, RicalNet]
tags: [cloud, docker, cybersecurity, privacy, RicalNet]
author: rical
---

## 1. Pendahuluan

[WeeBeeTalk](https://ricaldocs.github.io/posts/weebeetalk/) merupakan arsitektur telekomunikasi hybrid berorientasi privasi yang dirancang khusus untuk memenuhi kebutuhan konferensi enterprise melalui integrasi tumpukan teknologi sumber terbuka (open-source stack). Solusi ini dikembangkan oleh [Risnanda Pascal](https://ricaldocs.github.io/posts/risnanda-pascal/) & [Gineng B. Pamungkas](https://astarajingga.github.io) sebagai respons terhadap tantangan kontemporer dalam komunikasi bisnis modern, terutama menyangkut kerahasiaan data, interoperabilitas sistem, dan kontrol infrastruktur mandiri. 

Dalam konteks lingkungan korporat yang semakin terdigitalisasi, kebutuhan akan platform konferensi yang mampu menjamin keamanan end-to-end tanpa mengorbankan fungsionalitas menjadi krusial. Arsitektur hybrid [WeeBeeTalk](https://ricaldocs.github.io/posts/weebeetalk/) memadukan teknologi berbasis IP ([Rocket.Chat](https://www.rocket.chat/)), komunikasi real-time berbasis WebRTC ([Jitsi](https://jitsi.org/)), dan teleponi tradisional ([Asterisk](https://www.asterisk.org/)) dalam satu ekosistem terintegrasi. Pendekatan ini memungkinkan organisasi untuk:
1. Mempertahankan kedaulatan data melalui implementasi *on-premise*
2. Mengurangi ketergantungan pada penyedia layanan cloud pihak ketiga
3. Menerapkan kebijakan enkripsi dan otentikasi yang konsisten
4. Menjaga interoperabilitas dengan infrastruktur telekomunikasi existing

Inti arsitektur ini terletak pada integrasi strategis tiga komponen utama: 
- [Rocket.Chat](https://www.rocket.chat/) sebagai platform kolaborasi berbasis pesan instan
- [Jitsi Meet](https://jitsi.org/) sebagai engine konferensi video WebRTC
- [Asterisk](https://www.asterisk.org/) sebagai gateway teleponi berbasis IP-PBX

![WeeBeeTalk Architecture](/assets/img/posts/2025-06-10-weebeetalk/weebeetalk.png)
_WeeBeeTalk Architecture_

Implementasi [WeeBeeTalk](https://ricaldocs.github.io/posts/weebeetalk/) mengadopsi paradigma "privacy by design" dengan menerapkan enkripsi end-to-end pada semua lapisan komunikasi (data-at-rest dan data-in-transit), Role-Based Access Control (RBAC), serta mekanisme autentikasi multi-faktor.

## 2. Lingkungan Sistem dan Prasyarat  
[WeeBeeTalk](https://ricaldocs.github.io/posts/weebeetalk/) diimplementasikan pada lingkungan sistem operasi [Debian GNU/Linux](https://www.debian.org/) (versi stabil terkini) sebagai platform dasar, dipilih karena stabilitas jangka panjang (LTS), ekosistem paket yang komprehensif, dan kompatibilitas optimal dengan tumpukan teknologi open-source yang digunakan. Implementasi ini mengasumsikan lingkungan server Debian minimal dengan konfigurasi berikut:  

### 2.1. Spesifikasi Sistem Minimum  
- **Sistem Operasi**: Debian 12 (Bookworm) x86_64  
- **CPU**: 4 core (x64 architecture)  
- **RAM**: 8 GB  
- **Storage**: 50 GB (SSD direkomendasikan)  
- **Jaringan**: Alamat IP publik statis/DNS yang terkonfigurasi  

### 2.2. Prasyarat Khusus Debian  
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

```bash
sudo apt install -y apt-transport-https ca-certificates gnupg2 curl software-properties-common
```

## 3. Konfigurasi Rocket.Chat via Docker
### 3.1 Struktur Direktori
Struktur direktori dasar untuk pengembangan adalah sebagai berikut:
```bash
weebeetalk/
├── docker-compose.yml  # Konfigurasi container
├── .env                # Variabel lingkungan
└── mongodb_data/       # Volume database
└── jitsi/              # WebRTC
```

Untuk membuat direktori dan berpindah ke dalamnya, gunakan perintah berikut:

```bash
mkdir weebeetalk && cd weebeetalk
```

> Lihat dokumentasi mengenai [instalasi Docker](https://docs.docker.com/engine/install/debian/) di Debian.
{: .prompt-tip}

### 3.2 File Konfigurasi
Unduh konfigurasi resmi dengan menjalankan perintah berikut:

```bash
curl -O https://raw.githubusercontent.com/RocketChat/Docker.Official.Image/master/compose.yml
```

Buat file `.env`{: .filepath} dengan konten berikut:

```ini
NODE_VERSION=
DENO_VERSION=
MONGODB_VERSIONS=
APPS_ENGINE_VERSION=
```

> Lihat versi rilis di [halaman berikut](https://github.com/RocketChat/Rocket.Chat/releases).
{: .prompt-tip}

### 3.3 Perintah Deployment
Untuk memulai kontainer, jalankan perintah berikut:
```bash
docker compose up -d 
```

Untuk memverifikasi status kontainer, gunakan perintah berikut:
```bash
docker ps -a
```

## 4. Integrasi dengan WebRTC (Jitsi)
### 4.1 Paket yang Diperlukan dan Pembaruan Repositori
Untuk menyiapkan lingkungan yang diperlukan, paket-paket berikut harus diinstal:

Paket: 
- `gnupg2`: Implementasi lengkap dan gratis dari standar OpenPGP.
- `nginx-full`: Server web berkinerja tinggi dan server proxy terbalik.
- `sudo`: Diperlukan hanya jika berniat menggunakan sudo untuk tugas administratif.
- `curl`: Alat baris perintah untuk mentransfer data dengan URL. Sebagai alternatif, wget dapat digunakan untuk menambahkan repositori paket Jitsi.

Pastikan sistem diperbarui dan paket-paket yang diperlukan telah diinstal. Jalankan sebagai `root` atau dengan `sudo`:

```bash
sudo apt update && sudo apt install -y apt-transport-https gnupg2 nginx-full curl
```

> Sangat penting untuk menggunakan OpenJDK 11 demi kompatibilitas dan kinerja yang optimal.
{: .prompt-info}

### 4.2 Instalasi Jitsi Meet
#### 4.2.1 Menginstal Kunci Repositori Jitsi
Kunci repositori Jitsi dapat diinstal ke dalam sistem dengan menjalankan perintah berikut:

```bash
curl https://download.jitsi.org/jitsi-key.gpg.key | sudo sh -c 'gpg --dearmor > /usr/share/keyrings/jitsi-keyring.gpg'
```

#### 4.2.2 Membuat File `sources.list.d`{: .filepath} dengan Repositori

File `sources.list.d`{: .filepath} untuk repositori Jitsi dapat dibuat menggunakan perintah berikut:

```bash
echo 'deb [signed-by=/usr/share/keyrings/jitsi-keyring.gpg] https://download.jitsi.org stable/' | sudo tee /etc/apt/sources.list.d/jitsi-stable.list > /dev/null
```

#### 4.2.3 Memperbarui Daftar Paket
Daftar paket dapat diperbarui dengan menjalankan perintah berikut:

```bash
sudo apt update
```

#### 4.2.4 Menyiapkan dan Mengonfigurasi Firewall
Port-port berikut perlu dibuka di firewall untuk memungkinkan lalu lintas ke server Jitsi Meet:

- `80 TCP`: Untuk verifikasi/pembaruan sertifikat SSL dengan Let's Encrypt. Diperlukan.
- `443 TCP`: Untuk akses umum ke Jitsi Meet. Diperlukan.
- `10000 UDP`: Untuk pertemuan audio/video jaringan umum. Diperlukan.
- `22 TCP`: Untuk mengakses server menggunakan SSH (port dapat diubah sesuai kebutuhan jika bukan 22). Diperlukan.
- `3478 UDP`: Untuk menanyakan server STUN (coturn, opsional, perlu perubahan di `config.js` untuk mengaktifkannya).
- `5349 TCP`: Untuk komunikasi video/audio jaringan cadangan melalui TCP (misalnya, ketika UDP diblokir), dilayani oleh coturn. Diperlukan.

Jika menggunakan `ufw`, buka port dengan perintah berikut:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow 10000/udp
sudo ufw allow 22/tcp
sudo ufw allow 3478/udp
sudo ufw allow 5349/tcp
sudo ufw enable
```

Status firewall dapat diperiksa dengan menjalankan perintah berikut:

```bash
sudo ufw status verbose
```

#### 4.2.5 Sertifikat TLS
Untuk memastikan komunikasi yang terenkripsi, diperlukan sertifikat TLS.

Selama instalasi Jitsi Meet, terdapat beberapa opsi yang dapat dipilih:
1. Opsi yang direkomendasikan adalah memilih sertifikat dari Let's Encrypt.
2. Jika ingin menggunakan sertifikat yang berbeda, sertifikat tersebut harus diperoleh terlebih dahulu, kemudian Jitsi Meet dapat diinstal dengan memilih opsi "**I want to use my own certificate**."
3. Penggunaan [sertifikat yang ditandatangani sendiri](https://ricaldocs.github.io/posts/mastering-self-signed-certificates/) juga dimungkinkan dengan memilih opsi "**Generate a new self-signed certificate**," tetapi ini tidak disarankan karena beberapa alasan:
   - Penggunaan [sertifikat yang ditandatangani sendiri](https://ricaldocs.github.io/posts/mastering-self-signed-certificates/) akan mengakibatkan peringatan di browser pengguna, karena identitas server tidak dapat diverifikasi.
   - Aplikasi seluler Jitsi Meet memerlukan sertifikat yang valid dan ditandatangani oleh [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority) yang tepercaya. Jika menggunakan [sertifikat yang ditandatangani sendiri](https://ricaldocs.github.io/posts/mastering-self-signed-certificates/), aplikasi tidak akan dapat terhubung ke server.

#### 4.2.6 Menginstal Paket Jitsi
Seluruh suite Jitsi dapat diinstal dengan menjalankan perintah berikut:

```bash
sudo apt install -y jitsi-meet
```

**Generasi Sertifikat SSL/TLS**: Selama instalasi, akan diminta untuk melakukan generasi sertifikat SSL/TLS. Untuk detail lebih lanjut, lihat bagian [di atas](https://ricaldocs.github.io/posts/weebeetalk/#425-sertifikat-tls).

**Hostname**: Selanjutnya, akan diminta untuk memasukkan nama host dari instance Jitsi Meet. Jika memiliki domain, gunakan nama domain spesifik, misalnya: `meet.example.org`. Sebagai alternatif, alamat IP mesin dapat dimasukkan (jika statis atau tidak berubah).

Nama host ini akan digunakan untuk konfigurasi virtual host di dalam Jitsi Meet dan juga akan digunakan oleh pengguna untuk mengakses konferensi web.

> Untuk menginstal paket tertentu dari Jitsi, gunakan perintah berikut:
```bash
sudo apt -y install jitsi-videobridge
sudo apt -y install jicofo
sudo apt -y install jigasi
```
{: .prompt-tip}

#### 4.2.7 Access Control
**Server Jitsi Meet**: Secara default, siapa pun yang memiliki akses ke server Jitsi Meet dapat memulai konferensi. Jika server terbuka untuk umum, siapa pun dapat melakukan obrolan dengan orang lain.

**Conferences/Rooms**: Kontrol akses untuk konferensi atau ruang dikelola di dalam ruang tersebut. Kata sandi dapat diatur di halaman web ruang tertentu setelah dibuat.

**Konfigurasi Lanjutan**: Jika instalasi dilakukan pada mesin [di belakang NAT](https://jitsi.github.io/handbook/docs/faq#how-to-tell-if-my-server-instance-is-behind-nat), jitsi-videobridge seharusnya mengonfigurasi dirinya secara otomatis saat boot. Jika panggilan tiga arah tidak berfungsi, konfigurasi lebih lanjut dari jitsi-videobridge diperlukan agar dapat diakses dari luar.

Pastikan semua port yang diperlukan telah diarahkan (forwarded) ke mesin tempat jitsi-videobridge berjalan. Secara default, port yang digunakan adalah TCP/443 dan UDP/10000.

Tambahkan pemetaan statis ke bagian `ice4j.harvest.mapping` di `/etc/jitsi/videobridge/jvb.conf`{: .filepath}:

```
ice4j {
  harvest {
    mapping {
      static-mappings = [
        {
          local-address = "<Local.IP.Address>"
          public-address = "<Public.IP.Address>"
        }
      ]
    }
  }
}
```

**Systemd/Limits**: Penerapan default akan memiliki nilai rendah untuk maksimum proses dan file terbuka. Untuk lebih dari 100 peserta, ubah `/etc/systemd/system.conf`{: .filepath} menjadi:

```
DefaultLimitNOFILE=65000
DefaultLimitNPROC=65000
DefaultTasksMax=65000
```

**Detail Systemd**

Untuk memuat perubahan systemd pada sistem yang sedang berjalan, eksekusi perintah berikut:

```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl restart jitsi-videobridge2
```

Untuk memeriksa bagian tugas, jalankan:

```bash
sudo systemctl status jitsi-videobridge2
```

Untuk memeriksa nilai-nilai tersebut, jalankan perintah berikut:

```bash
systemctl show --property DefaultLimitNPROC
```

```bash
systemctl show --property DefaultLimitNOFILE
```

```bash
systemctl show --property DefaultTasksMax
```

Seharusnya terlihat `Tasks: XX (limit: 65000)`. Untuk memeriksa bagian file dan proses, jalankan:

```bash
cat /proc/`cat /var/run/jitsi-videobridge/jitsi-videobridge.pid`/limits
```

Seharusnya terlihat:

```
Max processes             65000                65000                processes
Max open files            65000                65000                files
```

#### 4.2.8 Konfirmasi bahwa Instalasi Berfungsi

Luncurkan peramban web (seperti Firefox, Chrome, atau Safari) dan masukkan nama host atau alamat IP dari langkah sebelumnya ke dalam bilah alamat.

Jika menggunakan [sertifikat yang ditandatangani sendiri](https://ricaldocs.github.io/posts/mastering-self-signed-certificates/) (berbeda dengan menggunakan Let's Encrypt), peramban web akan meminta konfirmasi untuk mempercayai sertifikat tersebut. Jika menguji dari aplikasi iOS atau Android, kemungkinan besar akan gagal pada titik ini jika menggunakan [sertifikat yang ditandatangani sendiri](https://ricaldocs.github.io/posts/mastering-self-signed-certificates/).

Setelah mengakses, seharusnya terlihat halaman web yang meminta untuk membuat pertemuan baru. Pastikan dapat berhasil membuat pertemuan dan bahwa peserta lain dapat bergabung dalam sesi tersebut.

Jika semua langkah ini berhasil, maka layanan konferensi Jitsi telah beroperasi dengan baik.

### 4.3 Instalasi Jitsi Meet via Docker (Recommended)
Salah satu metode untuk menginstal Jitsi Meet adalah melalui Docker, yang menyediakan lingkungan terisolasi untuk menjalankan aplikasi.

#### Langkah-langkah Instalasi
1. Untuk memulai, kloning repositori resmi Jitsi Meet dari GitHub dengan perintah berikut:

   ```bash
   git clone https://github.com/jitsi/docker-jitsi-meet.git && cd docker-jitsi-meet
   ```

2. Salin file contoh konfigurasi ke dalam file `.env`{:. filepath} yang akan digunakan untuk mengatur variabel lingkungan:

   ```bash
   cp env.example .env
   ```

3. Buka file `.env`{:. filepath} menggunakan editor teks dan sesuaikan konfigurasi yang diperlukan. Pastikan untuk mengganti nilai `PUBLIC_URL` dengan URL yang akan digunakan untuk mengakses Jitsi Meet secara publik. Contoh:

   ```plaintext
   PUBLIC_URL=https://your-domain.com
   ```

4. Untuk meningkatkan keamanan, jalankan skrip berikut untuk menghasilkan password yang diperlukan:

   ```bash
   ./gen-passwords.sh
   ```

5. Setelah semua konfigurasi selesai, jalankan Jitsi Meet dengan menggunakan Docker Compose. Pastikan berada di direktori `docker-jitsi-meet`{:. filepath} dan jalankan perintah berikut:

   ```bash
   docker-compose up -d
   ```

[Konfirmasi bahwa Instalasi Berfungsi](https://ricaldocs.github.io/posts/weebeetalk/#428-konfirmasi-bahwa-instalasi-berfungsi).

## 5. Integrasi dengan Asterisk
Lihat dokumentasi tentang [Membangun VoIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/) menggunakan Asterisk.

## Pranala Luar
- [Deploy Rocket.Chat](https://docs.rocket.chat/docs/deploy-with-docker-docker-compose)
- [Asterisk Manager Interface AMI](https://docs.asterisk.org/Configuration/Interfaces/Asterisk-Manager-Interface-AMI/)
- [Jitsi Meet Handbook](https://jitsi.github.io/handbook/docs/intro)

## Pranala Menarik
- [Home Server](https://ricaldocs.github.io/posts/home-server/)
- [Membangun VoIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/)
- [Docker Command Reference](https://ricaldocs.github.io/posts/docker-command-reference/)