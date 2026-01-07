\# Secure Remote Access via Tailscale



\## Goal

Enable secure SSH access to the server from public Wi-Fi without exposing SSH to the public internet.



\## Threat Model

Public Wi-Fi networks are untrusted and susceptible to:

\- Traffic interception (MITM attacks)

\- Credential harvesting

\- Network scanning and service discovery



\## Architecture

\- WireGuard-based VPN using Tailscale

\- Identity-based device authentication

\- No port forwarding or public IP exposure

\- SSH accessible only over the VPN interface



```Laptop / Phone (Public Wi-Fi)

|

Encrypted VPN Tunnel

|

Tailscale Mesh Network

|

mcserverface (Ubuntu Server)

SSH (Key-only)```



\## Implementation Summary

\- Installed Tailscale on the Ubuntu server and client devices

\- Verified private Tailscale IP assignment

\- Disabled SSH password authentication

\- Restricted SSH to the Tailscale interface only

\- Disabled systemd SSH socket activation to prevent global port binding



\## Key Commands Used

```bash

\# Verify Tailscale IP

tailscale ip -4



\# Check effective SSH configuration

sudo sshd -T | grep listenaddress



\# Disable systemd socket activation for SSH

sudo systemctl disable --now ssh.socket



\# Restart SSH service

sudo systemctl restart ssh



\# Verify SSH listening interface

ss -tuln | grep :22



