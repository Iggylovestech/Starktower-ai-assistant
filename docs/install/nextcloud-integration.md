# 🧩 Nextcloud Integration (Optional Dashboards + File Access)

This guide adds a local file-sharing and dashboarding layer to your Starktower stack using **Nextcloud**, giving you a private hub for files, dashboards, notes, and browser-accessible controls.

---

## 📋 Prerequisites

- Docker installed (`docker-install.md`)
- Basic Starktower services running (Open WebUI, Whisper, etc.)
- Tailscale installed (optional, for remote access)
- Optional: Home Assistant integration (for smart home dashboards)

---

## 🐳 Step 1: Deploy Nextcloud with Docker Compose

```bash
mkdir -p ~/starktower/nextcloud
cd ~/starktower/nextcloud
```

Create `docker-compose.yml`:

```yaml
version: '3.7'

services:
  nextcloud:
    image: nextcloud
    container_name: nextcloud
    ports:
      - 8080:80
    volumes:
      - ./nextcloud:/var/www/html
    restart: unless-stopped
```

Then deploy it:

```bash
docker compose up -d
```

---

## 🌐 Step 2: Access the Web UI

Visit `http://<your-local-ip>:8080`

- Create your **Nextcloud admin account**
- Follow setup instructions
- You can now upload files, create folders, and install dashboard apps (via the “Apps” section)

---

## 📂 Step 3: Create Project Dashboard

- Install the **Dashboard** app (under Apps → Office & Text)
- Create a new dashboard (e.g., “Jarvis Control”)
- Add widgets like:
  - Quick notes
  - Calendar sync
  - Links to:
    - Open WebUI
    - Home Assistant
    - Uptime Kuma (if installed)
    - Jarvis orchestrator launch page (if served via Flask or similar)

---

## 🔐 Step 4: Secure with Tailscale or Reverse Proxy

If you're using **Tailscale**, you're already protected.

Otherwise, you can optionally add **Caddy** or **NGINX** with TLS.

---

## 🚀 Optional Extensions

- **Nextcloud Talk** for internal video chat
- **Notes** app to store prompts, commands, or HA routines
- **WebDAV** integration with your phone or desktop for easy file sync

---

## ✅ Success

You now have a self-hosted cloud interface to interact with Starktower modules, access voice prompt logs, upload scripts, and build internal dashboards.

Next steps:

- `ha-automations.md` (Home Assistant routines)
- `snapshot-backups.md` (for offline rollbacks)
