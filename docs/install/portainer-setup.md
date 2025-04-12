# 🧭 Portainer Setup for Docker Management

This guide adds **Portainer CE** to your Starktower AI stack — a web-based GUI to manage Docker containers, images, volumes, and networks.

---

## ✅ Prerequisites

- Docker CE already installed  
- Optional but recommended: `docker compose` installed and functional

---

## 🧱 Step 1: Create a Management Directory

```bash
mkdir -p ~/starktower/portainer
cd ~/starktower/portainer
```

---

## 📝 Step 2: Create `docker-compose.yml`

```bash
nano docker-compose.yml
```

Paste the following:

```yaml
version: '3.3'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    ports:
      - "9443:9443"
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

Save and exit.

---

## 🚀 Step 3: Deploy Portainer

```bash
docker compose up -d
```

---

## 🌐 Step 4: Access Web Interface

- Open browser to:  
  `https://<your-local-ip>:9443` (secure)  
  or  
  `http://<your-local-ip>:9000` (non-SSL)

- On first login, set your admin password.

---

## 🛡 Optional: Use Tailscale to Access Remotely

If Tailscale is installed on the host, you can access Portainer with the Tailscale IP:

```
https://100.x.x.x:9443
```

---

## ✅ Portainer is Ready

You can now:

- Manage running containers
- Launch new stacks via Docker Compose
- Monitor logs and resource usage
- Use GUI instead of CLI for deployment tasks

---

Next Steps:

- Use Portainer to verify `whisper`, `piper`, and `open-webui` are running
- Deploy `home-assistant.md` to enable home automation integration
