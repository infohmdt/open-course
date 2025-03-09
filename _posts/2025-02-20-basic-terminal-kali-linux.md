---
title: Basic Terminal Kali Linux
description: Mempelajari dasar-dasar penggunaan terminal, serta perintah-perintah fundamental sistem operasi Linux.
categories: [Cybersecurity, Linux]
tags: [cybersecurity, linux]
author: rical
---

---

Kali Linux, sebagai distribusi sistem operasi berbasis Linux yang populer di kalangan profesional keamanan siber, dilengkapi dengan antarmuka pengguna grafis (*graphical user interface* atau GUI). Namun, terminal tetap menjadi komponen yang paling kuat dan esensial dalam sistem ini. Terdapat berbagai alat terminal yang perlu digunakan selama pengujian keamanan, sehingga penting bagi pengguna untuk mempelajari setidaknya dasar-dasar penggunaan terminal.

> Sebagai seorang Penetration Tester, berbagai perintah terminal sering digunakan dalam aktivitas sehari-hari. Postingan ini bertujuan untuk memperkenalkan penggunaan dasar terminal serta beberapa perintah fundamental yang akan sangat membantu dalam perjalanan karier sebagai Penetration Tester.
{: .prompt-info}

## Membuka Terminal di Kali Linux
---

Untuk memulai, pengguna perlu membuka jendela terminal dari desktop Kali Linux. Pengguna juga dapat menggunakan kombinasi tombol `CTRL+ALT+T` untuk membuka jendela terminal secara langsung dari keyboard.

## Dasar-dasar Penggunaan Terminal
---

Terminal memungkinkan pengguna untuk melakukan berbagai tugas berbasis teks. Pengguna dapat mengetikkan perintah dan menekan tombol Enter ⤶ untuk menjalankan perintah tersebut. Jika tampilan terminal menjadi tidak teratur, pengguna dapat membersihkannya dengan menggunakan perintah `clear` atau dengan menekan `CTRL+L`. Untuk membuka jendela terminal baru dari sesi terminal yang sedang aktif, pengguna dapat menggunakan kombinasi `CTRL+SHIFT+T`.

### Penyelesaian Perintah dan Nama File
---

Untuk menyelesaikan perintah atau nama file di terminal, pengguna dapat menekan tombol `TAB`. Jika terdapat beberapa file dengan awalan nama yang sama, setiap kali tombol `TAB` ditekan, terminal akan menampilkan semua opsi yang tersedia. Sebagai contoh, jika terdapat dua file dengan awalan nama yang sama, yaitu `test.sh` dan `test.txt` di direktori `/home`{: .filepath}, pengguna akan melihat kedua opsi tersebut saat menekan tombol `TAB`:

```
┌──(kali㉿kali)-[~]
└─$ cat test.
Completing file
test.sh test.txt
```

### Menghentikan dan Menutup Terminal
---

Jika pengguna menjalankan sebuah perintah dan perlu menghentikan eksekusinya, kombinasi tombol `CTRL+C` dapat digunakan. Untuk menutup jendela terminal, pengguna dapat menggunakan kombinasi tombol `CTRL+D` atau menjalankan perintah `exit`.

### Mematikan dan Merestart Sistem
---

Pengguna juga dapat mematikan dan merestart sistem melalui jendela terminal. Untuk mematikan sistem, perintah `poweroff` digunakan, sedangkan untuk merestart, perintah `reboot` dengan hak akses root diperlukan.

### Melihat Riwayat Perintah
---

Untuk memeriksa perintah-perintah yang baru saja digunakan di terminal, pengguna dapat menggunakan perintah `history`. Selain itu, untuk menggunakan perintah yang telah digunakan sebelumnya, pengguna dapat menekan `CTRL+R` dan mengetikkan sebagian dari perintah tersebut; terminal akan menyarankan perintah yang relevan. Contoh tampilan perintah `history` adalah sebagai berikut:

```
┌──(kali㉿kali)-[~]
└─$ history
bck-i-search: his_
```

## Pengalihan Output di Terminal
---

Dalam sistem Linux, termasuk Kali Linux, terdapat banyak pengalihan (*redirection*) yang perlu dipahami. Sebagai contoh, untuk menyimpan output dari perintah daftar file (`ls`) ke dalam sebuah file teks (`.txt`), pengguna dapat menjalankan perintah berikut:

```bash
ls > ls-list.txt
```

Output dari perintah tersebut dapat dilihat:

```
┌──(kali㉿kali)-[~]
└─$ cat ls-list.txt
Desktop
Documents
Downloads
ls-list.txt
Music
Pictures
Public
rical_net
Templates
Videos
```

Dengan menggunakan perintah di atas, output dari perintah `ls` disimpan ke dalam file teks dengan nama `ls-list.txt`. Pengalihan output dilakukan dengan menggunakan karakter `>`.

