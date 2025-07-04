---
title: Daftar Perintah Lengkap ADB dan Fastboot
description: Kumpulan perintah penting ADB dan Fastboot untuk pengembang Android!
categories: [OS, Android]
tags: [android]
author: rical
---

[Android Debug Bridge](https://en.wikipedia.org/wiki/Android_Debug_Bridge) (ADB) dan [Fastboot](https://en.wikipedia.org/wiki/Fastboot) merupakan alat baris perintah penting dalam ekosistem pengembangan Android. ADB berfungsi sebagai jembatan komunikasi antara komputer dan perangkat Android yang sedang berjalan, sedangkan Fastboot digunakan untuk memodifikasi sistem saat perangkat dalam mode bootloader.

## Perintah ADB (Android Debug Bridge)
### Manajemen Perangkat dan Koneksi

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb devices` | Menampilkan daftar perangkat terhubung | `-l`: Detail lengkap perangkat |
| `adb connect <host>[:<port>]` | Menghubungkan ke perangkat via TCP/IP | Port default: 5555 |
| `adb disconnect [<host>[:<port>]]` | Memutus koneksi jaringan | Tanpa argumen: putus semua |
| `adb kill-server` | Menghentikan server ADB | |
| `adb start-server` | Memulai server ADB | |
| `adb usb` | Beralih ke mode koneksi USB | |

### Manajemen Aplikasi

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb install [opsi] <path>` | Menginstal aplikasi | `-r`: Install ulang<br>`-d`: Izinkan downgrade<br>`-g`: Beri semua izin |
| `adb uninstall [opsi] <paket>` | Menghapus aplikasi | `-k`: Simpan data |
| `adb shell pm list packages [opsi]` | Daftar paket terinstal | `-f`: Tampilkan path<br>`-s`: Paket sistem<br>`-3`: Aplikasi pihak ketiga |
| `adb shell pm path <paket>` | Menampilkan lokasi APK | |
| `adb shell pm clear <paket>` | Menghapus data aplikasi | |
| `adb shell pm disable-user <paket>` | Menonaktifkan aplikasi | |
| `adb shell pm enable <paket>` | Mengaktifkan aplikasi | |

### Manajemen File

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb push <lokal> <remote>` | Mengirim file ke perangkat | |
| `adb pull [opsi] <remote> [<lokal>]` | Mengambil file dari perangkat | `-a`: Pertahankan metadata |
| `adb shell ls [opsi] <path>` | Daftar file/direktori | `-l`: Format panjang<br>`-a`: Tampilkan tersembunyi |
| `adb shell rm [opsi] <path>` | Menghapus file | `-r`: Rekursif |
| `adb shell mkdir [opsi] <path>` | Membuat direktori | `-p`: Buat direktori induk |
| `adb shell mv <sumber> <tujuan>` | Memindahkan/mengganti nama | |
| `adb shell cp [opsi] <sumber> <tujuan>` | Menyalin file | `-r`: Rekursif |

### Operasi Shell dan Sistem

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb shell` | Masuk ke shell interaktif | |
| `adb shell <command>` | Eksekusi perintah langsung | |
| `adb shell screencap <path>` | Tangkap layar | |
| `adb shell screenrecord [opsi] <path>` | Rekam layar | `--time-limit <n>`: Durasi<br>`--bit-rate <n>`: Kualitas |
| `adb reboot [target]` | Reboot perangkat | `recovery`<br>`bootloader`<br>`sideload` |
| `adb root` | Restart adbd dengan akses root | |
| `adb remount` | Remount partisi /system | |

### Logging dan Diagnostik

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb logcat [opsi]` | Tampilkan log sistem | `-v <format>`: Format output<br>`-s <tag>`: Filter tag<br>`-c`: Bersihkan log |
| `adb bugreport [opsi]` | Hasilkan laporan bug | `-z`: Kompresi ZIP |
| `adb shell dumpsys <service>` | Dump info layanan sistem | `battery`<br>`meminfo`<br>`package` |
| `adb shell dumpstate` | Dump status sistem | |
| `adb shell dmesg` | Tampilkan pesan kernel | |

### Operasi Lanjutan

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `adb backup [opsi] <paket>` | Backup data aplikasi | `-f <file>`: Nama file<br>`-apk`: Sertakan APK<br>`-shared`: Backup SD card |
| `adb restore <file>` | Restore data backup | |
| `adb forward <lokal> <remote>` | Forward port ke perangkat | |
| `adb reverse <remote> <lokal>` | Forward port ke PC | |
| `adb jdwp` | Daftar proses JDWP | |
| `adb sideload <file>` | Install paket via recovery | |

## Perintah Fastboot
### Manajemen Perangkat dan Informasi

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot devices` | Daftar perangkat terhubung | |
| `fastboot getvar <variabel>` | Tampilkan variabel bootloader | `all`: Semua variabel |
| `fastboot help` | Tampilkan bantuan | |
| `fastboot --version` | Tampilkan versi | |

### Operasi Boot dan Reboot

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot reboot` | Reboot ke sistem | |
| `fastboot reboot-bootloader` | Reboot ke bootloader | |
| `fastboot reboot recovery` | Reboot ke recovery | |
| `fastboot reboot fastboot` | Reboot ke fastbootd | |
| `fastboot boot <kernel>` | Boot sementara dari image | |

### Flashing Partisi

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot flash <partisi> <file>` | Flash image ke partisi | `boot`<br>`recovery`<br>`system` |
| `fastboot flash:raw <partisi> <kernel> [ <ramdisk> ]` | Flash kernel dan ramdisk | |
| `fastboot flashall` | Flash semua partisi | `-w`: Hapus data |
| `fastboot erase <partisi>` | Hapus partisi | |
| `fastboot format[:<fs_type>] <partisi>` | Format partisi | `ext4`<br>`f2fs` |
| `fastboot update <file.zip>` | Flash update ZIP | |

### Manajemen Bootloader

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot oem unlock` | Buka kunci bootloader | |
| `fastboot flashing unlock` | Buka kunci (alternatif) | |
| `fastboot oem lock` | Kunci bootloader | |
| `fastboot flashing lock` | Kunci bootloader (alternatif) | |
| `fastboot oem device-info` | Info status bootloader | |

### Manajemen Slot (Sistem A/B)

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot set_active <slot>` | Set slot aktif | `a` atau `b` |
| `fastboot getvar current-slot` | Tampilkan slot aktif | |
| `fastboot --set-active=<slot>` | Set slot aktif (opsi global) | |

### Perintah Tingkat Lanjut

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot continue` | Lanjutkan booting | |
| `fastboot oem <command>` | Perintah OEM spesifik | |
| `fastboot stage <file>` | Unggah file ke memori staging | |
| `fastboot get_staged <file>` | Unduh file dari memori staging | |
| `fastboot fetch <partisi> <file>` | Ambil partisi sebagai image | |
| `fastboot set_active <slot>` | Ubah slot partisi aktif | |

### Verifikasi dan Tanda Tangan

| Perintah | Deskripsi | Opsi/Penggunaan |
|----------|-----------|-----------------|
| `fastboot flash vbmeta <file>` | Flash image vbmeta | |
| `fastboot --disable-verity` | Nonaktifkan dm-verity | |
| `fastboot --disable-verification` | Nonaktifkan verifikasi vbmeta | |

## Tabel Referensi Variabel Fastboot

| Variabel | Deskripsi | Contoh Nilai |
|----------|-----------|--------------|
| `product` | Model perangkat | `walleye` |
| `version-bootloader` | Versi bootloader | `mwm2.0.3.0` |
| `secure` | Status keamanan | `yes` |
| `unlocked` | Status kunci bootloader | `yes` |
| `is-userspace` | Mode userspace | `no` |
| `current-slot` | Slot partisi aktif | `a` |
| `slot-suffixes` | Daftar slot | `a,b` |
| `serialno` | Nomor seri perangkat | `HT82F1A12345` |

## Catatan Penggunaan Penting
> Persyaratan: 
- ADB memerlukan pengaktifan USB Debugging di Opsi Developer
- Fastboot memerlukan akses [bootloader unlocking](https://en.wikipedia.org/wiki/Bootloader_unlocking)
- Driver USB spesifik perangkat harus terinstal
{: .prompt-info}

> Konvensi Penulisan:
- `<parameter>`: Nilai wajib diisi
- `[parameter]`: Nilai opsional
- `-opsi`: Opsi baris perintah
{: .prompt-tip}

> Keselamatan Operasi:
- Selalu pastikan baterai cukup (>50%) sebelum operasi flash
- Operasi flash yang salah dapat menyebabkan [brick](https://en.wikipedia.org/wiki/Brick_(electronics)) permanen
- Backup data penting sebelum modifikasi sistem
{: .prompt-warning}

## Pranala Menarik
- [Bypass Xiaomi Bootloader Restrictions](https://ricaldocs.github.io/posts/bypass-xiaomi-bootloader-restrictions/)
- [Android Tools & Fix](https://ricaldocs.github.io/posts/android-tools-and-fix/)
