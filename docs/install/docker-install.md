# 🐳 Docker Installation for Starktower AI Assistant

This guide sets up Docker CE on your Proxmox LXC or VM to prepare for containerized AI services like Ollama, Open WebUI, and Whisper.

---

## ✅ Step 1: Update & Install Dependencies

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release -y

---

## ✅ Step 2: Install Docker Engine

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

docker version
docker run hello-world
```

---

## ⚙️ Optional: Disable Docker Rootless (for LXC compatibility)

If you installed Docker inside an **LXC container** on Proxmox, rootless Docker may cause conflicts.

To disable rootless mode:

```bash
dockerd-rootless-setuptool.sh uninstall
```

---

## ✅ Docker is ready!

Next steps:
- Deploy Ollama or Open WebUI with Docker Compose
- Continue to `ollama-openwebui.md` for model setup
- Or install Portainer with `portainer.md` to manage containers from a GUI

