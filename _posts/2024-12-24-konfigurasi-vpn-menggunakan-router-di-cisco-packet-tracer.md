---
title: Konfigurasi VPN Menggunakan Router di Cisco Packet Tracer
description: Mempelajari cara mengonfigurasi dan menggunakan VPN pada router dan membuat tunnel VPN antara router untuk komunikasi yang aman.
categories: [Cybersecurity]
tags: [cybersecurity, cisco packet tracer]
author: rical
---

![VPN Configuration in Cisco Packet Tracer](/assets/img/posts/2024-12-24-konfigurasi-vpn-menggunakan-router-di-cisco-packet-tracer/vpn-configuration.png)

Sekarang, seperti yang terlihat, saya menggunakan tiga *router* untuk menunjukkan konfigurasi VPN pada *router*. Ini adalah contoh lab yang menunjukkan cara mengonfigurasi *VPN tunnel* menggunakan Cisco Packet Tracer.

> Total ada empat *network* yang digunakan di sini:
- Network 192.168.1.0/24
- Network 192.168.2.0/24
- Network 1.0.0.0/8
- Network 2.0.0.0/8
{: .prompt-info}

Langkah pertama yang akan dilakukan adalah memberikan alamat IP pada setiap antarmuka *router* dan juga memberikan alamat IP pada komputer yang digunakan di sini.

## R1 configuration
**Router>**`en`

**Router#**`conf t`

**Router(config)#**`host r1`

**r1(config)#**`int fa0/0`

**r1(config-if)#**`ip add 192.168.1.1 255.255.255.0` 

**r1(config-if)#**`no sh`

**r1(config-if)#**`ex`

**r1(config)#**`int fa0/1`

**r1(config-if)#**`ip add 1.0.0.1 255.0.0.0`

**r1(config-if)#**`no sh`

## R2 configuration
**Router>**`en`

**Router#**`conf t`

**Router(config)#**`host r2`

**r2(config)#**`int fa0/0`

**r2(config-if)#**`ip add 1.0.0.2 255.0.0.0`

**r2(config-if)#**`no shut`

**r2(config-if)#**`ex`

**r2(config)#**`int fa0/1`

**r2(config-if)#**`ip add 2.0.0.1 255.0.0.0`

**r2(config-if)#**`no shut`

## R3 configuration
**Router>**`en`

**Router#**`conf t`

**Router(config)#**`host r3`

**r3(config)#**`int fa0/0`

**r3(config-if)#**`ip add 2.0.0.2 255.0.0.0`

**r3(config-if)#**`no sh`

**r3(config-if)#**`ex`

**r3(config)#**`int fa0/1`

**r3(config-if)#**`ip add 192.168.2.1 255.255.255.0`

**r3(config-if)#**`no sh`

Sekarang saatnya untuk melakukan routing. Di sini, saya akan mengonfigurasi *routing default*.

## Konfigurasi Routing Default pada Router R1
**r1>**`en`

**r1#**`conf t`

> Masukkan perintah konfigurasi, satu per satu. Akhiri dengan menekan `ctr+z`.
{: .prompt-tip}

**r1(config)#**`ip route 0.0.0.0 0.0.0.0 1.0.0.2`

**r1#**

## Konfigurasi Routing Default pada Router R3
**r3>**`enable`

**r3#**`config t`

> Masukkan perintah konfigurasi, satu per satu. Akhiri dengan menekan `ctr+z`.
{: .prompt-tip}

**r3(config)#**`ip route 0.0.0.0 0.0.0.0 2.0.0.1`

**r3#**

Sekarang, mari kita periksa koneksi dengan melakukan `ping` satu sama lain.

Pertama, kita akan pergi ke *router* R1 dan melakukan `ping` ke *router* R3:

**r1#**`ping 2.0.0.2`

Keluarannya akan seperti ini:

