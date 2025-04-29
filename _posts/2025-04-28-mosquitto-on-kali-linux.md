---
title: Mosquitto on Debian-based Linux
description: Melaksanakan protokol MQTT pada sistem operasi berbasis Debian dan memanfaatkannya.
categories: [Internet of Things]
tags: [IoT, microcontroller]
author: rical
---

Mosquitto adalah broker pesan yang ringan dan open-source yang menggunakan protokol MQTT (Message Queuing Telemetry Transport). Protokol ini dirancang untuk komunikasi mesin-ke-mesin (M2M) dan [Internet of Things](https://ricaldocs.github.io/categories/internet-of-things/) (IoT).

## Instalasi Mosquitto
```bash
sudo apt update && sudo apt install -y mosquitto mosquitto-clients
```

## Menjalankan Server Mosquitto
Setelah instalasi selesai, pengguna dapat menjalankan server Mosquitto dengan menggunakan perintah berikut:
```bash
mosquitto_sub -h test.mosquitto.org -t ricalnet
```

Perintah ini melakukan langganan (subscribe) ke topik `ricalnet` pada broker Mosquitto yang dihosting di `test.mosquitto.org`. Setelah perintah ini dijalankan, server akan menunggu dan menampilkan pesan yang diterima pada topik tersebut.

## Mengirim Pesan 
Untuk mengirim pesan ke topik yang sama, pengguna dapat menggunakan perintah berikut:
```bash
mosquitto_pub -h test.mosquitto.org -t ricalnet -m "Hello Friend"
```

Perintah ini mengirimkan pesan "Hello Friend" ke topik `ricalnet` pada broker yang sama.

## Contoh Output
Setelah menjalankan perintah untuk berlangganan dan mengirim pesan, output yang diharapkan di terminal adalah sebagai berikut:
```
┌──(titor㉿system)-[~]
└─$ mosquitto_sub -h test.mosquitto.org -t ricalnet

Hello Friend
Hello Friend
Hello Friend
```

Output menunjukkan bahwa pesan "Hello Friend" berhasil diterima beberapa kali, yang menunjukkan bahwa klien berlangganan berhasil menerima pesan yang dikirim ke topik `ricalnet`.

## Wokwi
[Wokwi](https://wokwi.com) adalah platform yang memungkinkan pengguna untuk merancang dan menguji proyek berbasis mikrokontroler secara online. Salah satu fitur utama dari [Wokwi](https://wokwi.com) adalah kemampuannya untuk mensimulasikan perangkat keras dan mengintegrasikan berbagai pustaka perangkat lunak untuk memfasilitasi pengembangan aplikasi IoT ([Internet of Things](https://ricaldocs.github.io/categories/internet-of-things/)).

![Pengujian](assets/img/posts/2025-04-28-mosquitto-on-kali-linux/wokwi-mqtt-test.png)
    _MQTT - Wokwi test_

### Contoh Kode Sumber
Berikut adalah contoh kode sumber yang menggunakan pustaka `WiFi` dan `PubSubClient` untuk menghubungkan perangkat ESP32 ke jaringan WiFi dan menerbitkan pesan ke broker MQTT.

```c++
#include <WiFi.h>
#include <PubSubClient.h>

const char* ssid = "Wokwi-GUEST";
const char* password = "";
const char* mqtt_server = "test.mosquitto.org"; 
const char* mqtt_topic = "ricalnet"; 

WiFiClient espClient;
PubSubClient client(espClient);

const int MSG_BUFFER_SIZE = 50;
char msg[MSG_BUFFER_SIZE]; 
int value = 1;

void setup() {
    Serial.begin(115200);
    WiFi.begin(ssid, password);
    
    while (WiFi.status() != WL_CONNECTED) {
        delay(1000);
        Serial.println("Connecting to WiFi...");
    }
    Serial.println("Connected to WiFi");

    client.setServer(mqtt_server, 1883);
}

void loop() {
    if (!client.connected()) {
        // Kode untuk menghubungkan kembali ke MQTT jika terputus
        // Misalnya, client.connect("clientID");
    }
    client.loop();

    snprintf(msg, MSG_BUFFER_SIZE, "Nomor Absen #%1d", value);
    Serial.print("Publish message: ");
    Serial.println(msg);
    client.publish(mqtt_topic, msg);
    
    delay(2000); 
}
```

### Diagram Konfigurasi
Berikut adalah representasi konfigurasi perangkat dalam format JSON yang digunakan dalam Wokwi:
```json
{
  "version": 1,
  "author": "Anonymous maker",
  "editor": "wokwi",
  "parts": [ { "id": "esp", "type": "board-esp32-devkit-c-v4" } ],
  "connections": [ [ "esp:TX", "$serialMonitor:RX", "" ], [ "esp:RX", "$serialMonitor:TX", "" ] ]
}
```

### Library Manager
Wokwi mendukung berbagai pustaka yang dapat digunakan dalam proyek pengembangan. Berikut adalah beberapa pustaka yang umum digunakan:
```
# Wokwi Library List
# See https://docs.wokwi.com/guides/libraries

PubSubClient
DHT sensor library for ESPx
WiFi
```