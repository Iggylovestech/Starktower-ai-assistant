# 🏠 Home Assistant Automations for Starktower AI

This guide connects your voice assistant pipeline to **Home Assistant** to trigger automations via voice — such as toggling lights, adjusting temperature, or running routines.

All automations are executed locally, without relying on cloud APIs.

---

## 📋 Prerequisites

- Home Assistant running (as a VM, container, or on a Pi)
- Whisper STT + Ollama + TTS stack working (see `jarvis-voice-pipeline.md`)
- MQTT broker available (optional but recommended)
- Tailscale installed (optional, for remote control)

---

## 🧠 Concept Overview

Your voice assistant stack will:

1. Wake on trigger phrase
2. Capture your spoken intent (e.g., “Turn on the living room lights”)
3. Transcribe using Whisper
4. Forward the prompt to Ollama
5. Ollama returns a structured command like:
   ```json
   {"action": "turn_on", "device": "living_room_lights"}
   ```
6. A script or MQTT client relays this command to Home Assistant

---

## 🔧 Step 1: Enable Long-Lived Access Token in Home Assistant

In Home Assistant:

1. Go to **Profile**
2. Scroll down → Click **Create Token**
3. Name it `Jarvis Assistant`
4. Copy and save the token securely

---

## 🔌 Step 2: Install `hassapi.py` or Call Script from Python

Install `requests` if using Python to trigger Home Assistant automations:

```bash
pip install requests
```

Example Python call:

```python
import requests

ha_url = "http://homeassistant.local:8123/api/services/light/turn_on"
token = "your-long-lived-access-token"

headers = {
    "Authorization": f"Bearer {token}",
    "content-type": "application/json",
}

data = {
    "entity_id": "light.living_room"
}

response = requests.post(ha_url, headers=headers, json=data)
print(response.text)
```

---

## 📡 Optional: Use MQTT Instead

If your Home Assistant is subscribed to an MQTT broker (e.g., Mosquitto):

```python
import paho.mqtt.client as mqtt

mqttc = mqtt.Client()
mqttc.connect("mqtt.local", 1883, 60)
mqttc.publish("jarvis/command", "turn_on living_room_lights")
```

In Home Assistant:
- Use MQTT automation trigger for `"jarvis/command"`
- Use a template or value match to run the action

---

## 🧪 Example Automations

| Voice Prompt                     | Automation Triggered                            |
|----------------------------------|--------------------------------------------------|
| “Turn on the kitchen lights”     | `light.turn_on` → `light.kitchen`               |
| “Arm the security system”        | `alarm_control_panel.arm_away`                 |
| “Start the coffee maker”         | `switch.turn_on` → `switch.coffee_maker`       |
| “Open the garage door”           | `cover.open_cover` → `cover.garage_door`       |

---

## 🛠 Tips

- Use `templates` in HA to parse incoming MQTT data
- Add fallback commands (e.g., “I didn’t catch that”)
- Log all prompts/responses in a flat file for debugging

---

## ✅ Success

Your Starktower AI Assistant now has **hands-free control** over your home — using local AI processing, with no cloud dependence.

Next Steps:

- Build `/scripts/` to automate orchestration
- Add `snapshot-backups.md` to manage full-system rollbacks
