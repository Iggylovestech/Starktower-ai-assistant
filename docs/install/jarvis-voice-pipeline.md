# 🗣️ Jarvis-Style Voice Assistant Pipeline (Offline, Local)

This guide sets up a **local voice assistant** on Proxmox using:
- Wake word detection (`porcupine` or custom)
- Whisper STT (speech-to-text)
- Ollama LLM (local reasoning)
- Coqui or Piper TTS (text-to-speech)

All running in containers or LXCs with Docker Compose orchestration.

---

## ✅ Prerequisites

- Docker installed
- `ollama-openwebui.md` already completed
- Whisper + Piper already tested individually
- Optional: Python 3.10+ and `venv` (for orchestration script)

---

## 📦 Directory Structure

```bash
~/starktower/
├── voice/
│   ├── docker-compose.yml   # whisper + piper
│   └── wakeword/            # porcupine or whisper.cpp keyword
├── ollama/                  # docker-compose.yml with open-webui
├── scripts/
│   └── voice_pipeline.py    # Orchestrates everything
```

---

## 🧠 Step 1: Clone Voice Orchestration Script

```bash
mkdir -p ~/starktower/scripts
cd ~/starktower/scripts

curl -O https://raw.githubusercontent.com/Iggylovestech/starktower-ai-assistant/main/scripts/voice_pipeline.py
```

(You can also paste the script manually from your GitHub repo.)

---

## 📥 Step 2: Install Python Dependencies (LXC)

If you're using Python outside Docker (recommended for orchestration):

```bash
sudo apt install python3-pyaudio portaudio19-dev python3-venv -y
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Sample `requirements.txt`:

```txt
whispercpp
ollama
pyttsx3
sounddevice
porcupine
```

---

## 🛎 Step 3: Set Up Wake Word Listener

Example (using Porcupine):

```bash
python3 wakeword.py --keyword jarvis
```

Or Whisper keyword detection (lower RAM):

```bash
python3 wakeword_whisper.py
```

---

## 🔁 Step 4: Run the Full Pipeline

Once wakeword is triggered:

1. Record mic input (5s–15s)
2. Send audio to Whisper
3. Transcribe → forward to Ollama
4. Receive LLM response
5. TTS via Piper → play audio

Launch script:

```bash
python3 voice_pipeline.py
```

---

## 🧪 Testing

- Say “Jarvis” (or your chosen keyword)
- Speak prompt (e.g. “What’s the weather tomorrow?”)
- Listen for TTS reply

---

## 🔐 Bonus: Secure with Tailscale

- Add `tailscale.md` for remote debugging
- Use SSH + Tailscale to monitor logs and restart services

---

## ✅ Voice AI Ready

You now have a **private offline voice assistant** running on Proxmox:

- Wake word + STT + LLM + TTS
- No OpenAI API, no cloud access required
- Fully modular: swap models, wakewords, voices

---

Next steps:
- Add to crontab or systemd for boot auto-launch
- Integrate with `home-assistant.md` for home automation
- Add a GUI dashboard (`flask`, `streamlit`, or `open-webui` command tab)
