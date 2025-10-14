# 🐳 Docker Compose Development Templates

Kumpulan template `docker-compose` untuk lingkungan pengembangan lintas bahasa (PHP, Python, Node.js).
Setiap service berjalan dalam mode `network_mode: host` agar port lokal host langsung bisa diakses dari container.
Direktori kerja otomatis di-*mount* dari folder saat ini (`.`) agar perubahan file langsung terlihat.

---

## 📦 1. PHP Development

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

---

## 🐍 2. Python Development

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

---

## 🟩 3. Node.js Development

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

---

## ⚙️ Cara Menggunakan

1. **Salin salah satu blok di atas** ke file `docker-compose-dev.yml` dalam proyekmu.
2. Jalankan container sesuai kebutuhan:

   ```bash
   docker-compose -f docker-compose-dev.yml up -d
   ```
3. Masuk ke dalam container:

   ```bash
   docker exec -it php-dev bash
   ```

   *(Ganti `php-dev` sesuai nama container yang kamu gunakan.)*

---

## 💡 Tips

* Tambahkan lebih banyak service sesuai kebutuhan (misalnya `mysql`, `redis`, `nginx`, dll).
* Gunakan `.env` file untuk menyimpan variabel environment umum.
* Jika ingin menjaga port host agar tidak konflik, hapus `network_mode: host` dan gunakan port mapping manual, misalnya:

  ```yaml
  ports:
    - "8080:80"
  ```

---
