---
title: Python Virtual Environment
description: Membuat lingkungan virtual di Python untuk mempermudah proses developments.
categories: [Linux]
tags: [linux, python, open source, android]
author: rical
---

> Sebelum melanjutkan ke langkah-langkah konfigurasi, pastikan bahwa <a href="https://www.python.org/" target="_blank">Python</a> telah diinstal.
{: .prompt-info }

Masukkan perintah berikut ke terminal untuk melihat versi Python:
```bash
python3 --version
```

## Instalasi venv
Gunakan perintah berikut untuk menginstall paket `venv`:

```bash
sudo apt install python3-venv
```

Buat folder, misalnya:

```bash
mkdir projects
```

Buat `venv` dengan menjalankan perintah:

```bash
python3 -m venv projects/
```

### Mengaktifkan venv

```bash
source projects/bin/activate
```
Setelah diaktfikan, prompt terminal akan menunjukkan nama *virtual environment* yang menandakan bahwa `venv` sudah siap digunakan.

### Mematikan venv

``` bash
deactivate
```

## Android venv
Unduh aplikasi [Termux](https://f-droid.org/en/packages/com.termux/) dan instal melalui pengelola file seperti biasanya.

Gunakan perintah berikut untuk memperbarui paket:
```bash
pkg update && pkg upgrade -y
```

Gunakan perintah berikut untuk memasang Python:
```bash
pkg install python && python --version
```

Gunakan perintah berikut untuk membuat `venv`:
```bash
python3 -m venv venv
```

Aktifkan `venv`:
```bash
source venv/bin/activate
```

Setelah diaktfikan, prompt terminal akan menunjukkan nama *virtual environment* yang menandakan bahwa `venv` sudah siap digunakan.

Terakhir, pasang modul dengan menggunakan perintah:
```bash
pip install nama_modul
```

## Referensi
- <a href="https://risnandapascal.github.io/ricalwiki.html" target="_blank">ricalWiki</a>





