# Redis Docker Application (Redis + RedisInsight) 🚀

Bu repo, Docker Compose ile tek komutla Redis ve RedisInsight (grafik arayüz) servislerini ayağa kaldırmak için hazırlanmış hafif bir başlangıç (boilerplate) projesidir.

---

## ✅ Özellikler

* Redis Port: **6379**
* RedisInsight UI: **5540**
* AOF Persistence aktif
* Docker named volume ile veri kalıcılığı

---

## 📌 İçerik

* Gereksinimler
* Hızlı Başlangıç
* Servisler ve Portlar
* RedisInsight ile Bağlanma
* Redis CLI ile Test
* Veri Kalıcılığı
* Yaygın Sorunlar

---

## Gereksinimler

* Docker
* Docker Compose (Docker Desktop ile birlikte gelir)

Kurulum kontrolü:

```bash
docker --version
docker compose version
```

> Not: Bazı sistemlerde `docker-compose` (tireli) komutu kullanılır. Yeni sürümlerde `docker compose` önerilir.

---

## 🚀 Hızlı Başlangıç

Repo:

```
https://github.com/Muhsindl/Redis_Application.git
```

### 1️⃣ Projeyi klonla

```bash
git clone https://github.com/Muhsindl/Redis_Application.git
cd Redis_Application
```

### 2️⃣ Servisleri başlat

```bash
docker compose up -d
```

Eski Compose sürümü için:

```bash
docker-compose up -d
```

### 3️⃣ Çalıştığını kontrol et

```bash
docker ps
```

---

## 🔌 Servisler ve Portlar

| Servis       | Container Name | Adres                                | Port |
| ------------ | -------------- | ------------------------------------ | ---- |
| Redis        | redis-service  | localhost                            | 6379 |
| RedisInsight | redis-insight  | [http://localhost](http://localhost) | 5540 |

---

## 🖥 RedisInsight ile Bağlanma

### 1️⃣ Tarayıcıdan aç:

```
http://localhost:5540
```

### 2️⃣ Add Database butonuna tıkla.

### 🔹 Docker ağı içinden (önerilen)

* Host: `redis-service`
* Port: `6379`

### 🔹 Host bilgisayardan (lokal uygulamalar için)

* Host: `localhost`
* Port: `6379`

---

## 💻 Redis CLI ile Test

Redis container içine gir:

```bash
docker exec -it redis-service redis-cli
```

Basit test:

```bash
SET mykey "Merhaba Redis!"
GET mykey
```

---

## 💾 Veri Kalıcılığı

Redis verileri Docker named volume kullanılarak saklanır:

* Volume adı: `redis-data`
* Container path: `/data`
* AOF (Append Only File) aktif

Volume'u görmek için:

```bash
docker volume ls
```

---

## ⚠ Yaygın Sorunlar

### 1️⃣ Port çakışması

Eğer makinede başka bir servis 6379 veya 5540 portunu kullanıyorsa container başlatılamaz.

Çözüm: `docker-compose.yml` içinde port mapping değiştirin:

```yaml
ports:
  - "6380:6379"
```

### 2️⃣ RedisInsight açılmıyor

Container loglarını kontrol et:

```bash
docker logs -f redis-insight
```

Tarayıcıdan doğru adrese gittiğinden emin ol:

```
http://localhost:5540
```

---

## 🛑 Servisleri Durdurma / Silme

Durdur:

```bash
docker compose down
```

Volume dahil her şeyi sil:

```bash
docker compose down -v
```

---

## 📦 Kullanılan Docker Image’ları

* Redis: `redis:7.2-alpine`
* RedisInsight: `redis/redisinsight:latest`
