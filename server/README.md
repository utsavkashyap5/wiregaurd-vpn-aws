# 🖥️ Server Setup (AWS EC2)

This directory documents the complete setup of a WireGuard VPN server running on an Ubuntu EC2 instance.

---

## 🎯 Objective

Deploy a secure WireGuard VPN server on AWS EC2 and configure it to securely route client traffic through an encrypted tunnel.

---

## Infrastructure

| Component        | Technology                |
| ---------------- | ------------------------- |
| Cloud Provider   | AWS EC2                   |
| Operating System | Ubuntu 24.04 LTS          |
| VPN Software     | WireGuard                 |
| Networking       | Linux IP Forwarding & NAT |
| Firewall         | AWS Security Groups       |
| Protocol         | UDP (51820)               |

---

## Server Responsibilities

* Authenticate clients
* Maintain encrypted VPN tunnels
* Forward network packets
* Perform Network Address Translation (NAT)
* Route client traffic securely

---

## Setup Steps

1. Launch Ubuntu EC2 Instance
2. Configure Security Group
3. Connect via SSH
4. Install WireGuard
5. Generate Server Keys
6. Configure `wg0.conf`
7. Enable IP Forwarding
8. Configure NAT
9. Add Client Peer
10. Start WireGuard Service

---

## Networking

VPN Network

```text
Server : 10.0.0.1
Phone  : 10.0.0.2
```

WireGuard listens on:

```text
UDP 51820
```

---

## Security

* Server private key remains confidential.
* Public keys are exchanged with clients.
* Only registered peers are allowed to connect.
* NAT is enabled using iptables.

---

## Verification Commands

```bash
sudo wg
sudo systemctl status wg-quick@wg0
ip addr show wg0
```

---

## Learning Outcomes

* AWS EC2 Administration
* Linux Networking
* WireGuard Configuration
* VPN Architecture
* Secure Remote Access
* Public Key Cryptography

---

## Status

* ✅ EC2 Configured
* ✅ WireGuard Installed
* ✅ Server Keys Generated
* ✅ Server Configured
* ✅ Client Added
* ✅ VPN Running
* ✅ Secure Tunnel Established
