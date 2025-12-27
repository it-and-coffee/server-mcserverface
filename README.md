## Architecture Overview
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

   Remote Access (Optional):
   ───────────────────────
        Phone / Laptop
            │
        Tailscale
            │
        mcserverface



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


