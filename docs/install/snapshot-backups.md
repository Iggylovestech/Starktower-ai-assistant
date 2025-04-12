# 💾 Snapshot + Backup Strategy (Starktower AI)

This guide outlines how to back up your full Proxmox-based AI assistant stack — including LXC containers, Docker volumes, and important configuration files.

Backups ensure you can **revert**, **restore**, or **rebuild** in minutes if anything breaks.

---

## 🧠 Overview: What You’ll Back Up

| Component         | What to Back Up                              | How                |
|------------------|-----------------------------------------------|--------------------|
| Proxmox Config    | VM + LXC definitions, host settings           | Scheduled backups  |
| LXC Containers    | Filesystems (Open WebUI, Whisper, etc.)       | Snapshot + export  |
| Docker Volumes    | LLMs, WebUI data, Ollama cache                | Manual tarball     |
| Python Scripts    | Orchestration, wake-word handlers             | GitHub or zip      |
| Static Files      | Audio logs, prompts, voice responses          | Periodic rsync     |

---

## 📦 Step 1: Create Proxmox LXC Snapshot

On your Proxmox host:

```bash
# List containers
pct list

# Create snapshot for container 101
pct snapshot 101 starktower-checkpoint

# To rollback:
pct rollback 101 starktower-checkpoint
```

---

## 🧳 Step 2: Export LXC Container for Offsite Storage

```bash
# Replace 101 with your container ID
pct stop 101
vzdump 101 --mode stop --compress zstd --storage local
```

File will be saved to `/var/lib/vz/dump/`.

---

## 📁 Step 3: Back Up Docker Volumes (Manual or Scripted)

Example for `ollama` model volume:

```bash
docker run --rm \
  -v ollama_ollama:/volume \
  -v $(pwd):/backup \
  alpine tar -czf /backup/ollama_backup.tar.gz -C /volume .
```

Repeat for:
- `openwebui_data`
- `whisper_audio`
- `piper_voice_data`

---

## 💻 Step 4: Back Up Scripts + Markdown Docs

If you've saved your orchestration, STT/TTS helpers, and install guides locally:

```bash
tar -czvf starktower_scripts_backup.tar.gz ~/starktower/scripts/
```

Push them to:
- GitHub repo (recommended)
- Encrypted USB stick
- Tailscale-connected NAS

---

## 🧪 Optional: Automate with Cron

Create backup script:

```bash
nano /usr/local/bin/starktower_backup.sh
```

```bash
#!/bin/bash
pct snapshot 101 daily-snap
docker exec ollama ollama list > /root/model-list.txt
tar -czf /root/docker-volumes.tar.gz /var/lib/docker/volumes/
```

Make it executable and schedule it:

```bash
chmod +x /usr/local/bin/starktower_backup.sh
crontab -e
```

Add:

```
0 3 * * * /usr/local/bin/starktower_backup.sh
```

Runs daily at 3AM.

---

## ✅ Backup System Ready

With snapshot and export logic in place, you now have:

- Point-in-time LXC recovery
- Portable backups of all AI assistant containers
- Data security without cloud reliance

Test restore monthly. Store backups on at least two devices.

Next steps:
- Use this strategy for each new container or service
- Add `docs/troubleshooting/common-errors.md` for recovery support
