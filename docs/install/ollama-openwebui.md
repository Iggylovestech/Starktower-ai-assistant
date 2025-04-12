# 🧠 Ollama + Open WebUI Setup (Starktower AI)

This guide deploys a full local AI stack using **Ollama** for model inference and **Open WebUI** as the chat frontend — running in Docker Compose.

---

## ✅ Prerequisites

Make sure Docker CE is already installed. If not, follow `docker-install.md` first.

---

## 🧱 Step 1: Create Deployment Directory

```bash
mkdir -p ~/starktower/ollama-webui
cd ~/starktower/ollama-webui
```

---

## 📝 Step 2: Create `docker-compose.yml`

```bash
nano docker-compose.yml
```

Paste the following:

```yaml
version: "3.9"
services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    ports:
      - "11434:11434"
    volumes:
      - ./ollama:/root/.ollama
    restart: unless-stopped

  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: open-webui
    ports:
      - "3000:3000"
    environment:
      - OLLAMA_BASE_URL=http://ollama:11434
    volumes:
      - ./webui:/app/backend/data
    depends_on:
      - ollama
    restart: unless-stopped
```

Save and exit the editor.

---

## 🚀 Step 3: Launch the Stack

```bash
docker compose up -d
```

Check containers:

```bash
docker ps
```

You should see both `ollama` and `open-webui` running.

---

## 🌐 Step 4: Access the Interface

Open a browser and go to:

```
http://<your-server-ip>:3000
```

You’ll see the Open WebUI chat interface. The first user to log in becomes the admin.

---

## 🧠 Step 5: Pull a Local LLM

Example (Tiny model):

```bash
ollama run tinyllama
```

Other popular models:
- `llama2`
- `mistral`
- `codellama`
- `gemma`
- `phi`

You can run this from your host or the container:

```bash
docker exec -it ollama ollama run mistral
```

---

## ✅ Done!

- Web UI: [http://your-server:3000](http://your-server:3000)  
- API: [http://your-server:11434](http://your-server:11434)

To install more models or test STT/TTS features, continue to:

- `whisper-piper.md` *(coming next)*
- `portainer.md` *(for GUI management)*

---