>Type escape sequence to abort.<br>
Sending 5, 100-byte ICMP Echos to 2.0.0.2, timeout is 2 seconds:<br>
!!!!!<br>
Success rate is 100 percent (5/5), round-trip min/avg/max = 26/28/33 ms<br>

Sekarang, kita akan menuju ke *router* R3 dan menguji jaringan dengan melakukan `ping` ke antarmuka *router* R1.

**r3#**`ping 1.0.0.1`

Keluarannya akan seperti ini:

> Type escape sequence to abort.<br>
Sending 5, 100-byte ICMP Echos to 1.0.0.1, timeout is 2 seconds:<br>
!!!!!<br>
Success rate is 100 percent (5/5), round-trip min/avg/max = 25/28/32 ms<br>

Dapat dilihat dengan jelas bahwa kedua *router* berhasil saling melakukan `ping`.

## Membuat VPN Tunnel antara R1 dan R3
**r3#**`conf t`

**r3(config)#**`interface tunnel 100`

**r3(config-if)#**`ip add 172.16.1.2 255.255.0.0`

**r3(config-if)#**`tunnel source fa0/0`

**r3(config-if)#**`tunnel destination 1.0.0.1`

**r3(config-if)#**`no sh`

Sekarang, mari kita uji komunikasi antara kedua *router* ini lagi dengan melakukan `ping` satu sama lain:

**r1#**`ping 172.16.1.2`

Keluarannya akan seperti ini:

> Type escape sequence to abort.<br>
Sending 5, 100-byte ICMP Echos to 172.16.1.2, timeout is 2 seconds:<br>
!!!!!<br>
Success rate is 100 percent (5/5), round-trip min/avg/max = 30/32/36 ms<br>

**r1#**

 

**r3#**`ping 172.16.1.1`

Keluarannya akan seperti ini:

> Type escape sequence to abort.<br>
Sending 5, 100-byte ICMP Echos to 172.16.1.1, timeout is 2 seconds:<br>
!!!!!<br>
Success rate is 100 percent (5/5), round-trip min/avg/max = 33/45/83 ms<br>

Sekarang, lakukan *routing* untuk *VPN tunnel* yang telah dibuat pada kedua *router* R1 dan R3.

**r1(config)#**`ip route 192.168.2.0 255.255.255.0 172.16.1.2`

**r3(config)#**`ip route 192.168.1.0 255.255.255.0 172.16.1.1`

## Uji Konfigurasi VPN Tunnel
Sekarang, kita akan menuju ke *router* R1 dan menguji apakah *tunnel* telah berhasil dibuat atau tidak.

**r1#**`show interfaces Tunnel 10`

Keluarannya akan seperti ini:

> Tunnel10 is up, line protocol is up (connected)<br>
Hardware is Tunnel<br>
Internet address is 172.16.1.1/16<br>
MTU 17916 bytes, BW 100 Kbit/sec, DLY 50000 usec,<br>
reliability 255/255, txload 1/255, rxload 1/255<br>
Encapsulation TUNNEL, loopback not set<br>
Keepalive not set<br>
Tunnel source 1.0.0.1 (FastEthernet0/1), destination 2.0.0.2<br>
Tunnel protocol/transport GRE/IP<br>
Key disabled, sequencing disabled<br>
Checksumming of packets disabled<br>
Tunnel TTL 255<br>
Fast tunneling enabled<br>
Tunnel transport MTU 1476 bytes<br>
Tunnel transmit bandwidth 8000 (kbps)<br>
Tunnel receive bandwidth 8000 (kbps)<br>
Last input never, output never, output hang never<br>
Last clearing of "show interface" counters never<br>
Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 1<br>
Queueing strategy: fifo<br>
Output queue: 0/0 (size/max)<br>
5 minute input rate 32 bits/sec, 0 packets/sec<br>
5 minute output rate 32 bits/sec, 0 packets/sec<br>
52 packets input, 3508 bytes, 0 no buffer<br>
Received 0 broadcasts, 0 runts, 0 giants, 0 throttles<br>
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort<br>
0 input packets with dribble condition detected<br>
52 packets output, 3424 bytes, 0 underruns<br>
0 output errors, 0 collisions, 0 interface resets<br>
0 unknown protocol drops<br>
0 output buffer failures, 0 output buffers swapped out

