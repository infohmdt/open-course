---
title: Periferal Utama dalam Mikrokontroler (MCU)
description: GPIO, UART, PWM, ADC, Interupsi GPIO, dan Interupsi Timer
categories: [OS, Learning Materials]
tags: [microcontroller]
author: rical
---

Mikrokontroler (MCU) adalah sirkuit terintegrasi yang dirancang untuk mengontrol operasi perangkat elektronik. Periferal yang tertanam di dalamnya memungkinkan interaksi dengan dunia eksternal melalui antarmuka digital, analog, dan komunikasi. Artikel ini membahas enam komponen kritis dalam arsitektur MCU: [GPIO](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#1-gpio-general-purpose-inputoutput), [UART](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#2-uart-universal-asynchronous-receivertransmitter), [PWM](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#3-pwm-pulse-width-modulation), [ADC](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#4-adc-analog-to-digital-converter), [Interupsi GPIO](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#5-gpio-interrupt-interupsi-gpio), dan [Interupsi Timer](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#6-timer-interrupt-interupsi-timer), beserta prinsip kerja, aplikasi, dan implementasinya.

## 1. GPIO (General-Purpose Input/Output)  
### Overview  
GPIO adalah pin serbaguna pada MCU yang dapat dikonfigurasi sebagai input (masukan) atau output (keluaran). Pin ini tidak memiliki fungsi khusus bawaan, sehingga fleksibel untuk berbagai aplikasi. 

> Seperti saklar lampu di rumah: bisa menyalakan lampu (output) atau mendeteksi apakah pintu terbuka (input). 
{: .prompt-info}

### Fungsi dan Karakteristik  
- **Mode Input**: Mendeteksi sinyal eksternal (misal: logika tinggi/rendah).  
  - Contoh: Membaca status tombol, sensor digital (PIR, limit switch).  
- **Mode Output**: Mengirim sinyal ke perangkat eksternal.  
  - Contoh: Mengendalikan LED, relay, atau driver motor.  
- **Voltage Level**: Tergantung arsitektur MCU (umumnya 3.3V atau 5V).  
- **Pull-up/Pull-down Resistor**: Fitur internal untuk menstabilkan input saat tidak ada sinyal eksternal.  

### Aplikasi Khas  
- Antarmuka dengan sensor sederhana (tombol, saklar).  
- Kontrol aktuator (LED, buzzer).  

## 2. UART (Universal Asynchronous Receiver/Transmitter)  
### Overview  
UART adalah protokol komunikasi serial asinkron yang menggunakan dua jalur: [TX](https://en.wikipedia.org/wiki/Transmitter) (transmisi) dan [RX](https://en.wikipedia.org/wiki/Radio_receiver) (penerimaan). Data dikirim dalam bentuk frame tanpa sinyal clock eksternal.  

> Seperti dua orang berbicara bergantian lewat telepon, tanpa perlu waktu yang disinkronkan (asinkron).
{: .prompt-info}

### Prinsip Kerja 
- **Baud Rate**: Kecepatan transmisi (misal: 9600, 115200 bit per detik). Kedua perangkat harus memiliki baud rate yang sama.  
- **Frame Data**:  
  - **Start Bit**: Menandai awal transmisi (logika rendah).  
  - **Data Bits**: 5–9 bit data (biasanya 8 bit).  
  - **Parity Bit**: Opsional, untuk deteksi kesalahan.  
  - **Stop Bit**: Menandai akhir transmisi (logika tinggi).  

### Aplikasi Khas 
- Komunikasi antara MCU dan komputer via USB-to-UART (contoh: Arduino Uno).  
- Antarmuka dengan modul GPS, Bluetooth (HC-05), atau layar LCD. 

## 3. PWM (Pulse Width Modulation)  
### Overview  
PWM adalah teknik untuk menghasilkan sinyal analog dari sumber digital dengan memodulasi lebar pulsa.  

### Parameter Utama  
- **Duty Cycle**: Persentase waktu sinyal dalam keadaan aktif (ON) dalam satu periode.  
  - Contoh: Duty cycle 25% → ON 25% waktu, OFF 75%.  
- **Frekuensi**: Jumlah siklus per detik (Hz). Frekuensi tinggi mengurangi riak (ripple) pada beban analog.  

### Aplikasi Khas  
- Kontrol kecerahan LED atau kecepatan motor DC.  
- Generasi sinyal audio sederhana.  

## 4. ADC (Analog-to-Digital Converter) 
### Overview  
ADC mengubah sinyal analog (misal: tegangan) menjadi nilai digital yang dapat diproses oleh MCU.

> Seperti penggaris yang mengukur panjang dan menerjemahkannya ke angka.
{: .prompt-info}

### Karakteristik Teknis  
- **Resolusi**: Jumlah bit output (misal: 10-bit → 1024 nilai diskrit).  
- **Sampling Rate**: Kecepatan konversi (contoh: 100 kSps → 100.000 sampel per detik).  
- **Referensi Tegangan**: Rentang input analog (misal: 0–3.3V).  

### Aplikasi Khas  
- Pembacaan sensor analog (suhu LM35, potensiometer, sensor cahaya).  
- Sistem akuisisi data (pemantauan baterai, tegangan panel surya).  

## 5. GPIO Interrupt (Interupsi GPIO) 
### Overview  
Interupsi GPIO memungkinkan MCU merespons perubahan status pin secara instan, tanpa perlu polling (pengecekan berulang).  

> Seperti bel pintu—Anda bisa lanjut bekerja sampai bel berbunyi, baru menghampiri pintu.
{: .prompt-info}

### Jenis Trigger  
- **Rising Edge**: Terpicu saat sinyal naik dari rendah ke tinggi.  
- **Falling Edge**: Terpicu saat sinyal turun dari tinggi ke rendah.  
- **Level-sensitive**: Terpicu selama sinyal berada pada level tertentu.  

### Aplikasi Khas  
- Sistem wake-up dari mode sleep (misal: tombol daya).  
- Deteksi kejadian waktu nyata (sensor gerak, alarm).  

## 6. Timer Interrupt (Interupsi Timer)  
### Overview 
Interupsi Timer dipicu oleh pencapaian nilai tertentu pada timer internal MCU, memungkinkan eksekusi kode pada interval waktu yang presisi.  

> Seperti alarm yang berbunyi setiap jam untuk mengingatkan minum air.
{: .prompt-info}

### Komponen Timer  
- **Prescaler**: Pembagi frekuensi clock untuk mengatur kecepatan penghitungan.  
- **Counter Register**: Menyimpan nilai penghitungan saat ini.  
- **Auto-reload**: Fitur untuk mengatur ulang timer secara otomatis.  

### Aplikasi Khas 
- Multitasking sederhana (sistem operasi waktu nyata).  
- Pengendalian PID (Proportional-Integral-Derivative) untuk motor.  
- Pembangkitan delay presisi tanpa blokir eksekusi program utama.  

## Integrasi Periferal dalam Sistem MCU 
Periferal seperti GPIO, ADC, dan PWM sering diintegrasikan untuk membentuk sistem kompleks. Contoh:  
1. **Sistem Kontrol Motor**:  
   - ADC membaca posisi potensiometer (input analog).  
   - PWM mengatur kecepatan motor sesuai nilai ADC.  
   - Timer Interrupt memantau kecepatan setiap 100 ms.  
2. **Sistem Keamanan**:  
   - GPIO Interrupt mendeteksi pintu terbuka (falling edge).  
   - UART mengirim notifikasi ke server via modul Wi-Fi.  

## Pertimbangan Teknis
1. **GPIO**:  
   - Batasan arus (umumnya 20 mA per pin).  
   - Perlindungan ESD (Electrostatic Discharge) untuk input.  
2. **UART**:  
   - Perlindungan noise dengan resistor pull-up atau isolasi optik.  
   - Penggunaan protokol lapis tinggi (contoh: Modbus) untuk komunikasi industri.  
3. **PWM**:  
   - Efek frekuensi PWM pada beban induktif (motor) atau kapasitif (LED).  
4. **ADC**:  
   - Filter anti-aliasing untuk menghindari noise frekuensi tinggi.  
5. **Interupsi**:  
   - Prioritas interupsi untuk menghindari konflik sumber daya. 

## Ringkasan Analogi 
- [GPIO](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#1-gpio-general-purpose-inputoutput) = Tangan dan sensor sentuh (input/output).
- [UART](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#2-uart-universal-asynchronous-receivertransmitter) = Mulut dan telinga untuk berkomunikasi.
- [PWM](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#3-pwm-pulse-width-modulation) = Cara mengatur kekuatan pukulan tangan robot.
- [ADC](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#4-adc-analog-to-digital-converter) = Mata yang bisa melihat tingkat kecerahan cahaya.
- [GPIO INT](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#5-gpio-interrupt-interupsi-gpio) = Refleks cepat saat tangan menyentuh benda panas.
- [TMR INT](https://ricaldocs.github.io/posts/periferal-utama-dalam-mikrokontroler/#6-timer-interrupt-interupsi-timer) = Jam weker yang mengingatkan robot untuk beristirahat tiap 1 jam.


## Pranala Menarik
- [Komponen Sistem Operasi](https://ricaldocs.github.io/posts/komponen-sistem-operasi/)