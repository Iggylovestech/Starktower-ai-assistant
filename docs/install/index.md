# 📦 Starktower AI Build — Install Guide Index

Welcome to the modular install path for the **Starktower AI Assistant** project.  
Below is the recommended setup sequence, from core virtualization to final testing.

---

## 🧰 Core System Setup

1. [`proxmox-setup.md`](./proxmox-setup.md)  
   Install and configure Proxmox VE on your Dell R730 or equivalent hardware.

2. [`docker-install.md`](./docker-install.md)  
   Set up Docker CE in a VM or LXC container for containerized services.

3. [`portainer-setup.md`](./portainer-setup.md) *(optional)*  
   Install Portainer to manage your Docker environment with a web GUI.

---

## 🧠 AI Assistant Core Stack

4. [`ollama-openwebui.md`](./ollama-openwebui.md)  
   Deploy Ollama (LLM inference) + Open WebUI for local AI chat.

5. [`whisper-piper.md`](./whisper-piper.md)  
   Install Whisper.cpp (STT) and Coqui or Piper (TTS) for voice I/O.

6. [`jarvis-voice-pipeline.md`](./jarvis-voice-pipeline.md)  
   Combine wake word, STT, LLM, and TTS into a full Jarvis-style assistant.

---

## 🧠 Automation & Integration

7. [`tailscale-access.md`](./tailscale-access.md)  
   Securely access your server and containers remotely using Tailscale.

8. [`nextcloud-integration.md`](./nextcloud-integration.md) *(optional)*  
   Set up personal cloud storage for files, photos, and media sharing.

9. [`ha-automations.md`](./ha-automations.md) *(optional)*  
   Integrate your voice assistant with Home Assistant automations.

10. [`automation-orchestration.md`](./automation-orchestration.md)  
    Orchestrate AI + HA startup and shutdown using scripts or schedulers.

---

## 🔒 Backups & Final Testing

11. [`snapshot-backups.md`](./snapshot-backups.md)  
    Set up Proxmox snapshots and external backup routines.

12. [`final-testing.md`](./final-testing.md)  
    Verify your install: network, containers, remote access, automation, voice control.

---

> ⚙️ For project overview, visit the root [`README.md`](../../README.md)  
> ✍️ For the creator’s personal journey, see [GitHub Profile »](https://github.com/iggylovestech)

---

Built on a Dell PowerEdge R730 • 2x Xeon E5-2690 v4 • 128GB RAM • Tailscale-secured • Offline AI-ready