Sebaliknya, pengguna juga dapat mencetak isi file teks ke dalam jendela terminal dengan menggunakan karakter `<`:

```bash
cat < ls-list.txt
```

### Penggunaan Command Pipe
---

Pengalihan lain yang penting untuk diketahui adalah penggunaan *command pipe*. Dengan menggunakan karakter `|`, pengguna dapat menggabungkan output dari setiap perintah dan menggunakannya sebagai input untuk perintah berikutnya. Contoh penggunaannya adalah sebagai berikut:

```
command 1 | command 2 | command 3
```

Sebagai contoh, jika pengguna ingin membaca sebuah file, mengurutkan hasilnya, dan menggunakan perintah `grep` untuk memfilter beberapa string teks, perintah yang dapat digunakan adalah:

```
cat ls-list.txt | sort | grep test
```

Output dari perintah tersebut dapat dilihat:

```
┌──(kali㉿kali)-[~]
└─$ cat ls-list.txt | sort | grep test
decrypted-test.pdf
pentestlab
speedtest-cli
testbackdoor.php
test.sh
testshell.php
test.txt
```

## Perintah Dasar Linux
---

### 1. `ls`
---

**Deskripsi**: Perintah `ls` digunakan untuk menampilkan daftar file dan direktori dalam direktori saat ini.

**Sintaks**:
```bash
ls [opsi] [file...]
```

**Opsi Umum**:
- `-l`: Menampilkan informasi detail tentang file, termasuk izin, pemilik, ukuran, dan tanggal modifikasi.
- `-a`: Menampilkan semua file, termasuk file tersembunyi yang diawali dengan titik (`.`).
- `-h`: Menampilkan ukuran file dalam format yang lebih mudah dibaca (misalnya, KB, MB).

**Contoh**:
```bash
ls -la
```
Perintah ini akan menampilkan semua file dan direktori, termasuk yang tersembunyi, dalam format daftar yang panjang.

### 2. `cd`
---

**Deskripsi**: Perintah `cd` (*change directory*) digunakan untuk berpindah antara direktori dalam sistem file.

**Sintaks**:
```bash
cd [direktori]
```

**Contoh**:
```bash
cd /home/user/Documents
```
Perintah ini akan memindahkan pengguna ke direktori `Documents`{: .filepath} di dalam direktori `user`{: .filepath}.

### 3. `cp`
---

**Deskripsi**: Perintah `cp` digunakan untuk menyalin file dan direktori.

**Sintaks**:
```bash
cp [opsi] sumber tujuan
```

**Opsi Umum**:
- `-r`: Menyalin direktori secara rekursif.
- `-i`: Meminta konfirmasi sebelum menimpa file yang ada.

**Contoh**:
```bash
cp -r /source/directory /destination/directory
```
Perintah ini akan menyalin direktori dari lokasi sumber ke lokasi tujuan.

### 4. `mv`
---

**Deskripsi**: Perintah `mv` digunakan untuk memindahkan atau mengubah nama file dan direktori.

**Sintaks**:
```bash
mv [opsi] sumber tujuan
```

**Contoh**:
```bash
mv oldname.txt newname.txt
```
Perintah ini akan mengubah nama file `oldname.txt` menjadi `newname.txt`.

### 5. `rm`
---

**Deskripsi**: Perintah `rm` digunakan untuk menghapus file dan direktori.

**Sintaks**:
```bash
rm [opsi] file...
```

**Opsi Umum**:
- `-r`: Menghapus direktori secara rekursif.
- `-f`: Menghapus file tanpa meminta konfirmasi.

**Contoh**:
```bash
rm -rf /path/to/directory
```
Perintah ini akan menghapus direktori dan semua isinya tanpa konfirmasi.

### 6. `mkdir`
---

**Deskripsi**: Perintah `mkdir` digunakan untuk membuat direktori baru.

**Sintaks**:
```bash
mkdir [opsi] direktori...
```

**Opsi Umum**:
- `-p`: Membuat direktori induk jika belum ada.

**Contoh**:
```bash
mkdir -p /path/to/new/directory
```
Perintah ini akan membuat direktori baru, termasuk direktori induknya jika diperlukan.

### 7. `chmod`
---

**Deskripsi**: Perintah [chmod](https://ricaldocs.github.io/posts/chmod/) digunakan untuk mengubah izin akses file dan direktori.

---

Perintah-perintah di atas merupakan dasar dari penggunaan sistem operasi Linux. Pengguna dapat mengkombinasikan berbagai opsi untuk memenuhi kebutuhan spesifik dalam pengelolaan file dan direktori. Untuk informasi lebih lanjut, pengguna disarankan untuk merujuk pada manual sistem dengan menggunakan perintah `man [perintah]`.