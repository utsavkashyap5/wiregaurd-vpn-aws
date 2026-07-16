# 📜 WireGuard Setup Scripts

This document contains every command used to configure a WireGuard VPN server on an AWS EC2 Ubuntu instance. Follow the steps in order to reproduce the setup.

> **Note:** Replace placeholder values (such as keys and public IPs) with your own values before using these commands.

---

# Step 1 — Update the System

Update the package list and install the latest security updates.

```bash
sudo apt update
sudo apt upgrade -y
```

---

# Step 2 — Install WireGuard

Install WireGuard and its utilities.

```bash
sudo apt install wireguard -y
```

Verify the installation.

```bash
wg --version
```

---

# Step 3 — Generate Server Keys

Create the server's private and public keys.

```bash
wg genkey | sudo tee /etc/wireguard/server_private.key | wg pubkey | sudo tee /etc/wireguard/server_public.key
```

Restrict access to the private key.

```bash
sudo chmod 600 /etc/wireguard/server_private.key
```

Verify the generated keys.

```bash
sudo ls -l /etc/wireguard
```

Display the server public key.

```bash
sudo cat /etc/wireguard/server_public.key
```

---

# Step 4 — Create the Server Configuration

Create the configuration file.

```bash
sudo nano /etc/wireguard/wg0.conf
```

Paste the following configuration.

```ini
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = <SERVER_PRIVATE_KEY>

PostUp = sysctl -w net.ipv4.ip_forward=1
PostUp = iptables -t nat -A POSTROUTING -o ens5 -j MASQUERADE

PostDown = iptables -t nat -D POSTROUTING -o ens5 -j MASQUERADE
```

> Replace `<SERVER_PRIVATE_KEY>` with the contents of:

```bash
sudo cat /etc/wireguard/server_private.key
```

---

# Step 5 — Start WireGuard

Start the VPN service.

```bash
sudo systemctl start wg-quick@wg0
```

Enable WireGuard at boot.

```bash
sudo systemctl enable wg-quick@wg0
```

Verify the service.

```bash
sudo systemctl status wg-quick@wg0
```

Display WireGuard status.

```bash
sudo wg
```

Display the VPN interface.

```bash
ip addr show wg0
```

---

# Step 6 — Generate Client Keys

Create a key pair for the Android client.

```bash
wg genkey | tee phone_private.key | wg pubkey > phone_public.key
```

Display the client public key.

```bash
cat phone_public.key
```

---

# Step 7 — Register the Client

Edit the server configuration.

```bash
sudo nano /etc/wireguard/wg0.conf
```

Append the following block.

```ini
[Peer]
PublicKey = <PHONE_PUBLIC_KEY>
AllowedIPs = 10.0.0.2/32
```

Restart WireGuard.

```bash
sudo systemctl restart wg-quick@wg0
```

---

# Step 8 — Install QR Generator

Install QR encoding utility.

```bash
sudo apt install qrencode -y
```

---

# Step 9 — Create Client Configuration

Create the client configuration file.

```bash
nano phone.conf
```

Paste the following configuration.

```ini
[Interface]
PrivateKey = <PHONE_PRIVATE_KEY>
Address = 10.0.0.2/24
DNS = 1.1.1.1

[Peer]
PublicKey = <SERVER_PUBLIC_KEY>
Endpoint = <EC2_PUBLIC_IP>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```

---

# Step 10 — Generate QR Code

Display a QR code directly in the terminal.

```bash
qrencode -t ansiutf8 < phone.conf
```

Or generate a PNG image.

```bash
qrencode -o phone.png < phone.conf
```

---

# Step 11 — Verification Commands

Check WireGuard status.

```bash
sudo wg
```

Check the service.

```bash
sudo systemctl status wg-quick@wg0
```

Check the VPN interface.

```bash
ip addr show wg0
```

Display the server public key.

```bash
sudo cat /etc/wireguard/server_public.key
```

Display the client public key.

```bash
cat phone_public.key
```

Display the server configuration.

```bash
sudo cat /etc/wireguard/wg0.conf
```

---

# AWS Security Group

| Type      | Protocol | Port  | Source    |
| --------- | -------- | ----- | --------- |
| SSH       | TCP      | 22    | Your IP   |
| WireGuard | UDP      | 51820 | 0.0.0.0/0 |

---

# Project Workflow

```text
Launch EC2
      │
SSH Connection
      │
Install WireGuard
      │
Generate Server Keys
      │
Configure wg0.conf
      │
Start WireGuard
      │
Generate Client Keys
      │
Register Client
      │
Create phone.conf
      │
Generate QR Code
      │
Import into Android
      │
VPN Tunnel Established
```

---

# Security Best Practices

* Never commit private keys to GitHub.
* Keep `server_private.key` and `phone_private.key` secret.
* Use Security Groups to expose only required ports.
* Rotate keys if they are accidentally exposed.
* Restrict SSH access to trusted IP addresses whenever possible.

---

# Learning Outcomes

By completing this setup, you will gain practical experience with:

* AWS EC2
* Ubuntu Server Administration
* WireGuard VPN
* Linux Networking
* Public Key Cryptography
* IP Forwarding
* NAT (MASQUERADE)
* Android VPN Configuration
* Secure Remote Access
