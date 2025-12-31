# server-mcserverface

Personal Ubuntu Server (Home Lab)

## SSH
- Key-based authentication only
- Password login disabled
- Client alias: mcface

## Devices
- Windows laptop (tanya@MSI)
- Android phone (tanya-phone)
- Tablet

## Network
- Local IP: 192.xxx.x.xx
- SSH: port 22

## Notes
- SSH configs via /etc/ssh/sshd_config.d/
- authorized_keys managed per-device

Built by learning, breaking, and fixing.



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


## 🔐 SSH Hardening (Key-Only Access)
### Overview
Hardened SSH access on an Ubuntu server by disabling password-based authentication and enforcing key-only login to reduce exposure to brute-force attacks and credential compromise.

```$ sudo sshd -T -f /etc/ssh/sshd_config | grep passwordauthentication
passwordauthentication no

$ ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no user@server
Permission denied (publickey).
```

### Actions Taken
- Generated a dedicated ED25519 SSH key pair for the server
- Configured SSH to disable password authentication
- Disabled root login over SSH
- Implemented a final override configuration using `/etc/ssh/sshd_config.d/100-final.conf`
- Verified effective SSH configuration using `sshd -T`
- Confirmed password authentication was denied via forced login tests

### Security Impact
This configuration eliminates password-based SSH access, significantly reducing the risk of brute-force attacks. Enforcing cryptographic key authentication ensures that only trusted devices can access the server while preserving secure administrative control.


### Lessons Learned
- Ubuntu SSH configuration is layered and may include multiple override files
- Cloud-init and included configs can silently re-enable defaults
- `sshd -T` is the authoritative way to verify effective SSH configuration
- Hardening must be validated through testing, not assumptions


