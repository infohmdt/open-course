---
title: DNS List for Security & Privacy
description: Daftar DNS yang dapat digunakan untuk meningkatkan keamanan dan privasi, serta mengakses situs-situs yang diblokir.
categories: [Cybersecurity, Privacy]
tags: [privacy, android]
author: rical
---

## 1. Cloudflare
---

###  Cloudflare - Desktop
---

| IPv4                            | IPv6       				   |
| :--------------------- | :---------------------------- |
| 1.1.1.1                       | 2606:4700:4700::1111 |
| 1.0.0.1 			| 2606:4700:4700::1001 |

### Cloudflare - Android
---

Cari pengaturan DNS (biasanya bernama `Private DNS` atau `DNS Pribadi`) dan masukkan informasi berikut:
```
security.cloudflare-dns.com
```

## 2. Quad9
---

### Quad9 - Desktop
---

| IPv4                            | IPv6              |
| :--------------------- | :----------- - |
| 9.9.9.9                      	| 2620:fe::fe |
| 149.112.112.112 | 2620:fe::9  |

### Quad9 - Android
---

Cari pengaturan DNS (biasanya bernama `Private DNS` atau `DNS Pribadi`) dan masukkan informasi berikut:
```
dns.quad9.net
```

## 3. OpenDNS
---

| IPv4                         | IPv6                          |
| :------------------- | :-------------------- |
| 208.67.222.222 | 2620:119:35::35 |
| 208.67.220.220 | 2620:119:53::53 |

## 4. AdGuard
---

### AdGuard - Desktop
---

| IPv4                         | IPv6                          |
| :------------------- | :-------------------- |
| 94.140.14.14      | 2a10:50c0:8000::1 |
| 94.140.15.15      | 2a10:50c0:8001::1 |

### AdGuard - Android 
---

Cari pengaturan DNS (biasanya bernama `Private DNS` atau `DNS Pribadi`) dan masukkan informasi berikut:
```
dns.adguard.com
```

## 5. NextDNS
---

### NextDNS - Desktop
---

| IPv4                         | IPv6                                 |
| :------------------- | :------------------------ |
| 45.90.28.0           | 2a07:a8c0::e2:4ddc |
| 45.90.30.0           | 2a07:a8c1::e2:4ddc |

### NextDNS - Android 
---

Cari pengaturan DNS (biasanya bernama `Private DNS` atau `DNS Pribadi`) dan masukkan informasi berikut:
```
e24ddc.dns.nextdns.io
```

## 6. Google Public DNS
---

### Google Public DNS - Desktop
---

| IPv4                | IPv6                                        |
| :-------------- | :---------------------------- |
| 8.8.8.8           | 2001:4860:4860::8888 |
| 8.8.4.4           | 2001:4860:4860::8844 |

### Google Public DNS - Android 
Cari pengaturan DNS (biasanya bernama `Private DNS` atau `DNS Pribadi`) dan masukkan informasi berikut:
```
dns.google.com
```

## 7. LibreDNS (Recommended)
---

The `noads` service is a solution for blocking advertisements and trackers. 

| Endpoint                             | Description                   |
| :------------------------------      | :---------------------------- |
| `https://doh.libredns.gr/dns-query` <br> `https://doh.libredns.gr/noads`  | DNS over HTTPS  |
| `dot.libredns.gr` <br> `noads.libredns.gr`                    | DNS over TLS  |

> 1. **DNS over HTTPS (DoH)**: It is optimally configured and utilized within applications, particularly web browsers.
2. **DNS over TLS (DoT)**: It is best configured at the operating system level.
{: .prompt-info}

## Pranala Menarik
---

- [Privacy Is Not A Crime](https://ricaldocs.github.io/posts/privacy-is-not-a-crime/)

## Pranala Luar
---

- [Cloudflare Docs](https://developers.cloudflare.com/1.1.1.1/setup/)
- [quad9](https://quad9.net/)
- [OpenDNS](https://www.opendns.com/setupguide/)
- [AdGuard](https://adguard.com/kb/)
- [NextDNS](https://my.nextdns.io/e24ddc/setup)
- [Google Public DNS](https://developers.google.com/speed/public-dns)
- [LibreDNS](https://libredns.gr/)

## Referensi
---

- [ricalWiki: DNS List for Security and Privacy](https://ricalnet.github.io/ricalwiki.html)

