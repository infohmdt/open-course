---
title: Wireless Network Attack Using the Fluxion Method
description: Meretas kata sandi WiFi dalam hitungan menit.
categories: [Cybersecurity, Linux, Red Team]
tags: [cybersecurity, red team, linux]
author: rical
---

Fluxion adalah alat audit keamanan dan penelitian social engineering yang dirancang untuk menguji keamanan jaringan nirkabel. Alat ini merupakan pengembangan dari [linset](https://github.com/vk496/linset), yang dibuat oleh vk496 dan tidak diperbarui selama enam tahun terakhir. Fluxion menawarkan fungsionalitas yang lebih luas dan berusaha untuk mendapatkan kunci WPA/WPA2 dari titik akses target melalui serangan social engineering (phishing). Alat ini kompatibel dengan Kali Linux.

> Pengguna diharapkan untuk mematuhi semua hukum yang berlaku dan mendapatkan izin eksplisit sebelum melakukan pengujian terhadap jaringan yang bukan milik mereka. Penyalahgunaan alat ini dapat mengakibatkan konsekuensi hukum yang serius dan merusak reputasi profesional di bidang keamanan siber. Penggunaan Fluxion harus dilakukan dengan tanggung jawab dan integritas, serta dengan tujuan untuk meningkatkan keamanan, bukan untuk mengeksploitasi kerentanan.
{: .prompt-danger}

## Instalasi
Proses instalasi Fluxion di Kali Linux cukup sederhana. Pengguna perlu mengkloning Fluxion dari repositori GitHub dengan menggunakan perintah berikut di terminal:

```bash
git clone https://github.com/FluxionNetwork/fluxion
```

Setelah proses kloning selesai, navigasikan ke direktori Fluxion dengan perintah:

```bash
cd fluxion
```

Untuk pertama kalinya, jalankan skrip bash `fluxion.sh` dengan flag `-i` untuk menginstal persyaratan yang diperlukan:

```bash
sudo ./fluxion.sh -i
```

Pada penggunaan berikutnya, cukup jalankan:

```bash
sudo ./fluxion.sh
```

Setelah menginstal persyaratan, aplikasi akan mulai secara otomatis dan meminta pengguna untuk memilih bahasa. Selanjutnya, pengguna perlu memilih antarmuka nirkabel. 

> Jika antarmuka nirkabel sistem mendukung packet injection dan [monitor mode](https://ricaldocs.github.io/posts/enabling-and-disabling-monitor-mode-kali-linux/), maka dapat digunakan. Namun, jika chipset nirkabel pada laptop tidak mendukung fitur tersebut, disarankan untuk menggunakan adaptor nirkabel eksternal yang sesuai, seperti [TP-Link Archer T2U Plus](https://ricaldocs.github.io/posts/memperbaiki-masalah-usb-wifi-adapter-archer-t2u-v3-di-kali-linux/).
{: .prompt-info}

![Select Wireless Interface](assets/img/posts/2025-03-11-fluxion/select-wireless-interface.png)

## Proses Penggunaan
Selanjutnya, pengguna perlu melakukan pemindaian untuk mencari jaringan WiFi yang tersedia di sekitar.

![Channel](assets/img/posts/2025-03-11-fluxion/channel.png)

Pengguna dapat memilih untuk mencari sinyal dual band atau sinyal dari saluran tertentu selama proses pemindaian. Setelah pilihan dibuat, Fluxion akan mulai mendeteksi jaringan nirkabel yang ada di sekitar, memberikan informasi tentang jaringan yang terdeteksi, termasuk kekuatan sinyal dan jenis enkripsi yang digunakan. Proses ini memungkinkan pengguna untuk mengidentifikasi jaringan target yang mungkin menjadi fokus dalam audit keamanan.

![Fluxion Scanner](assets/img/posts/2025-03-11-fluxion/fluxion-scanner.png)

Setelah memberikan waktu yang cukup untuk mendeteksi semua jaringan nirkabel, pengguna dapat menghentikan proses pemindaian dengan menekan kombinasi tombol `ctrl + c`. Setelah itu, Fluxion akan menampilkan daftar jaringan WiFi yang berhasil ditemukan, lengkap dengan informasi terkait seperti nama jaringan (SSID), kekuatan sinyal, dan jenis enkripsi yang digunakan. Daftar ini akan membantu pengguna dalam memilih jaringan target untuk langkah selanjutnya dalam proses audit keamanan.

![Wifi List](assets/img/posts/2025-03-11-fluxion/wifi-list.png)

Selanjutnya, pengguna diminta untuk memilih antarmuka nirkabel yang akan digunakan untuk pelacakan jaringan. Jika pengguna tidak yakin tentang pilihan yang harus diambil, mereka dapat melewati langkah ini dengan memilih opsi 3. 

![Target Tracking](assets/img/posts/2025-03-11-fluxion/target-tracking.png)

Setelah memilih antarmuka nirkabel, langkah selanjutnya adalah memilih metode pengambilan handshake. 

> MDK4 memiliki kemampuan untuk melakukan serangan de-authentication, di mana alat ini dapat mengirimkan paket de-authentication ke perangkat yang terhubung ke jaringan, memaksa mereka untuk terputus dari jaringan. Setelah terputus, penyerang dapat mencoba untuk menangkap kredensial otentikasi saat perangkat mencoba untuk terhubung kembali.
{: .prompt-info}

![Handshake Retrieval](assets/img/posts/2025-03-11-fluxion/handshake-retrieval.png)

Untuk tujuan [jamming](https://en.wikipedia.org/wiki/Radio_jamming) dan monitoring, pengguna perlu memilih antarmuka yang akan digunakan. Dalam konteks ini, pengguna disarankan untuk memilih kartu nirkabel yang mendukung fitur tersebut, seperti kartu [Archer T2U Plus](https://ricaldocs.github.io/posts/memperbaiki-masalah-usb-wifi-adapter-archer-t2u-v3-di-kali-linux/), yang dalam contoh ini diidentifikasi sebagai `wlan0`.

![Interface for Jamming](assets/img/posts/2025-03-11-fluxion/interface-for-jamming.png)

Setelah memilih antarmuka, Fluxion akan meminta pengguna untuk melakukan proses verifikasi hash. Pada tahap ini, pengguna akan diberikan beberapa opsi untuk metode verifikasi yang dapat digunakan.

> Disarankan untuk mengikuti metode yang direkomendasikan oleh Fluxion, karena ini biasanya merupakan cara yang paling efektif dan aman untuk memastikan bahwa proses pengambilan handshake berjalan dengan baik.
{: .prompt-tip}

> Cowpatty berfungsi dengan membandingkan hash yang ditangkap dari komunikasi jaringan dengan hash yang dihasilkan dari kata sandi yang terdapat dalam daftar kata (wordlist). Jika terdapat kecocokan, maka kata sandi yang benar dapat diidentifikasi. Penggunaan Cowpatty umumnya dilakukan dalam pengujian penetrasi untuk mengevaluasi kekuatan kata sandi jaringan nirkabel.
{: .prompt-info}

![Verification Method](assets/img/posts/2025-03-11-fluxion/verification-method.png)

Opsi-opsi lainnya dalam proses ini bersifat dasar dan tidak memerlukan penjelasan mendalam. Setelah semua pengaturan selesai, Fluxion akan mulai melakukan de-authentikasi terhadap semua perangkat yang terhubung ke jaringan nirkabel yang menjadi target. Proses de-authentikasi ini akan memaksa perangkat-perangkat tersebut untuk terputus dari jaringan. Ketika perangkat yang telah dide-authentikasi mencoba untuk terhubung kembali, Fluxion akan menangkap handshake yang diperlukan untuk mendapatkan kunci WPA/WPA2. Proses ini merupakan inti dari serangan yang dilakukan oleh Fluxion dan memungkinkan pengguna untuk melanjutkan ke langkah berikutnya dalam mendapatkan akses ke jaringan target.

![Handshake Capturing](assets/img/posts/2025-03-11-fluxion/handshake-capturing.png)

Meskipun jenis serangan ini dapat dilaksanakan dengan menggunakan [aircrack-ng](https://www.aircrack-ng.org/), Fluxion menyediakan pendekatan yang lebih canggih dan lebih ramah pengguna.

![Handshake Snooper](assets/img/posts/2025-03-11-fluxion/handshake-snooper.png)

## Evil-Twin Attack
Fluxion juga memiliki kemampuan untuk melakukan serangan Evil-Twin. Dalam teknik serangan ini, pengguna mengirimkan paket de-authentikasi secara terus-menerus kepada perangkat yang terhubung ke jaringan target, sehingga semua klien yang terhubung akan terputus dari jaringan tersebut. Sementara itu, pengguna menciptakan jaringan WiFi baru dengan nama yang sama (SSID) seperti jaringan asli. Jika klien menganggap jaringan WiFi yang baru dibuat tersebut sebagai jaringan asli mereka, mereka akan terjebak dan dapat secara tidak sadar memberikan kredensial mereka kepada penyerang. 

Teknik ini mirip dengan metode phishing, di mana pengguna tertipu untuk memasukkan informasi sensitif ke dalam jaringan yang tidak aman. Serangan Evil-Twin ini merupakan salah satu cara yang efektif untuk mendapatkan akses tidak sah ke informasi pengguna dan dapat digunakan dalam konteks pengujian penetrasi untuk mengidentifikasi kerentanan dalam keamanan jaringan.

## Pranala Menarik
- [Penetration Testing](https://ricaldocs.github.io/posts/penetration-testing/)
- [Linux Incident Response and Forensics](https://ricaldocs.github.io/posts/linux-incident-response-and-forensics/)