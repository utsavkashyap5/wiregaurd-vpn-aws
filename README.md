# 🔐 WireGuard VPN on AWS EC2

> Build your own secure VPN server on AWS using **WireGuard**, **Ubuntu 24.04**, and **Linux Networking**.

A beginner-friendly infrastructure project that demonstrates how to deploy a personal VPN on an AWS EC2 instance and securely connect an Android device through an encrypted WireGuard tunnel.

---

# 🚀 Why this project?

Whenever you browse the internet normally, your traffic travels directly through your Internet Service Provider (ISP).

```text
Phone
   │
ISP
   │
Internet
   │
Website
```

This means websites see your ISP's public IP address.

With WireGuard, an encrypted tunnel is established between your device and your own cloud server.

```text
Phone
   │
Encrypted WireGuard Tunnel
   │
AWS EC2 (Ubuntu)
   │
Internet
   │
Website
```

Now, internet traffic leaves from your AWS server instead of your mobile network, while remaining encrypted between your phone and the server.

---

# 🏗️ Project Architecture

```text
                    Internet
                        │
                AWS EC2 Instance
            Ubuntu 24.04 + WireGuard
              Public IP : xx.xx.xx.xx
                        │
          Encrypted WireGuard Tunnel
                        │
          Android Phone (WireGuard)
```

---

# 🌐 VPN Network

WireGuard creates a private network for trusted devices.

```text
VPN Network

Server (AWS EC2)
10.0.0.1
      │
      │
Phone
10.0.0.2
```

Every connected device receives its own private VPN IP address.

---

# ⚙️ Tech Stack

* ☁️ AWS EC2
* 🐧 Ubuntu 24.04 LTS
* 🔐 WireGuard
* 🖥️ Bash
* 🌐 Linux Networking
* 🔑 Public Key Cryptography
* 📡 UDP (51820)

---

# ✨ Features

* Secure VPN Server on AWS EC2
* WireGuard-based encrypted tunnel
* Android client support
* Public / Private Key authentication
* QR Code based client provisioning
* Linux IP Forwarding
* Network Address Translation (NAT)
* Lightweight and high-performance VPN

---

# 📂 Project Structure

```text
wireguard-vpn-aws/
│
├── README.md
├── client/
│   └── README.md
├── server/
│   └── README.md
├── scripts/
│   └── README.md
├── screenshots/
└── LICENSE
```

---

# 🛣️ Project Roadmap

* ✅ Launch AWS EC2 Instance
* ✅ Configure Security Groups
* ✅ Connect using SSH
* ✅ Install WireGuard
* ✅ Generate Server Keys
* ✅ Configure `wg0.conf`
* ✅ Start WireGuard Service
* ✅ Generate Client Keys
* ✅ Register Android Client
* ✅ Generate QR Code
* ✅ Connect Android Device
* ✅ Verify Secure VPN Tunnel
* ✅ Documentation

---

# 🔑 Core Concepts Learned

* VPN Fundamentals
* WireGuard Architecture
* Linux Networking
* Public & Private Key Cryptography
* IP Forwarding
* NAT (MASQUERADE)
* Client–Server Communication
* AWS EC2 Administration
* Secure Remote Access

---

# 📚 Documentation

Detailed documentation is available inside each directory.

| Folder     | Description                                          |
| ---------- | ---------------------------------------------------- |
| `server/`  | WireGuard server setup and configuration             |
| `client/`  | Android client configuration                         |
| `scripts/` | Commands and setup guide used throughout the project |

---

# 🎯 Learning Outcome

By completing this project, you will understand how a modern VPN works internally rather than simply installing one. You'll gain practical experience with Linux networking, cloud infrastructure, secure tunneling, key-based authentication, and WireGuard deployment on AWS.

---

# 📄 License

This project is available under the MIT License.

---

⭐ If this repository helped you learn WireGuard or Linux networking, consider giving it a star!
