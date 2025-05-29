---
title: Docker Command Reference
description: Docker adalah platform open-source untuk mengembangkan, mengirimkan, dan menjalankan aplikasi dalam wadah terisolasi. 
categories: [Cloud Computing]
tags: [cloud, docker]
author: rical
---

## 1. Manajemen Kontainer

```docker
docker run -d --name nama_container -p host_port:container_port -v host_dir:container_dir image:tag
```

Jalankan container baru dengan opsi: 
- `-d`: detach (background) 
- `--name`: nama custom
- `-p`: port mapping 
- `-v`: volume binding

Perintah-perintah untuk mengontrol siklus hidup kontainer:

| Perintah | Deskripsi |
|----------|-----------|
| `docker start nama_container` | Mulai container yang berhenti |
| `docker stop nama_container` | Hentikan container dengan graceful shutdown |
| `docker restart nama_container` | Restart container |
| `docker rm nama_container` | Hapus container yang berhenti |
| `docker rm -f nama_container` | Paksa hapus container (termasuk yang berjalan) |
| `docker ps` | Lihat container yang sedang berjalan |
| `docker ps -a` | Lihat semua container (termasuk yang berhenti) |
| `docker logs nama_container` | Tampilkan log container |
| `docker logs -f nama_container` | Pantau log secara real-time |

## 2. Manajemen Image
Operasi untuk mengelola image Docker:

| Perintah | Deskripsi |
|----------|-----------|
| `docker pull nama_image:tag` | Download image dari Docker Hub |
| `docker build -t nama_image:tag .` | Build image dari Dockerfile |
| `docker images` | Lihat semua image lokal |
| `docker rmi nama_image:tag` | Hapus image lokal |
| `docker push username/nama_image:tag` | Upload image ke Docker Hub |

## 3. Operasi dalam Kontainer
Interaksi langsung dengan lingkungan kontainer:

| Perintah | Deskripsi |
|----------|-----------|
| `docker exec -it nama_container bash` | Akses shell di dalam container <br>(ganti `bash` dengan `sh` jika perlu) |
| `docker cp nama_container:/path/file /host/dir` | Salin file dari container ke host |
| `docker cp /host/file nama_container:/path` | Salin file dari host ke container |

## 4. Manajemen Jaringan
Konfigurasi konektivitas antar kontainer:

| Perintah | Deskripsi |
|----------|-----------|
| `docker network ls` | Lihat daftar jaringan |
| `docker network create nama_jaringan` | Buat jaringan baru |
| `docker run --network=nama_jaringan ...` | Jalankan container di jaringan tertentu |

## 5. Manajemen Volume
Pengelolaan penyimpanan persisten:

| Perintah | Deskripsi |
|----------|-----------|
| `docker volume create nama_volume` | Buat volume baru |
| `docker volume ls` | Lihat daftar volume |
| `docker run -v nama_volume:/dir ...` | Gunakan volume di container |
| `docker volume rm <volume_name>` | Menghapus volume |

## 6. Operasi Sistem
Perintah administratif dan pemeliharaan:

| Perintah | Deskripsi |
|----------|-----------|
| `docker system prune` | Hapus semua: <br>- Container berhenti <br>- Jaringan tidak terpakai <br>- Build cache |
| `docker system prune -a` | Hapus seluruh data tidak terpakai (termasuk image!) |
| `docker stats` | Pantau resource usage (CPU/Mem) |
| `docker info` | Tampilkan info sistem Docker |

## 7. Docker Compose (Opsional)
Untuk aplikasi multi-kontainer:

```bash
docker-compose up -d      # Menjalankan layanan
docker-compose down       # Menghentikan dan menghapus
docker-compose logs -f    # Melihat log terintegrasi
```

## Contoh Perintah Kompleks
```bash
docker run -d \
  --name myapp \
  -p 8080:80 \
  -v /data/app:/var/www/html \
  -e DB_HOST=database \
  --network my_network \
  --restart unless-stopped \
  nginx:latest
```

> - Jalankan container Nginx di background
- Port mapping `8080 (host) → 80 (container)`
- Mount volume lokal `/data/app` ke `/var/www/html`
- Set environment variable `DB_HOST`
- Sambungkan ke jaringan `my_network`
- Restart otomatis kecuali di-stop manual
{: .prompt-info}

> 1. Gunakan `docker-compose` untuk aplikasi multi-container ([contoh file](https://docs.docker.com/compose/compose-file/)).
2. Untuk otentikasi Docker Hub:
   ```bash
   docker login
   ```
3. Lihat dokumentasi lengkap: [https://docs.docker.com/engine/reference/commandline/docker/](https://docs.docker.com/engine/reference/commandline/docker/)
{: .prompt-tip}

## Pranala Menarik
- [Docker on AWS](https://ricaldocs.github.io/posts/docker-on-aws/)
- [Docker Compose](https://ricaldocs.github.io/posts/docker-compose/)