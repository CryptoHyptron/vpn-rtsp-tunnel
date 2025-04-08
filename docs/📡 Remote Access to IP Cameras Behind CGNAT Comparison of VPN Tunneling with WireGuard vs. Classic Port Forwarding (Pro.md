### 📡 **Remote Access to IP Cameras Behind CGNAT: Comparison of VPN Tunneling with WireGuard vs. Classic Port Forwarding (Projects A, B, C)**

------

#### 🖥️ Hardware:

- 💻 **DELL XPS L702X with Ubuntu** – workstation acting as WireGuard client and gateway in Plan A, with `enp10s0` network card, LAN and Wi-Fi connection, local IP: 192.168.8.100 / 192.168.0.x
- 🌐 **Huawei H122-373 Router (T-Mobile)** – used in Plans A and B, under CGNAT, crashed during static routing attempts.
- 🌐 **Fiber Router (Home)** – used in Plan C, with public IP, supports RTSP port forwarding.
- ☁️ **AWS EC2 Server** – with public IP (xx.xxx.xx.xxx), acting as WireGuard server in Plans A and B.
- 📷 **Overmax Hot Spot 4.4 Wall Camera** – IP: 192.168.0.111, RTSP port: 554, login: admin, password: 123456.
- 📷 **Overmax Hot Spot 3.3 Rotating Camera** – IP: 192.168.0.109, RTSP port: 10554, login: admin, no password.
- 📱 **iPhone X** – used for VLC testing over LTE, remote camera access in Plan C.

------

### ❌ Plan A: Computer as WireGuard VPN Gateway (Failed Project)

**Goal:** Access IP cameras behind CGNAT (T-Mobile, Huawei router) using Ubuntu computer as a VPN gateway to AWS.

**Diagram:**

```
[iPhone LTE] ⇄ [AWS (WireGuard server)] ⇄ [Ubuntu (VPN gateway)] ⇄ [LAN 192.168.8.0/24] ⇄ [IP Cameras]
```

**Steps:**

1. Configure WireGuard server on AWS.
2. Set up WireGuard client on Ubuntu.
3. Enable IP forwarding (`sysctl`).
4. Add `iptables` NAT/routing rules.
5. Configure AWS with `AllowedIPs = 0.0.0.0/0`.
6. Connection lost after setting route – no internet or packets returned.

**Result:**

- ❌ AWS server unresponsive.
- ❌ Routing failed.
- ❌ Huawei router crashed with static routes.

**Conclusion:**
 Too risky with CGNAT + hardware issues. But valuable networking lesson 🧠.

------

### ❌ Plan B: WireGuard Client + RTSP Port Forwarding (Partial Attempt)

**Goal:** Use client VPN and forward RTSP port via socat to AWS public IP.

**Diagram:**

```
[iPhone LTE] ⇄ [rtsp://AWS-IP:8054] ⇄ [WireGuard tunnel] ⇄ [Ubuntu VPN client] ⇄ [Camera LAN]
```

**Steps:**

1. Set up VPN tunnel (Ubuntu ↔ AWS).
2. Configure `socat` and `iptables` on AWS.
3. Tested with both cameras.
4. Accessed via VLC/FFmpeg.

**Result:**

- ❌ socat running, ports open.
- ❌ RTSP stream failed.
- Errors: timeout / invalid data.

**Conclusion:**
 Setup correct ✅, but RTSP stream failed ❌ – likely camera compatibility or RTP issue.

------

### ✅ Plan C: Classic RTSP Port Forwarding (Success)

**Goal:** Simplify – no VPN, use public IP and router port forwarding.

**Diagram:**

```
[iPhone LTE] ⇄ [rtsp://PUBLIC-IP:8054] ⇄ [Fiber Router] ⇄ [Camera]
```

**Steps:**

1. Static IP for rotating camera: 192.168.0.109.
2. Port 8054 forwarded → 10554 (RTSP).
3. VLC over LTE successful.

**Result:**

- ✅ Smooth RTSP streaming.
- ⚠️ Wall cam unstable (connected once).

**Conclusion:**
 Most effective, minimal setup, perfect for real-world use 🎯.

------

### 📊 Comparison Summary

| Plan | Status    | Remote Access          | Cameras                 | Notes                                 |
| ---- | --------- | ---------------------- | ----------------------- | ------------------------------------- |
| A    | ❌ Failed  | WireGuard VPN Gateway  | none                    | Routing crash, CGNAT, unstable router |
| B    | ❌ Failed  | VPN Client + socat     | none                    | socat running, but RTSP didn’t stream |
| C    | ✅ Success | Direct Port Forwarding | rotating camera working | Easy, reliable, production-ready      |

------

🧠 **Project developed in collaboration with ChatGPT** as technical and documentation assistant.
 ✅ All data confirmed step-by-step by the author.