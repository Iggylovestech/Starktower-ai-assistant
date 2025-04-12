# 🔐 Tailscale Remote Access Setup (Starktower AI)

This guide sets up **remote access** to your Proxmox server, LXC containers, and Docker services using [Tailscale](https://tailscale.com).

Tailscale creates a secure WireGuard-based mesh network across all your devices — perfect for accessing your AI assistant stack without opening ports or using cloud tunnels.

---

## ✅ Prerequisites

- A Tailscale account ([free plan works fine](https://tailscale.com/pricing/))
- Docker installed (for container-based install) or direct Proxmox host access

---

## 🧠 Step 1: Choose Install Method

**Option A**: Install Tailscale inside a **container or VM**

```bash
# On Debian-based container/VM
sudo apt update && sudo apt install tailscale -y
sudo tailscale up
```

**Option B**: Install Tailscale **directly on the Proxmox host**

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

You'll be given a login URL — sign in with your Tailscale account.

---

## 🧪 Step 2: Test Remote Access

Once connected:

- Visit your Tailscale dashboard: https://login.tailscale.com/admin/machines
- You should see your device listed and reachable via its `100.x.x.x` Tailnet IP
- Use this IP or assigned hostname to access:
  - `Proxmox GUI (https://100.x.x.x:8006)`
  - `Open WebUI (http://100.x.x.x:3000)`
  - `Portainer (http://100.x.x.x:9000)`

---

## 🛡️ Notes

- No port forwarding needed
- Works across mobile and desktop
- Ideal for local-only, offline-by-default setups

---

## 🧩 Integration Tips

- Set a **device name** in the Tailscale admin panel (e.g., `starktower-node`)
- Set up **ACLs (Access Control Rules)** if sharing access
- Enable **MagicDNS** for easier name-based access like:

```
https://starktower-node.tailnet-yourname.ts.net
```

---

## ✅ Remote access is now secure!

You're now ready to reach your full AI assistant stack from anywhere — without exposing anything to the public internet.
