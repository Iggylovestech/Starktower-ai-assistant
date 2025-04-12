# 🧠 Automation + Wake Word Orchestration (Starktower AI)

This guide wires together your voice assistant pipeline with automation triggers, startup behaviors, and wake-word orchestration logic.

All components run locally on Proxmox inside LXC containers or Docker Compose stacks.

---

## ✅ Prerequisites

- Docker + `ollama-openwebui.md` stack already running
- `jarvis-voice-pipeline.md` already tested
- Python 3.10+ installed on the orchestrator container
- Optional: Home Assistant, MQTT broker

---

## 🗂️ Step 1: Clone Orchestrator Scripts

Create a folder to hold your orchestration logic:

```bash
mkdir -p ~/starktower/orchestrator
cd ~/starktower/orchestrator
```

Clone or manually create the orchestration Python script:

```bash
touch orchestrate_jarvis.py
nano orchestrate_jarvis.py
```

Paste a basic orchestration flow (placeholder — replace with real logic later):

```python
import os
import subprocess

# Wake word detected (placeholder trigger)
def on_wake_word():
    print("Wake word detected. Starting voice pipeline...")

    # Run Whisper + Ollama + Piper stack
    subprocess.run(["docker", "exec", "whisper", "start-whisper.sh"])
    subprocess.run(["docker", "exec", "ollama", "start-model.sh"])
    subprocess.run(["docker", "exec", "piper", "start-piper.sh"])

# Simulate wake word trigger
on_wake_word()
```

---

## 🧠 Step 2: Enable Auto-Start with Systemd (Optional)

If you're running the orchestrator in an LXC container, create a systemd service:

```bash
sudo nano /etc/systemd/system/jarvis-orchestrator.service
```

```ini
[Unit]
Description=Start Starktower AI Orchestrator
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/python3 /root/starktower/orchestrator/orchestrate_jarvis.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and start the service:

```bash
sudo systemctl enable jarvis-orchestrator
sudo systemctl start jarvis-orchestrator
```

---

## 🗣️ Optional: MQTT/Home Assistant Automation Hooks

If using MQTT, install the Paho MQTT client:

```bash
pip install paho-mqtt
```

Add hooks to publish voice events to Home Assistant:

```python
import paho.mqtt.client as mqtt

mqtt_client = mqtt.Client()
mqtt_client.connect("mqtt.local", 1883, 60)
mqtt_client.publish("jarvis/trigger", "wakeword-detected")
```

---

## 🧪 Testing Tips

- Manually run the script and verify container orchestration
- Use `docker ps` to monitor running services
- Tail logs for each container using `docker logs <container>`

---

## ✅ Voice orchestration is live!

Jarvis-style voice activation is now wired to your AI stack, ready to handle custom triggers or automated routines.
