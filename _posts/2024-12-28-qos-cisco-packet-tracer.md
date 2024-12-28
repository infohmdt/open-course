---
title: Konfigurasi QoS di Cisco Packet Tracer
description: 
categories: [Telecommunications]
tags: [cisco packet tracer]
author: rical
---

- ip pc0: 192.168.1.2, gateway 192.168.1.1
- ip pc1: 192.168.1.3, gateway 192.168.1.1
- ip server: 172.16.0.254, gateway 172.16.0.1

## konfigurasi r3

```
en
conf t
hostname rical
int g0/0
ip add 11.0.0.1 255.255.255.0
no sh
int g0/1
ip add 192.168.1.1 255.255.255.0
no sh
router ospf 10
network 11.0.0.0 0.255.255.255 area 0
network 192.168.1.0 0.255.255.255 area 0
write
```

## konfigurasi r4

```
en
conf t
hostname pascal
int g0/0
ip add 11.0.0.2 255.255.255.0
no sh
int g0/1
ip add 172.16.0.1 255.255.255.0
no sh
router ospf 10
network 11.0.0.0 0.255.255.255 area 0
network 172.16.0.0 0.0.0.255 area 0
write
```

## konfigurasi r2

```
conf t
class-map voice
match protocol rtp
class
ex
class-map httpmatch protocol http
ex
class-map icmp
match protocol icmp
ex
policy-map mark
class voice
set ip dscp ef
priority 100
ex
ex
policy-map mark
class http
set ip dscp af31
bandwidth 50
ex
class icmp
set ip dscp af11
int g0/0
service-policy output mark
write
```

## konfigurasi r3

```
en 
conf t
class-map voice
match ip dscp ef
ex
class-map http
match ip dscp af31
ex
class-map icmp
match ip dscp af11
ex
policy-map remark
class voice
set precedence critical
ex
class http
set precedence 3
class icmp
set precedence routine
int g0/0
service-policy input remark
write
```

## pengujian
- cek pc1, masuk ke web browser dan akses 172.16.0.254 
- lakukan ping ke 172.16.0.254