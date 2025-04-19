# 🚀 Self-Hosted Nextcloud Stack

This repository contains a `docker-compose.yml` setup to run a **Nextcloud** instance backed by **MariaDB**, **Redis**, and exposed securely via **Cloudflared** (Cloudflare Tunnel).

---

## 🧱 Services

### 1. MariaDB

- **Image:** `mariadb:10.6`
- Acts as the database for Nextcloud.
- Environment variables define rootless access, database name, and user credentials.
- Data is persisted to: `/home/elucri/nextcloud/db`.

### 2. Redis

- **Image:** `redis:alpine`
- Provides caching and memory locking to speed up Nextcloud.
- Data is persisted to: `/home/elucri/nextcloud/redis`.

### 3. Nextcloud

- **Image:** `nextcloud`
- The main web application.
- Depends on both MariaDB and Redis.
- Exposes port: `52006`.
- Data and configuration are stored in:
  - `/home/elucri/nextcloud/app/html`
  - `/home/elucri/nextcloud/app/custom_apps`
  - `/home/elucri/nextcloud/app/config`
  - `/home/elucri/nextcloud/app/data`

### 4. Cloudflared

- **Image:** `cloudflare/cloudflared:latest`
- Tunnels traffic securely from Cloudflare to your Nextcloud instance.
- Requires a `.env` file containing a valid `CLOUDFLARED_TOKEN`.

---

## 🛠️ Prerequisites

- Docker & Docker Compose installed.
- Cloudflare account with a configured Tunnel and token.
- Ensure all necessary volumes and directories exist:

```bash
mkdir -p /home/elucri/nextcloud/{db,redis,app/html,app/custom_apps,app/config,app/data}
``` 
