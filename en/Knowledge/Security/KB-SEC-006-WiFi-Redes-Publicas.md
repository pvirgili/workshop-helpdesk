# KB-SEC-006: Safe use of corporate, home, and public WiFi networks

**Category:** Cybersecurity  
**Impact:** High  
**Estimated resolution time:** Informational document

---

## Introduction

Using the right type of network connection is essential to protect Techint's corporate information and your personal data. This guide covers best practices for the three main network scenarios: corporate office, home (home office), and public spaces.

---

## Corporate office network (Techint)

### Corporate WiFi — `Techint-Corp`

- **Who can access it:** Employees with corporate devices.
- **Authentication:** Automatically through the device certificate (no manual password needed).
- **Connection:** Open Techint network connections → Select `Techint-Corp`.
- **Level of protection:** High — monitored, filtered, protected by Zscaler.

### Guest WiFi — `Techint-Guest`

- **Who can access it:** Visitors, personal devices, external contractors.
- **Access:** Password available at reception or requested through the IT portal.
- **Restrictions:** Does NOT access the corporate network. Internet-only access with navigation restrictions.
- **Must NOT be used:** by employees for corporate work.

> ⚠️ **Warning:** Do not connect corporate devices to `Techint-Guest`. For corporate work, always use `Techint-Corp` or VPN.

---

## Home network (home office)

### Recommended home network configuration

| Setting | Recommendation |
|---|---|
| Router WiFi encryption | WPA3 (preferred) or WPA2-AES |
| Network password | Minimum 12 characters with letters, numbers, and symbols |
| Router firmware | Keep updated (check manufacturer's page) |
| Remote administration | Disable if not needed |
| Default password | Change immediately when configuring a new router |
| Shared network | Avoid sharing the work network with devices of other household members |

### Separate work from personal traffic (recommended)

Many modern routers allow creating a **guest network** for personal or IoT devices (smart TVs, speakers, home automation devices):

1. Access the router panel (usually `192.168.1.1` or `192.168.0.1`).
2. Look for the option **"Guest network"** or **"Isolation"**.
3. Connect work devices to the main network and personal/IoT devices to the guest network.

This prevents a compromised home device from affecting the work connection.

### Connect to corporate VPN from home

For accessing internal resources (shared drives, intranet, corporate systems):

1. Open **GlobalProtect** → click **Connect**.
2. Enter corporate credentials.
3. Work normally — all traffic is protected and encrypted.

See **KB-IT-001** for VPN connection details.

---

## Public networks (cafes, airports, hotels, conferences)

### General rule: **NEVER use public WiFi without VPN**

Risks of public WiFi:
- **Man-in-the-Middle:** An attacker on the same network can intercept unencrypted traffic.
- **Evil twin:** Fake access points that impersonate the real network.
- **Session hijacking:** Theft of authentication tokens.
- **Packet sniffing:** Capture of network traffic for later analysis.

### What to do on public WiFi

| Action | Allowed? |
|---|---|
| Connect to public WiFi to use **GlobalProtect VPN** | ✅ Yes (first activate VPN, then work) |
| Access corporate apps WITHOUT VPN | ❌ Not allowed |
| Personal browsing (news, maps) WITHOUT VPN | ⚠️ Low risk for personal use, but not recommended |
| Corporate video conferences WITHOUT VPN | ❌ Not allowed |
| Enter credentials on corporate sites WITHOUT VPN | ❌ Never |

### Recommended procedure on public networks

1. Connect to the available WiFi.
2. **Immediately open GlobalProtect** and activate VPN before doing anything else.
3. If VPN doesn't connect, use **your phone's mobile data** (personal hotspot) instead.
4. After finishing, disconnect from public WiFi and deactivate VPN.

### Using mobile data as a hotspot (recommended alternative)

If public WiFi is not secure or VPN doesn't connect:
1. iPhone: **Settings → Personal Hotspot → Enable.**
2. Android: **Settings → Connections → Mobile Hotspot → Enable.**
3. Connect the laptop to the phone's WiFi hotspot.
4. Mobile data is more secure than public WiFi (data is encrypted by the mobile carrier).

> 💡 **Tip:** IT can provide an approved mobile data plan for frequent travelers. Request at `helpdesk@techint.com`.

---

## Quick summary of prohibited behaviors

| Prohibited action | Why it's risky |
|---|---|
| Connecting corporate device to `Techint-Guest` | Bypasses corporate network protection |
| Using public WiFi without VPN | Exposes data to interception |
| Sharing VPN credentials with colleagues | Violates security policy and traceability |
| Disabling WiFi filtering or Zscaler | Bypasses web traffic protection |
| Working from a public computer (hotel, library) | Uncontrolled device, possible keyloggers |
| Connecting to corporate WiFi with a personal device | Risk of exposure if device is compromised |

---

## Contact

- **IT Help Desk (network and VPN issues):** `helpdesk@techint.com` / extension #5000
- **SOC (suspicious network activity):** `soc@techint.com` / extension #7777
- **Full WiFi policy:** `https://intranet.techint.com/it/politicas/redes-wifi`
