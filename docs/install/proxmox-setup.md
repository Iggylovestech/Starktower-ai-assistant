# Proxmox Setup Guide (Dell R730 Build)

This guide walks through preparing a Dell PowerEdge R730 for the Starktower AI Assistant stack using Proxmox VE.

---

## Hardware Summary

| Component     | Details                         |
|---------------|---------------------------------|
| Model         | Dell PowerEdge R730XD (24-bay)  |
| CPU           | 2× Intel Xeon E5-2690 v4 (28C)  |
| RAM           | 128GB DDR4                      |
| Storage       | 6× 1.2TB SAS (RAID 5), 2× SSDs  |
| Network       | Dual 10GbE (LACP)               |
| Management    | iDRAC8 Express                  |

---

## Step-by-Step Proxmox Install

1. Download Proxmox ISO from [https://proxmox.com](https://proxmox.com)
2. Flash ISO to USB using Balena Etcher or Rufus
3. Boot server via USB, select UEFI
4. Install Proxmox VE on one SSD
5. Assign static IP (match VLAN/firewall config)
6. Configure second SSD or RAID volume for:
   - LXC storage
   - Backups
   - VM volumes

---

## Storage Planning

- `/dev/sda` = Proxmox OS
- `/dev/sdb` = LXC container storage (LVM Thin or ZFS)
- `/dev/md0` = RAID 5 array (VMs, Docker volumes, archive)

---

## Post-Install Checklist

- [ ] Disable Proxmox firewall (unless needed)
- [ ] Create bridge (e.g., `vmbr0`) for VLAN access
- [ ] Test web GUI: `https://<your-ip>:8006`
- [ ] Create backup volume (`Directory` or `LVM-Thin`)
- [ ] Enable SSH + root login for remote config

---

## Snapshots & Templates

- Use LXC templates for quick service deployments
- Snapshot base containers before major changes
- Schedule Proxmox backups to `/dev/sdb` or NAS

---

## Related Docs

- [LXC vs VM Audio](./lxc-vs-vm-audio.md)
- [Docker Deployment](./docker-deployment.md)
- [Voice Assistant Pipeline](./voice-assistant-pipeline.md)
