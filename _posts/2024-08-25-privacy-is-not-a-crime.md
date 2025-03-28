---
title: Privacy Is Not A Crime
description: Kebutuhan untuk melindungi informasi pribadi sering kali dipandang sebagai sesuatu yang terlalu rumit atau bahkan mencurigakan. Padahal, menjaga privasi adalah hak kita sebagai pengguna teknologi. 
categories: [Cybersecurity, Privacy]
tags: [cybersecurity, privacy, open source]
author: rical
pin: true
image:
  path: /assets/img/posts/snowden.jpg
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

## Pendahuluan
Menjaga privasi di internet ibarat merawat kebun yang penuh dengan tanaman berharga. Sementara itu, kita tahu bahwa kebun ini terpapar sinar matahari dan angin bebas, dan sulit untuk menutup seluruhnya. Begitu juga dengan privasi di dunia maya, hampir tidak mungkin untuk sepenuhnya menghilangkan jejak kita. Namun, kita bisa mengurangi risiko agar kebun kita tetap hijau dan aman dari pengunjung yang tidak diinginkan.

Meskipun usaha ini memerlukan perhatian dan kehati-hatian, penting untuk bertanya pada diri sendiri: Apakah kita benar-benar ingin membiarkan privasi kita tergerus begitu saja?

## Melakukan Adaptasi
Kadang-kadang, kita terbuai oleh posisi nyaman dan enggan untuk bergerak, seperti saat duduk santai di kursi empuk yang membuat kita lupa waktu. Namun, sikap ini bisa menjadi jebakan, karena kita sering kali tidak mengetahui kebijakan dari berbagai platform digital dan seringkali menyetujuinya tanpa membaca isinya.

> Kunjungi pengaturan setiap aplikasi dan pengaturan sistem, lalu nonaktifkan semua fitur personalisasi, program pengalaman pengguna, dan iklan yang dipersonalisasi. Pokoknya semua hal yang berbau [telemetri](https://id.wikipedia.org/wiki/Telemetri).
{: .prompt-tip}

> Matikan akses yang tidak diperlukan seperti kamera, mikrofon, lokasi, Bluetooth, dan lainnya. Gunakan di situasi penting saja.
{: .prompt-tip}

Sebagai alternatif, pertimbangkan untuk beralih ke aplikasi *open source*, yang ibaratnya adalah rumah kaca di mana kita bisa melihat setiap rinci tanaman di dalamnya. Dengan *open source*, kita dapat memeriksa kode secara langsung dan jika ada potensi masalah, kita bisa segera mengidentifikasinya dan melaporkannya kepada pengembang. Di dunia *open source*, pengembang pun akan lebih berhati-hati karena transparansi yang tinggi mengurangi kemungkinan adanya kode berbahaya atau *spyware*.

## Alternatif
### Sistem Operasi

| Nama                          | Alternatif     |
| :--------------------- | :--------------- |
| Desktop        | [QubesOS](https://www.qubes-os.org/) <br> [TailsOS](https://tails.net/) <br> [Whonix](https://www.whonix.org/) <br> [OpenBSD](https://www.openbsd.org/)|
| Android       | [LineageOS](https://lineageos.org/) <br> [GrapheneOS](https://grapheneos.org/) <br> [CalyxOS](https://calyxos.org/) <br> [LibreMobileOS](https://lmo.framer.website)<br> [/e/OS](https://e.foundation/e-os/) <br> Custom Rom (Vanilla Build) |

### Rekomendasi Penggunaan Sehari-hari

| Nama                   | Alternatif                                         | Desktop | Mobile |
|------------------------|-----------------------------------------------------|---------|--------|
| Google Play Services   | [MicroG](https://ricaldocs.github.io/posts/microg/)                      | No      | Yes    |
| App Store / Play Store | [F-Droid](https://f-droid.org/) (Open Source APK Store) <br> [Aurora Store](https://auroraoss.com/) (GPlay Store Alternative)                    | No      | Yes    |
| Authenticator          | [Aegis Authenticator](https://getaegis.app/) (Android only) <br> [Ente Auth](https://ente.io/auth/) | Yes      | Yes    |
| Browser                | [TOR Browser](https://www.torproject.org/) <br> [Brave](https://brave.com/) <br> [Firefox](https://www.mozilla.org/en-US/firefox/) | Yes     | Yes    |
| Email                  | [ProtonMail](https://protonmail.com/) <br> [TutaMail](https://tutanota.com/) | Yes     | Yes    |
| Peta                | [OpenStreetMap](https://openstreetmap.org) <br> [Organic Maps](https://organicmaps.app/) | Yes     | Yes    |
| Pesan                  | [Session](https://getsession.org/) <br> [Signal](https://signal.org/) / [Molly](https://molly.im/) <br> [Telegram](https://telegram.org/) | Yes     | Yes    |
| Catatan                | [Standard Notes](https://standardnotes.com/)       | Yes     | Yes    |
| Mesin Pencari          | [Startpage](https://startpage.com) <br> [DuckDuckGo](https://duckduckgo.com) | Yes     | Yes    |
| Penyimpanan            | [NextCrow](https://ricalnet.github.io/website/NextCrow.html) | Yes     | Yes    |
| VPN                    | [Riseup VPN](https://riseup.net/en/vpn) <br> [ProtonVPN](https://protonvpn.com/) | Yes     | Yes    |

### Alat
- [TOR Project](https://www.torproject.org/)
- [I2P](https://geti2p.net/en/)
- [Proxychains](https://github.com/haad/proxychains)
- [Prabu Incognito](https://ricaldocs.github.io/posts/prabu-incognito/)
- [DynamicArchive](https://ricaldocs.github.io/posts/DynamicArchive/)

## Membangun Ekosistem
Jika memiliki keahlian teknis di bidang server dan jaringan, pertimbangkan untuk membangun ekosistem sendiri. silakan merujuk pada dokumentasi [Home Server](https://ricaldocs.github.io/posts/home-server/) dan [Membangun VOIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/), yang dapat menjadi dasar yang berguna untuk memulai.

## Pranala Menarik 
- [Home Server](https://ricaldocs.github.io/posts/home-server/) 
- [Membangun VOIP Server](https://ricaldocs.github.io/posts/membangun-voip-server/)
- [Pelacakan Digital oleh Perusahaan Teknologi Besar dan Pemerintah](https://ricaldocs.github.io/posts/pelacakan-digital-oleh-perusahaan-teknologi-besar-dan-pemerintah/)

## Referensi
- [ricalWiki: Privacy Is Not A Crime](https://ricalnet.github.io/ricalwiki.html)