# KB-IT-001: I can't connect to the VPN

**Category:** Connectivity  
**Impact:** High  
**Estimated resolution time:** 15–30 minutes

---

## Problem description

The Techint VPN client (GlobalProtect) cannot establish a connection — it shows an authentication error, timeout, or simply won't connect.

---

## Most common causes

1. **Expired or incorrect credentials** — the network password was recently changed.
2. **Outdated GlobalProtect client** — minimum required version: 6.2.x.
3. **Conflict with another VPN** — Cisco AnyConnect, WireGuard, or another VPN running in parallel.
4. **Firewall or antivirus blocking traffic** — UDP 4501 and TCP 443 ports must be open.
5. **Expired machine certificate** — occurs on devices that haven't synced with the domain in more than 30 days.
6. **Corporate DNS not resolving the gateway** — occurs on networks with custom DNS (hotels, airports).

---

## Diagnostic and resolution steps

### Step 1 — Verify credentials

Confirm the user remembers their network password. If it expired:
- Go to `https://aka.ms/sspr` (Techint Self-Service Password Reset).
- If SSPR doesn't work, contact the help desk with a valid ID.

### Step 2 — Verify client version

1. Open GlobalProtect → system tray icon.
2. Go to **About** → check the version.
3. If older than 6.2.0: download the updated installer from the IT Portal:  
   `https://intranet.techint.com/it/vpn-installer`
4. Uninstall the old version → restart → install the new version.

### Step 3 — Close other active VPNs

1. Check the system tray for any other active VPN clients.
2. Disconnect and disable any other VPN client.
3. Try connecting GlobalProtect again.

### Step 4 — Check ports with the local router/firewall

From a corporate network or mobile data (not the problematic WiFi):
1. Try connecting GlobalProtect using your phone's mobile data as a hotspot.
2. If it connects via hotspot but not via WiFi → the local router or firewall is blocking the ports.
3. Solution: use a different network, or contact your ISP to open UDP 4501 and TCP 443 ports.

### Step 5 — Reinstall the client from scratch

1. Uninstall GlobalProtect from **Control Panel → Add or Remove Programs**.
2. Delete residual folders:
   - `C:\Program Files\Palo Alto Networks\GlobalProtect`
   - `C:\ProgramData\Palo Alto Networks`
3. Restart the device.
4. Install the latest version from `https://intranet.techint.com/it/vpn-installer`.
5. When configuring, use the gateway: `vpn.techint.com`.

### Step 6 — Renew the machine certificate (IT required)

If the device hasn't connected to the corporate domain in more than 30 days:
1. Connect the device to the office network (wired or corporate WiFi).
2. Restart the Windows session with domain credentials.
3. Wait 5 minutes for the Group Policy (GPO) to apply.
4. Try connecting to the VPN again.

---

## When to escalate to the help desk

- The issue persists after all the steps above.
- The user sees the error: **"Authentication failed – Certificate error"**.
- The device was borrowed, reassigned, or recovered from another user.
- The device hasn't been to an office in more than 6 months.

**Suggested priority when escalating:** High (the user cannot work remotely).

---

## Information to gather when escalating

- Operating system and Windows/macOS version.
- GlobalProtect version installed.
- Exact error message (screenshot).
- Network being used (home WiFi, mobile data, hotel, etc.).
- Last date the VPN worked correctly.
