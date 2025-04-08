---
title: "Beginner's Guide: WiFi Hacking with Kali Linux"
date: 2025-04-07
draft: false
tags: ["Kali Linux", "WiFi Hacking", "Cybersecurity", "Penetration Testing"]
categories: ["Guides", "Ethical Hacking"]
author: "ZeroDayGost"
---

### 5.) **Use `ifconfig` or `ip` in Kali Linux to View Network Details**

Before jumping into any wireless hacking activity, it's important to know your current network interface and IP configuration.

You can use the following command:

```bash
ifconfig
```

This shows all available network interfaces along with their IP addresses, MAC addresses, and other important network information.

![alt text](/20250328150501.png)

---

### 6.) **WiFi Hacking** (Educational Purposes Only ⚠️)

Let’s now walk through the **step-by-step process** of capturing a WPA2 handshake and attempting to crack a Wi-Fi password. This tutorial is strictly for ethical hacking practice in **authorized environments only**.

---

### 1. **Run the Script as Root**

Always run wireless hacking tools with elevated privileges to ensure access to network interfaces.

```bash
sudo ./your_script.sh
```

![alt text](/20250328150830.png)

---

### 2. **Select the Wireless Network Interface**

Choose your wireless adapter from the list that appears. Make sure it's compatible with monitor mode.

![alt text](/1.png)

---

### 3. **Put WiFi Adapter in Monitor Mode**

This mode allows the network adapter to capture packets from all networks in the air.

![alt text](/20250328151211.png)

**Successfully entered monitor mode:**

![alt text](/20250328151739.png)

---

### 4. **Scan for Available WiFi Networks**

To detect nearby Wi-Fi networks:

- Press `[4]` to begin scanning.
- After a few seconds, press `[Enter]` to stop the scan and move to the next step.

![alt text](/20250328151925.png)  
![alt text](/20250328152045.png)

---

### 5. **Select the Target**

After pressing `[Ctrl + C]`, the tool will ask you to choose a target network from the scan results.

Enter the number of the target network you want to attack.

![alt text](/20250328152116.png)

**Target successfully selected:**

![alt text](/20250328152157.png)

---

### 6. **Capture the WPA2 Handshake**

Capturing the handshake is the most critical step in a WPA2 attack.

- Press `[6]` to begin the handshake capture process.
- Choose `[1]` to launch a deauthentication attack.

This attack disconnects users from the network briefly, forcing them to reconnect. When they do, the WPA2 handshake is captured.

![alt text](/20250328152223.png)  
![alt text](/20250328152319.png)  
![alt text](/20250328152346.png)

Once started, you’ll see **two terminal windows**:

1. One to listen for the handshake.
2. Another to perform the attack.

Wait patiently for the handshake to appear in the logs.

![alt text](/20250328152411.png)  
![alt text](/20250328152529.png)

After successful capture, you'll be prompted to **save the handshake file**.

![alt text](/20250328153513.png)  
![alt text](/20250328153659.png)

---

### 7. **Crack the WPA2 Password**

Now comes the cracking part 🔐

We’ll use **brute-force** with a wordlist of possible passwords.

- Press `[1]` to use the wordlist option.
- Enter the path to your wordlist file (e.g., `/usr/share/wordlists/rockyou.txt`)

![alt text](/20250328155234.png)

Then press `[Enter]` to begin the attack. Sit back and wait.

![alt text](/20250328155249.png)

> ✅ **Successfully found the key!**  
> You now have the WPA2 password — job done!

---

### ⚠️ Final Thoughts

This walkthrough demonstrated how ethical hackers perform Wi-Fi security testing. These skills should only be used in lab environments or with **explicit permission**. Unauthorized access to networks is illegal and unethical.

Stay safe. Stay legal. Stay curious.  

---