Sekarang, kita akan menuju ke *router* R3 dan menguji pembuatan *VPN tunnel*.

**r3#**`show interface Tunnel 100`

> Tunnel100 is up, line protocol is up (connected)<br>
Hardware is Tunnel<br>
Internet address is 172.16.1.2/16<br>
MTU 17916 bytes, BW 100 Kbit/sec, DLY 50000 usec,<br>
reliability 255/255, txload 1/255, rxload 1/255<br>
Encapsulation TUNNEL, loopback not set<br>
Keepalive not set<br>
Tunnel source 2.0.0.2 (FastEthernet0/0), destination 1.0.0.1<br>
Tunnel protocol/transport GRE/IP<br>
Key disabled, sequencing disabled<br>
Checksumming of packets disabled<br>
Tunnel TTL 255<br>
Fast tunneling enabled<br>
Tunnel transport MTU 1476 bytes<br>
Tunnel transmit bandwidth 8000 (kbps)<br>
Tunnel receive bandwidth 8000 (kbps)<br>
Last input never, output never, output hang never<br>
Last clearing of "show interface" counters never<br>
Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 1<br>
Queueing strategy: fifo<br>
Output queue: 0/0 (size/max)<br>
5 minute input rate 32 bits/sec, 0 packets/sec<br>
5 minute output rate 32 bits/sec, 0 packets/sec<br>
52 packets input, 3424 bytes, 0 no buffer<br>
Received 0 broadcasts, 0 runts, 0 giants, 0 throttles<br>
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort<br>
0 input packets with dribble condition detected<br>
53 packets output, 3536 bytes, 0 underruns<br>
0 output errors, 0 collisions, 0 interface resets<br>
0 unknown protocol drops

## Melacak Jalur VPN Tunnel
Sekarang, jika ingin memeriksa jalur yang digunakan oleh *VPN tunnel*, cukup pergi ke salah satu komputer, misalnya PC, dan lakukan `ping` ke PC lain yang berada di jaringan yang berbeda. Kemudian, lacak jalurnya menggunakan perintah `tracert`. Hasilnya akan menunjukkan jalur yang diambil oleh *VPN tunnel* yang telah dibuat.

**PC>**`ipconfig`

Keluarannya kaan seperti ini:

> FastEthernet0 Connection:(default port)<br>
Link-local IPv6 Address.........: FE80::2E0:8FFF:FE0B:AEB2<br>
IP Address......................: 192.168.2.2<br>
Subnet Mask.....................: 255.255.255.0<br>
Default Gateway.................: 192.168.2.1

**PC>**`ping 192.168.1.2`

Keluarannya akan seperti ini:

> Pinging 192.168.1.2 with 32 bytes of data:<br>
Reply from 192.168.1.2: bytes=32 time=61ms TTL=126<br>
Reply from 192.168.1.2: bytes=32 time=55ms TTL=126<br>
Reply from 192.168.1.2: bytes=32 time=55ms TTL=126<br>
Reply from 192.168.1.2: bytes=32 time=57ms TTL=126<br>
Ping statistics for 192.168.1.2:<br>
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),<br>
Approximate round trip times in milli-seconds:<br>
Minimum = 55ms, Maximum = 61ms, Average = 57ms

**PC>**`tracert 192.168.1.2`

Keluarannya akan seperti ini:

> Tracing route to 192.168.1.2 over a maximum of 30 hops:<br>
1 3 ms 0 ms 18 ms 192.168.2.1<br>
2 35 ms 30 ms 30 ms 172.16.1.1<br>
3 65 ms 59 ms 60 ms 192.168.1.2<br>
Trace complete.

**PC>**

## Download file
Unduh file [di sini](/assets/posts/vpn-configuration.pkt).