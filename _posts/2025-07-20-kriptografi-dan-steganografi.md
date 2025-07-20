---
title: Kriptografi dan Steganografi
description: Implementasi dasar kriptografi (encoding, hashing, enkripsi) dan steganografi menggunakan perintah Linux seperti Base64, MD5, AES-256-CBC, dan Steghide.
categories: [Cybersecurity, Linux, Privacy]
tags: [cybersecurity, cryptography, linux, privacy]
author: rical
---

## Pendahuluan  
Kriptografi adalah ilmu dan seni mengamankan informasi melalui teknik penyandian (*encoding*, *hashing*, dan enkripsi). Dokumen ini menjelaskan tiga konsep utama:  
1. [Encoding](https://ricaldocs.github.io/posts/kriptografi-dan-steganografi/#1-encoding): Konversi data ke format lain yang dapat dikembalikan (*reversible*).  
2. [Hashing vs. Enkripsi](https://ricaldocs.github.io/posts/kriptografi-dan-steganografi/#2-hashing-vs-enkripsi): Perbedaan antara fungsi satu arah (*one-way*) dan dua arah (*two-way*).  
3. [Steganografi](https://ricaldocs.github.io/posts/kriptografi-dan-steganografi/#2-hashing-vs-enkripsi): Penyembunyian data dalam media digital (contoh: gambar).  

## 1. Encoding  
[Encoding](https://en.wikipedia.org/wiki/Character_encoding) mengubah data ke format spesifik menggunakan skema terstandarisasi, memungkinkan konversi balik ke bentuk asli tanpa kehilangan informasi.  

### Contoh Metode
#### Caesar Cipher
Caesar Cipher adalah metode enkripsi klasik yang menggantikan setiap huruf dalam teks asli (plaintext) dengan huruf lain dalam alfabet yang diposisikan sejauh nilai shift tertentu (misal +3), bersifat reversibel dan hanya menggeser karakter tanpa mengubah struktur teks. Diciptakan oleh Julius Caesar untuk komunikasi militer Romawi (~100 SM), menjadi fondasi kriptografi modern.  
- Contoh pergeseran 3 karakter: 

   | Karakter Asli | A | B | C | D | E | F | G | H | I |  
   |---------------|---|---|---|---|---|---|---|---|  
   | Hasil Shift   | D | E | F | G | H | I | J | K | L | 

   1. Enkripsi (Shift +3):  
      ```bash
      echo "TEXT_ASLI" | tr 'A-Za-z' 'D-ZA-Cd-za-c'
      ```
      
      Contoh:
      ```bash
      echo "cipher" | tr 'A-Za-z' 'D-ZA-Cd-za-c'
      # Output: flskhu
      ```

   2. Dekripsi (Shift -3):  
      ```bash
      echo "TEXT_ENKRIPSI" | tr 'D-ZA-Cd-za-c' 'A-Za-z'
      ```
      
      Contoh:  
      ```bash
      echo "flskhu" | tr 'D-ZA-Cd-za-c' 'A-Za-z'
      # Output: cipher
      ```

   3. Diagram Pergeseran (Shift +3):  
    
      | **Asli**  | A | B | C | D | E | F | ... | X | Y | Z |  
      |-----------|---|---|---|---|---|---|-----|---|---|---|  
      | **Hasil** | D | E | F | G | H | I | ... | A | B | C |  

   > 
   - Hanya memengaruhi huruf (A-Z/a-z).  
   - Karakter lain (angka, simbol) tetap tidak berubah.  
   - Shift ≥26 akan berperilaku modular (contoh: Shift +27 ≡ Shift +1). 
   {: .prompt-info}

#### Base64 (Linux)  
Base64 adalah skema encoding biner-ke-teks yang mengubah data biner (seperti file gambar atau biner) menjadi format teks ASCII menggunakan 64 karakter dasar (A-Z, a-z, 0-9, +, /), memungkinkan transmisi aman melalui sistem yang hanya mendukung teks. 
- Perintah:  
    1. Encoding:
    ```bash
    echo "encoding" | base64  # Output: ZW5jb2RpbmcK
    ```

    2. Decoding:
    ```bash
    echo "ZW5jb2RpbmcK" | base64 -d  # Output: encoding
    ```

## 2. Hashing vs. Enkripsi  

![Hashing vs. Enkripsi](/assets/img/posts/2025-07-20-kriptografi-dan-steganografi/hashing_vs_encryption.png)
_Hashing vs. Enkripsi_

### a. Hashing (One-Way)  
Proses mengubah plaintext menjadi nilai hash unik (hashtext) yang **tidak dapat dikembalikan** ke bentuk asli. Digunakan untuk verifikasi integritas data.  

- Contoh MD5:  
  ```bash
  echo "teks" | md5sum  # Output: c71448894eaaadb0217e6d4e92b44ef7
  ```  
  
  > MD5 dianggap tidak aman untuk keperluan kriptografi modern karena kerentanan terhadap tabrakan hash (*collision attacks*).
  {: .prompt-info}

### b. Enkripsi (Two-Way)  
Proses mengubah plaintext menjadi teks terenkripsi (ciphertext) menggunakan kunci, dan **dapat dikembalikan** ke bentuk asli dengan kunci dekripsi.  

- Contoh OpenSSL AES-256-CBC:  
  1. Enkripsi
  ```bash
  echo "teks" | openssl aes-256-cbc -a -pass pass:changeme -pbkdf2
  # Output: U2FsdGVkX188ZcetEtbc5uRwnzPC0XyXccmRWxoWWYc=
  ```

  2. Dekripsi
  ```bash
  echo "U2FsdGVkX188ZcetEtbc5uRwnzPC0XyXccmRWxoWWYc=" | openssl aes-256-cbc -d -a -pass pass:changeme -pbkdf2
  # Output: teks
  ```  

  > Parameter Kunci:  
  - `-a`: Encode/decode Base64 setelah enkripsi/dekripsi.  
  - `-d`: Mode dekripsi.  
  - `-pass pass:<password>`: Menentukan kata sandi untuk derivasi kunci.  
  - `-pbkdf2`: Menggunakan *Password-Based Key Derivation Function 2* (meningkatkan keamanan dengan iterasi salt).
  {: .prompt-info}  

## 3. Steganografi 
Steganografi (dari bahasa Yunani: steganos "tersembunyi" + graphein "menulis") adalah praktik penyembunyian informasi di dalam medium digital lain (seperti gambar, audio, video, atau berkas teks) untuk menyamarkan eksistensi pesan rahasia. Berbeda dengan kriptografi yang mengacak konten pesan, steganografi memfokuskan diri pada penyembunyian keberadaan komunikasi itu sendiri, sehingga tidak menarik perhatian pihak ketiga. Teknik ini memanfaatkan sifat redundansi data dalam medium pembawa (cover medium) untuk menyisipkan bit-bit pesan tanpa mengubah penampakan signifikan dari medium tersebut. 

[Steghide](https://www.kali.org/tools/steghide/) adalah perangkat lunak steganografi sumber terbuka (open-source) berlisensi GPL, dirancang untuk menyembunyikan data digital di dalam berkas gambar (format JPEG, BMP) atau audio (format WAV, AU). Menggunakan algoritma compression dan enkripsi opsional berbasis passphrase, Steghide memastikan:
 
### a. Instalasi Steghide
```bash
sudo apt update && sudo apt install -y steghide
```  

### b. Persiapkan File
- Buat file teks (`touch pesan-rahasia.txt`) berisi teks sembunyi.
- Siapkan gambar berformat JPG/JPEG (`gambar.jpg`).  

### c. Sisipkan Pesan
```bash
steghide embed -cf gambar.jpg -ef pesan-rahasia.txt
```  
>
- Pengguna akan diminta memasukkan passphrase.  
- File output (`gambar.jpg`) kini berisi data tersembunyi.  
{: .prompt-info}

### d. Ekstrak Pesan
```bash
steghide extract -sf gambar.jpg -xf pesan-ekstrak.txt
```  
>
- Passphrase sama harus dimasukkan untuk dekripsi.  
- Pesan asli tersimpan di `pesan-ekstrak.txt`.  
{: .prompt-info}

### e. Verifikasi
Bandingkan isi `pesan-rahasia.txt` dan `pesan-ekstrak.txt` untuk memastikan integritas.  

## Pranala Luar
- [Quantum Hasher](https://ricalnet.github.io/apps/QuantumHasher/index.html)

## Pranala Menarik
- [GNU Privacy Guard](https://ricaldocs.github.io/posts/gnu-privacy-guard/)