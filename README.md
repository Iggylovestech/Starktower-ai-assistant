# Starktower AI Assistant

A fully offline, modular AI assistant stack for local language model inference, voice interaction, and home automation — built on a Proxmox-powered Dell R730.

---

## 🔧 System Overview

This project includes:

- Proxmox virtualization (VM + LXC containers)
- Docker deployment of Ollama, Open WebUI, Whisper.cpp, Piper, Coqui
- Wake-word → STT → LLM → TTS pipeline
- Voice assistant integration with Home Assistant
- Secure remote access via Tailscale
- Optional Pi-hole + Unbound DNS stack

---

## 🧱 Modular Build Paths

Choose your build level:

| Level        | Description                                      |
|--------------|--------------------------------------------------|
| Basic        | Proxmox + Docker + Ollama + Open WebUI           |
| Intermediate | Adds STT/TTS pipeline, Tailscale, Portainer      |
| Expert       | Full Jarvis-style voice control, HA integration |

Each path is documented under `/docs/install/`

---

## 📊 Project Ratings

| Category   | Score | Notes                                                   |
|------------|-------|---------------------------------------------------------|
| Difficulty | 9.5   | Multi-layered networking, STT/TTS, Docker-in-LXC       |
| Coolness   | 10    | Fully local, no cloud, Iron-Man-core-for-your-house     |
| Uniqueness | 9.5   | Voice + LLM + Home Assistant, CPU-only, offline-ready  |

Full breakdown: [`docs/overview/starktower-project-ratings.md`](./docs/overview/starktower-project-ratings.md)

---

## 📁 Docs Structure

- `/docs/install/`: Setup guides
- `/docs/overview/`: Project ratings, summary
- `/docs/troubleshooting/`: Common issues + ChatGPT prompts

---

## ✅ Status

- [x] Tested on Dell R730 Proxmox 7.4+
- [x] Works without GPU
- [x] Fully local with Tailscale access
- [x] Home Assistant integration ready

---

## 🧠 Next Steps

- Add automation triggers via MQTT
- Add dashboards via Nextcloud
- Build command chaining into WebUI
