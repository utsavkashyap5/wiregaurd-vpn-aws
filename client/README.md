# 📱 Client Setup (Android WireGuard)

This directory contains the client-side configuration and documentation for connecting an Android device to the WireGuard VPN server hosted on AWS EC2.

---

## 🎯 Objective

Configure an Android device as a secure WireGuard client capable of establishing an encrypted tunnel with the AWS EC2 VPN server.

---

## Components

* Android Device
* WireGuard Android Application
* Client Key Pair
* WireGuard Client Configuration (`phone.conf`)

---

## Configuration Overview

The client configuration contains:

* Client Private Key
* VPN Address
* DNS Server
* Server Public Key
* Server Endpoint
* Allowed IPs
* Persistent Keepalive

---

## Workflow

1. Install the WireGuard Android application.
2. Generate a client key pair.
3. Create the client configuration file.
4. Import the configuration using a QR code.
5. Activate the VPN tunnel.
6. Verify the handshake with the server.

---

## Security Notes

* Never expose the client private key.
* Do not commit configuration files containing secrets.
* Rotate keys if they are accidentally leaked.

---

## Learning Outcomes

* Understanding WireGuard client architecture
* Public & Private Key authentication
* VPN tunnel establishment
* Secure mobile networking

---

## Status

* ✅ Client Keys Generated
* ✅ Configuration Created
* ✅ QR Code Imported
* ✅ Tunnel Connected
* ✅ Secure Handshake Established
