# 🐳 Podman & Docker Compose Development Templates

Kumpulan template **Docker Compose**, **Docker Run**, dan **Podman Run** untuk lingkungan pengembangan lintas bahasa (PHP, Python, Node.js).
Setiap container berjalan dengan `network_mode: host` agar port lokal host langsung dapat diakses dari container.
Direktori kerja otomatis di-*mount* dari folder saat ini (`.`) agar perubahan file langsung terlihat.

---

## 📦 1. PHP Development

### 🧩 docker-compose

```yaml
services:
  php-dev:
    image: shinsenter/php:8.2
    container_name: php-dev
    environment:
      APP_USER: root
      APP_GROUP: root
      APP_UID: 0
      APP_GID: 0
    volumes:
      - .:/var/www/html:z
    command: bash
    network_mode: host
    tty: true
```

### 🐋 docker run

```bash
docker run -it --rm \
  --name php-dev \
  -e APP_USER=root \
  -e APP_GROUP=root \
  -e APP_UID=0 \
  -e APP_GID=0 \
  -v "$(pwd)":/var/www/html:z \
  --network host \
  shinsenter/php:8.2 bash
```

### 🫧 podman run

```bash
podman run -it --rm \
  --name php-dev \
  -e APP_USER=root \
  -e APP_GROUP=root \
  -e APP_UID=0 \
  -e APP_GID=0 \
  -v "$(pwd)":/var/www/html:z \
  --network host \
  shinsenter/php:8.2 bash
```

---

## 🐍 2. Python Development

### 🧩 docker-compose

```yaml
services:
  python-dev:
    image: python:3.12-slim
    container_name: python-dev
    working_dir: /app
    volumes:
      - .:/app:z
    command: bash
    network_mode: host
    tty: true
```

### 🐋 docker run

```bash
docker run -it --rm \
  --name python-dev \
  -v "$(pwd)":/app:z \
  -w /app \
  --network host \
  python:3.12-slim bash
```

### 🫧 podman run

```bash
podman run -it --rm \
  --name python-dev \
  -v "$(pwd)":/app:z \
  -w /app \
  --network host \
  python:3.12-slim bash
```

---

## 🟩 3. Node.js Development

### 🧩 docker-compose

```yaml
services:
  node-dev:
    image: node:22-slim
    container_name: node-dev
    working_dir: /app
    volumes:
      - .:/app:z
    command: bash
    network_mode: host
    tty: true
```

### 🐋 docker run

```bash
docker run -it --rm \
  --name node-dev \
  -v "$(pwd)":/app:z \
  -w /app \
  --network host \
  node:22-slim bash
```

### 🫧 podman run

```bash
podman run -it --rm \
  --name node-dev \
  -v "$(pwd)":/app:z \
  -w /app \
  --network host \
  node:22-slim bash
```

---

## ⚙️ Cara Menggunakan

### 🧠 Menggunakan Compose

Jalankan salah satu file berikut sesuai kebutuhan:

```bash
# Podman
podman compose -f docker-compose-dev.yml up -d
podman exec -it php-dev bash

# Docker
docker compose -f docker-compose-dev.yml up -d
docker exec -it php-dev bash
```

*(Ganti `php-dev` sesuai service yang kamu gunakan, misal `python-dev` atau `node-dev`.)*

---

## 💡 Tips

* Tambahkan service tambahan seperti `mysql`, `redis`, atau `nginx` sesuai kebutuhan proyek.
* Gunakan `.env` file untuk menyimpan variabel environment umum.
* Jika tidak ingin menggunakan `network_mode: host`, ubah ke port mapping manual:

  ```yaml
  ports:
    - "8080:80"
  ```
* Untuk menghentikan container:

  ```bash
  docker stop php-dev
  # atau
  podman stop php-dev
  ```

---
