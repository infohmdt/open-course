---
title: GNU Privacy Guard
description: Dengan GnuPG, kita dapat mengamankan pesan dan file dari pengintaian, memastikan integritas dan keaslian informasi dalam dunia digital yang penuh ancaman.
categories: [Cybersecurity, Linux, Privacy]
tags: [cybersecurity, linux, privacy, open source]
author: rical
---

## Pendahuluan
---

**GNU Privacy Guard** (GnuPG atau GPG) adalah alat kriptografi sumber terbuka yang dirancang untuk melindungi data melalui [enkripsi](https://en.wikipedia.org/wiki/Encryption#Encryption_in_cryptography) dan tanda tangan digital. GnuPG dibangun berdasarkan standar OpenPGP, yang memungkinkan pengguna untuk menjaga privasi komunikasi dan integritas informasi dengan cara yang aman.

Dengan GnuPG, pengguna dapat mengamankan pesan dan file dari pengintaian, serta memastikan integritas dan keaslian informasi dalam dunia digital yang penuh ancaman. Meskipun berbagai aplikasi pengelola kata sandi tersedia, banyak pengguna lebih memilih penyimpanan lokal yang dienkripsi sebagai opsi yang lebih solid dan terpercaya.

## Fungsi Utama
---

GnuPG memiliki beberapa fungsi utama, antara lain:
- [x] Enkripsi Data
- [x] Komunikasi yang Aman
- [x] Kontrol Akses
- [x] Tanda Tangan Digital
- [x] Verifikasi Tanda Tangan

## Encryption & Decryption
---

### Asymmetric & Symmetric
---

- **Asymmetric:** Menggunakan dua kunci yang berbeda, yaitu **Public Key** dan **Private Key**. Metode ini sering digunakan untuk komunikasi.
- **Symmetric:** Menggunakan kunci yang sama untuk proses enkripsi dan dekripsi, yaitu *passphrase* atau kata sandi. Metode ini sering digunakan untuk mengenkripsi file.

### Asymmetric
---

Metode ini sering digunakan untuk memastikan keamanan komunikasi antara pihak-pihak yang terlibat. Kunci publik dapat dibagikan secara bebas, sementara kunci privat harus dijaga kerahasiaannya. Dengan menggunakan kedua kunci ini, informasi dapat dienkripsi dan didekripsi dengan aman, sehingga melindungi data dari akses yang tidak sah.

#### Menghasilkan Kunci
---

Untuk membuat kunci baru, gunakan perintah berikut:

```bash
gpg --full-generate-key
```

Ikuti instruksi yang muncul di terminal untuk mengonfigurasi kunci.

#### Enkripsi
---

Untuk mengenkripsi file, buat file bernama `file.txt` dan ketikkan perintah berikut:

```bash
gpg -e -r <email> file.txt
```

> - `-e` atau `--encrypt`: Menunjukkan bahwa data akan dienkripsi.
- `-r` atau `--recipient`: Diikuti oleh identifikasi *public key* penerima.
{: .prompt-info}

Setelah proses enkripsi, file akan berganti nama menjadi `file.txt.gpg`.

#### Dekripsi
---

Untuk mendekripsi file, gunakan perintah berikut:

```bash
gpg -d file.txt.gpg
```

> `-d` atau `--decrypt`: Menunjukkan bahwa data akan didekripsi.
{: .prompt-info}

Untuk mendekripsi data ke dalam sebuah file, gunakan perintah berikut:

```bash
gpg -d file.txt.gpg > file.txt
```

Jika menggunakan *passphrase* saat pembuatan kunci, masukkan *passphrase* tersebut untuk mendekripsi file, dan format file akan kembali seperti semula menjadi `file.txt`.

### Ekspor Kunci
---

> Jangan pernah membocorkan kunci pribadi; kunci tersebut adalah aset eksklusif yang seharusnya hanya berada di tangan pengguna.
{: .prompt-danger}

#### Kunci Publik
---

- Melihat daftar kunci publik:
```bash
gpg --list-keys
```

- Menampilkan kunci publik dalam format ASCII:
```bash
gpg --armor --export <key_id>
```

- Menyimpan kunci publik ke sebuah file:
```bash
gpg --armor --export <key_id> > my_public_key.asc
```

#### Kunci Pribadi
---

- Melihat daftar kunci pribadi:
```bash
gpg --list-secret-keys
```

- Menampilkan kunci pribadi dalam format ASCII:
```bash
gpg --armor --export-secret-keys <key_id>
```

- Menyimpan kunci pribadi ke sebuah file:
```bash
gpg --armor --export-secret-keys <key_id> > my_private_key.asc
```

### Impor Kunci
---

Untuk mengimpor kunci publik, gunakan perintah berikut:

```bash
gpg --import public-key.asc
```

Verifikasi kunci dengan menggunakan perintah:

```bash
gpg --list-keys
```

### Mengirim Pesan
---

Pengguna dapat mengenkripsi pesan yang disimpan dalam file atau yang ditulis langsung di *command line*.

- Untuk mengenkripsi pesan dalam file teks (misalnya `.txt`), gunakan perintah berikut:
```bash
gpg --encrypt --recipient <key_id> pesan.txt
```

- Untuk mengetikkan pesan langsung, gunakan perintah berikut:
```bash
echo "Halo, ini adalah pesan rahasia" | gpg --encrypt --armor --recipient <key_id> > pesan.asc
```

### Menghapus Kunci
---

#### Kunci Pribadi
---

Kunci pribadi biasanya memiliki ID yang sama dengan kunci publik. Sebelum menghapus kunci publik, hapus terlebih dahulu kunci pribadi dengan perintah berikut:

```bash
gpg --delete-secret-key <key_id>
```

#### Kunci Publik

Kemudian, hapus kunci publik jika perlu:

```bash
gpg --delete-key <key_id>
```

## Symmetric
---

Metode ini umum digunakan untuk mengenkripsi file dan data, di mana keamanan informasi bergantung pada kerahasiaan kunci yang digunakan. Dalam kriptografi kunci simetris, baik pengirim maupun penerima harus memiliki akses ke kunci yang sama untuk dapat mengamankan dan mengakses informasi yang terenkripsi.

### Enkripsi
---

Untuk mengenkripsi file menggunakan metode *symmetric*, misalnya dengan folder bernama `data.tar`{: .filepath}, gunakan perintah berikut:

```bash
gpg -c data.tar
```

atau

```bash
gpg --symmetric data.tar
```

Setelah itu, pengguna akan diminta untuk memasukkan *passphrase*. Masukkan *passphrase* atau kata sandi yang kuat, yang akan digunakan untuk proses dekripsi nanti.

> Metode ini juga dapat digunakan untuk format `.zip` atau arsip lainnya.
{: .prompt-info}

### Dekripsi
---

Untuk mendekripsi file yang telah dienkripsi, gunakan perintah berikut:

```bash
gpg -d data.tar.gpg > data.tar
```

## Pranala Luar
---

- [Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)

## Referensi
---

- [ricalWiki: GNU Privacy Guard](https://ricalnet.github.io/ricalwiki.html)