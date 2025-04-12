# ✅ Final Testing & Validation – Starktower AI Build

This guide walks through final testing to verify that all major components of your offline AI assistant stack are working together properly.

---

## 📦 Stack Components

You should now have the following services installed and running:

| Component           | Description                                      |
|---------------------|--------------------------------------------------|
| Proxmox             | Host hypervisor (VM/LXC management)              |
| Docker CE           | Container runtime for AI services                |
| Ollama + Open WebUI | LLMs and frontend chat interface                 |
| Whisper             | Offline speech-to-text (STT)                     |
| Piper / Coqui       | Offline text-to-speech (TTS)                     |
| Wake Word Engine    | Porcupine or alternative trigger phrase handler  |
| Orchestrator Script | Ties voice activation to container startup       |
| Tailscale           | Secure remote access to your system              |

---

## 🧪 Step 1: Run Voice Assistant from Wake Word

If installed:

```bash
# Test wake-word pipeline manually
cd ~/starktower/orchestrator
python3 orchestrate_jarvis.py
```

Speak the trigger phrase (e.g., "Hey Jarvis"). You should observe:

- Whisper begins listening and transcribing
- Ollama processes the transcription as a prompt
- Piper speaks the generated response

---

## 🌐 Step 2: Test Access to Web Services

- Visit **Open WebUI**:  
  `http://<your-local-ip>:3000`

- SSH into Proxmox or LXC containers via **Tailscale IPs**

- Access Home Assistant UI (if integrated):  
  `http://<home-assistant-ip>:8123`

---

## 🧠 Step 3: Test LLM with Voice Prompt

Use your wake-word pipeline to:

1. Ask a factual question (e.g., "What is the capital of Japan?")
2. Test Home Assistant control (e.g., "Turn on the hallway light.")
3. Ask a follow-up to check conversation memory

Verify Whisper → Ollama → Piper executes correctly.

---

## 📋 Step 4: Validate Docker Stack

```bash
docker ps
```

Ensure all containers are:

- Running
- Responding to logs:  
  `docker logs <container-name>`

Restart test:

```bash
docker restart <container-name>
```

---

## 🔒 Step 5: Test Tailscale from External Network

- Disconnect from your home Wi-Fi
- Open Tailscale on your phone/laptop
- SSH into your orchestrator container using the Tailscale IP

Example:

```bash
ssh root@100.x.x.x
```

---

## ✅ Final Checklist

- [x] Wake word triggers pipeline
- [x] STT → LLM → TTS is working
- [x] Orchestrator auto-starts on boot (if configured)
- [x] Docker containers are healthy
- [x] Remote access is working via Tailscale

---

## 🧠 You now have a local, private Jarvis stack!

Everything is fully offline, LLM-based, and extensible with Home Assistant, MQTT, and other automations.

Continue building on this with:

- `nextcloud-integration.md` (dashboards + file sharing)
- `ha-automations.md` (home automation routines)

