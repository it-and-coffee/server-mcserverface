## Architecture Overview
```
        ┌──────────────┐
        │  Windows PC  │
        │  (Git Bash)  │
        └──────┬───────┘
               │ SSH
               │
        ┌──────▼───────┐
        │ Ubuntu Server│
        │ mcserverface │
        │ (Home Lab)   │
        └──────┬───────┘
               │
      ┌────────▼────────┐
      │  Services / OS  │
      │  SSH, Files,    │
      │  Monitoring     │
      └─────────────────┘

```
## Remote Administration

```
Remote Access (Optional):
───────────────────────
Phone / Laptop
    │
Tailscale
    │
mcserverface
```
## Design Decisions

This homelab was intentionally designed to mirror real-world system administration practices while remaining simple and maintainable. SSH key-based authentication was chosen over password-based access to reduce brute-force risk and align with industry security standards. Tailscale was used for remote access instead of exposing ports on the home router, minimizing attack surface while enabling secure access from multiple devices. Documentation and version control were prioritized so configuration choices and system intent are clearly communicated, not just implemented.

## Network Flow
```
[Remote Device]
   (Laptop / Phone)
        │
        │ Encrypted Tunnel
        ▼
    [Tailscale]
        │
        │ Private Mesh Network
        ▼
[mcserverface]
 Ubuntu Server
 (SSH / Services)
```
# server-mcserverface

Personal Ubuntu Server (Home Lab)

## SSH
- Key-based authentication only
- Password login disabled
- Client alias: mcface

## Devices
- Windows laptop (tanya@MSI)
- Android phone (tanya-phone)

## Network
- Local IP: 192.168.1.75
- SSH: port 22

## Notes
- SSH configs via /etc/ssh/sshd_config.d/
- authorized_keys managed per-device

Built by learning, breaking, and fixing.


