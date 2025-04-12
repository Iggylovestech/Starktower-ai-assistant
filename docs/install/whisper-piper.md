# 🎤 Whisper + Piper Voice Pipeline Setup (Starktower AI)

This guide sets up OpenAI Whisper.cpp for **speech-to-text (STT)** and Piper for **text-to-speech (TTS)** inside Docker containers — the core of your voice interaction system.

---

## ✅ Prerequisites

Ensure Docker CE is installed and running. Ideally, you’ve already deployed `ollama-openwebui.md`.

---

## 🧱 Step 1: Create Voice Stack Directory

```bash
mkdir -p ~/starktower/voice
cd ~/starktower/voice
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
  whisper:
    image: ghcr.io/ggerganov/whisper.cpp:latest
    container_name: whisper
    volumes:
      - ./audio:/data
    command: ["--model", "base.en", "--file", "/data/input.wav"]
    restart: unless-stopped

  piper:
    image: rhasspy/piper
    container_name: piper
    ports:
      - "10200:10200"
    volumes:
      - ./piper:/data
    command: >
      --model en_US-lessac-medium
    restart: unless-stopped
```

Save and exit.

---

## 🎛 Step 3: Launch Voice Services

```bash
docker compose up -d
```

---

## 🔊 Step 4: Test TTS Output

Send text to Piper via HTTP POST:

```bash
curl -X POST http://localhost:10200/api/tts \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello, I am your assistant."}' --output output.wav
```

Play it with:

```bash
aplay output.wav
```

---

## 🧠 Step 5: Whisper STT (Command Line Use)

Place a WAV file in the `audio/` folder as `input.wav`. Then run:

```bash
docker restart whisper
```

Check logs for output:

```bash
docker logs whisper
```

---

## 🧪 Optional: Customize Models

- **Whisper Models:** tiny, base, small, medium, large
- **Piper Voices:** download from [Piper GitHub](https://github.com/rhasspy/piper#prebuilt-voices)

---

## ✅ Voice Stack Ready

- Whisper = microphone to text  
- Piper = text to voice  
- Integrate next with `home-assistant.md` or `jarvis-control.md` for full automation!

---
