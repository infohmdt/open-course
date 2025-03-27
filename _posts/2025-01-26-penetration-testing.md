---
title: Penetration Testing
description: Menjelaskan tahapan yang harus dilalui dalam pelaksanaan pengujian penetrasi (pentesting).
categories: [Cybersecurity, Red Team]
tags: [cybersecurity, red team]
author: rical
---

## Penetration Testing
---

Penetration Testing atau pentesting adalah suatu metode evaluasi keamanan yang bertujuan untuk mengidentifikasi dan mengeksploitasi kerentanan dalam sistem komputer, jaringan, atau aplikasi dengan mensimulasikan serangan dari entitas yang tidak berwenang. Tujuan utama dari pentesting adalah untuk mengungkap potensi risiko keamanan dan memberikan rekomendasi yang relevan untuk meningkatkan postur keamanan.

## Tahapan Penetration Testing
---

### 1. Perencanaan dan Persiapan
---

#### 1.1 Tujuan dan Ruang Lingkup
---

Pada fase ini, tim pentester menetapkan tujuan pengujian serta ruang lingkup yang akan dievaluasi. Ruang lingkup dapat mencakup sistem, aplikasi, dan jaringan yang relevan dengan konteks pengujian.

#### 1.2 Izin
---

Sebelum pelaksanaan pentesting, penting untuk memperoleh izin tertulis dari pemilik sistem. Hal ini bertujuan untuk memastikan bahwa pengujian dilakukan dalam kerangka hukum dan etika yang berlaku.

#### 1.3 Pembentukan Tim
---

Tim pentester harus terdiri dari individu yang memiliki kompetensi yang sesuai, termasuk pengetahuan mendalam tentang keamanan siber, pemrograman, dan teknik eksploitasi.

### 2. Pengumpulan Informasi
---

#### 2.1 Reconnaissance
Pengumpulan informasi dilakukan untuk memperoleh pemahaman yang lebih baik mengenai target. Terdapat dua jenis reconnaissance:

- **Passive Reconnaissance**: Mengumpulkan informasi tanpa interaksi langsung dengan target, menggunakan metode seperti WHOIS, DNS lookup, dan analisis media sosial.
- [**Active Reconnaissance**](https://ricaldocs.github.io/posts/active-reconnaissance): Melibatkan penggunaan alat untuk memindai dan mengidentifikasi layanan yang berjalan pada target, contohnya dengan menggunakan Nmap.

### 3. Pemindaian
---

#### 3.1 Port Scanning
---

Pada tahap ini, pentester melakukan pemindaian untuk mengidentifikasi port yang terbuka serta layanan yang berjalan pada port tersebut.

#### 3.2 Vulnerability Scanning
---

Menggunakan alat pemindai kerentanan, seperti Nessus atau OpenVAS, untuk mendeteksi kerentanan yang ada dalam sistem. Pemindaian ini berfungsi untuk mengidentifikasi titik lemah yang dapat dieksploitasi.

### 4. Eksploitasi
---

#### 4.1 Eksploitasi Kerentanan
---

Setelah kerentanan teridentifikasi, pentester berupaya untuk mengeksploitasi kerentanan tersebut guna memperoleh akses ke sistem. Ini dapat melibatkan:

- Penggunaan exploit yang telah ada.
- Pengembangan exploit kustom jika diperlukan.

### 5. Pemeliharaan Akses
---

#### 5.1 Backdoor
---

Jika pentester berhasil mendapatkan akses, mereka akan berusaha untuk menciptakan backdoor guna mempertahankan akses ke sistem.

#### 5.2 Privilege Escalation
---

Mencoba untuk meningkatkan hak akses guna memperoleh kontrol yang lebih besar atas sistem yang diuji.

### 6. Analisis dan Pelaporan
---

#### 6.1 Dokumentasi Temuan
---

Semua temuan harus dicatat secara rinci, termasuk kerentanan yang ditemukan, metode eksploitasi yang digunakan, dan data yang diakses.

#### 6.2 Laporan
---

Menyusun laporan yang jelas dan terperinci yang mencakup:

- Ringkasan eksekutif.
- Temuan teknis.
- Rekomendasi untuk perbaikan.

### 7. Tindak Lanjut
---

#### 7.1 Diskusi dengan Klien
---

Setelah laporan disusun, tim pentester harus mempresentasikan hasil pentesting kepada klien dan mendiskusikan langkah-langkah perbaikan yang diperlukan.

#### 7.2 Re-Test
---

Setelah perbaikan dilakukan, penting untuk melakukan pengujian ulang guna memastikan bahwa kerentanan telah diperbaiki.

### 8. Penutupan
---

#### 8.1 Hapus Jejak
---

Pastikan untuk menghapus semua jejak yang ditinggalkan selama pengujian untuk menjaga kerahasiaan dan integritas sistem.

#### 8.2 Evaluasi Proses
---

Tinjau proses pentesting untuk mengidentifikasi area yang dapat ditingkatkan di masa mendatang.

## Etika dan Hukum
---

Pelaksanaan pentesting harus mematuhi etika dan hukum yang berlaku. Pentester wajib menjaga kerahasiaan data yang diakses selama pengujian dan tidak menyalahgunakan informasi yang diperoleh.

## Pranala Menarik
---

- [Active Reconnaissance](https://ricaldocs.github.io/posts/penetration-testing/)

## Referensi 
---

- [ricalWiki: Penetration Testing](https://ricalnet.github.io/ricalwiki.html)