---
title: Membangun VoIP Server
description: Dapatkan kontrol penuh atas sistem komunikasi dengan panduan mendetail tentang instalasi dan konfigurasi server VoIP menggunakan Asterisk.
categories: [Cybersecurity, Linux, Privacy]
tags: [linux, privacy, open source]
author: rical
---

## Pendahuluan
Panduan ini bertujuan untuk membangun server VoIP dengan memanfaatkan [Asterisk](https://www.asterisk.org/) pada sistem operasi [Linux Mint](https://www.linuxmint.com/download.php) untuk pemula dan [Debian](https://www.debian.org/download) untuk pengguna tingkat lanjut. Ucapan terima kasih kepada [@inibim](https://discord.com/invite/nAVZkEwjYJ) atas kontribusinya dalam pemecahan masalah.

## Panduan untuk Pemula

### Instalasi Server
1. Buka terminal di Linux Mint dan jalankan perintah berikut untuk memperbarui sistem:
   ```bash
   sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
   ```

2. Instal paket yang diperlukan untuk membangun Asterisk:
   ```bash
   sudo apt install build-essential wget subversion && sudo apt install libncurses5-dev libssl-dev libxml2-dev
   ```

3. Instal Asterisk dari repositori Linux Mint:
   ```bash
   sudo apt install -y asterisk
   ```

4. Periksa versi Asterisk yang telah terinstal:
   ```bash
   asterisk -V
   ```

### Konfigurasi
> Sebelum melakukan konfigurasi, cadangkan file `sip.conf`, `extensions.conf`, dan `voicemail.conf`:
```bash
sudo mv /etc/asterisk/sip.conf /etc/asterisk/extensions.conf /etc/asterisk/voicemail.conf ~/Documents
```
Selanjutnya, buka dan hapus isi konfigurasi yang ada di:
- `/etc/asterisk/sip.conf`{: .filepath}
- `/etc/asterisk/extensions.conf`{: .filepath}
- `/etc/asterisk/voicemail.conf`{: .filepath}
{: .prompt-tip}

File konfigurasi utama terletak di `/etc/asterisk`{: .filepath}. Ubah konfigurasi pada file berikut:
- **`/etc/asterisk/asterisk.conf`{: .filepath}**: Ini adalah konfigurasi utama. Biarkan dalam pengaturan *default* untuk saat ini.
- Masukkan konfigurasi berikut ke dalam **`/etc/asterisk/sip.conf`{: .filepath}**:

> SIP (*Session Initiation Protocol*) adalah protokol komunikasi yang digunakan untuk mengelola dan mengatur sesi komunikasi, seperti panggilan suara dan video, di jaringan IP. Dalam konteks Asterisk, sebuah sistem telekomunikasi *open-source* yang sering digunakan sebagai PBX (*Private Branch Exchange*) dan sistem VoIP (*Voice over IP*), SIP memainkan peran penting. Beberapa fitur utama SIP yang ada di Asterisk meliputi:
 - [x] Pendaftaran dan Autentikasi
 - [x] Manajemen Panggilan
 - [x] Negosiasi Media
 - [x] Kompatibilitas
 - [x] Pengaturan Fitur
{: .prompt-info }

```ini
[general]
context=internal
allowguest=no
allowoverlap=no
bindport=5060
bindaddr=0.0.0.0
srvlookup=no
disallow=all
allow=ulaw
alwaysauthreject=yes
canreinvite=no
nat=yes
session-timers=refuse
localnet=192.168.100.220/255.255.255.0 #sesuaikan ip address

[7001]
type=friend
host=dynamic
secret=7001
context=internal

[7002]
type=friend
host=dynamic
secret=7002
context=internal
```

- Selanjutnya, masukkan konfigurasi ini ke dalam **`/etc/asterisk/extensions.conf`{: .filepath}**:

```ini
[internal]
exten => 7001,1,Answer()
exten => 7001,2,Dial(SIP/7001,60)
exten => 7001,3,Playback(vm-nobodyavail)
exten => 7001,4,VoiceMail(7001@main)
exten => 7001,5,Hangup()

exten => 7002,1,Answer()
exten => 7002,2,Dial(SIP/7002,60)
exten => 7002,3,Playback(vm-nobodyavail)
exten => 7002,4,VoiceMail(7001@main)
exten => 7002,5,Hangup()

exten => 8001,1,VoicemailMain(7001@main)
exten => 8001,2,Hangup()

exten => 8002,1,VoicemailMain(7002@main)
exten => 8002,2,Hangup()
```

- Terakhir, masukkan konfigurasi berikut ke dalam **`/etc/asterisk/voicemail.conf`{: .filepath}**:

```ini
[main]
7001 => 7001
7002 => 7002
```

### Mengelola Layanan Asterisk
- Untuk menghentikan layanan:
  ```bash
  sudo systemctl stop asterisk
  ```

- Untuk memulai layanan:
  ```bash
  sudo systemctl start asterisk
  ```

- Untuk melihat status layanan:
  ```bash
  sudo systemctl status asterisk
  ```

### Antarmuka Baris Perintah Asterisk (CLI)
Masuk ke antarmuka baris perintah Asterisk (CLI) dengan menggunakan perintah berikut:
```bash
sudo asterisk -rvv
```

Setelah masuk ke CLI Asterisk, gunakan perintah berikut untuk menampilkan daftar peer SIP yang telah dikonfigurasi dalam sistem Asterisk:
```bash
sip show peers
```

Pengaturan server telah selesai. Untuk menguji komunikasi antar klien, disarankan untuk menggunakan [Linphone](https://www.linphone.org/).

> Direkomendasikan untuk mengubah kata sandi, membatasi akses menggunakan *firewall*, serta melakukan pemantauan log dan sistem secara teratur untuk mendeteksi aktivitas yang mencurigakan demi keamanan yang lebih kuat.
{: .prompt-tip}

## Panduan untuk Pengguna Tingkat Lanjut

### Instalasi Asterisk di Debian
1. Buka terminal dan jalankan perintah berikut untuk memperbarui sistem:
   ```bash
   sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
   ```

2. Instal paket yang diperlukan untuk membangun Asterisk:
   ```bash
   sudo apt install build-essential wget subversion && sudo apt install libncurses5-dev libssl-dev libxml2-dev
   ```

3. Unduh versi terbaru Asterisk dari situs web resmi:
   ```bash
   cd /usr/src && sudo wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-20-current.tar.gz
   ```

4. Ekstrak file yang telah diunduh:
   ```bash
   sudo tar -xvf asterisk-20-current.tar.gz
   ```

### Kompilasi dan Instalasi Asterisk
> Proses ini mungkin memakan waktu cukup lama, jadi siapkan kopi untuk bersantai terlebih dahulu.
{: .prompt-info}

1. Masuk ke direktori Asterisk:
   ```bash
   cd asterisk-20*
   ```

2. Jalankan konfigurasi:
   ```bash
   sudo ./configure
   ```

3. Pilih opsi yang diinginkan dengan menampilkan menu:
   ```bash
   sudo make menuselect
   ```

4. Kompilasi Asterisk:
   ```bash
   sudo make
   ```

5. Instal Asterisk:
   ```bash
   sudo make install
   ```

6. Instal contoh konfigurasi:
   ```bash
   sudo make samples
   ```

7. Buat konfigurasi sistem:
   ```bash
   sudo make config
   ```

### Konfigurasi
Untuk melakukan konfigurasi, lihat bagian [Panduan untuk Pemula](https://ricaldocs.github.io/posts/membangun-voip-server/#panduan-untuk-pemula).

> Menyiapkan server VoIP menggunakan Asterisk pada Debian 12 memerlukan konfigurasi yang cermat. Namun, hasilnya adalah sistem komunikasi yang kuat dan fleksibel.
{: .prompt-warning}

> Jika berencana untuk memperluas skala operasi atau memerlukan bantuan profesional, pertimbangkan untuk menyewa teknisi [DevOps](https://en.wikipedia.org/wiki/DevOps) jarak jauh yang memiliki pengalaman dalam infrastruktur VoIP.
{: .prompt-tip}

## Referensi
- [ricalWiki](https://risnandapascal.github.io/ricalwiki.html)