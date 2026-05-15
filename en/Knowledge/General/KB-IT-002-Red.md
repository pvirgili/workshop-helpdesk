# KB-IT-002: No internet or corporate network connection

**Category:** Connectivity  
**Impact:** High  
**Estimated resolution time:** 10–20 minutes

---

## Problem description

The device has no access to the internet, the corporate network, or connectivity is very slow/unstable.

---

## Most common causes

1. Disabled network adapter or corrupt driver.
2. Incorrect static IP configuration (DHCP did not assign an address).
3. Corrupted DNS cache.
4. Misconfigured corporate proxy.
5. Disconnected or damaged network cable (for wired connection).
6. Issue with the office or home router/switch.

---

## Diagnostic and resolution steps

### Step 1 — Check the physical connection

**For wired connection:**
- Verify the RJ45 cable is properly connected to the device and the switch/router.
- Check that the network port LED is on (green or amber).
- Try a different cable if available.

**For WiFi:**
- Verify WiFi is not disabled (Fn+F2 key or tray icon).
- Verify the network name (SSID) is correct: `Techint-Corp` or `Techint-Guest`.

### Step 2 — Disable and re-enable the network adapter

1. Open **Device Manager** (right-click Start → Device Manager).
2. Expand **Network Adapters**.
3. Right-click the adapter → **Disable device** → wait 5 seconds → **Enable device**.
4. Alternatively, from PowerShell:
   ```powershell
   Disable-NetAdapter -Name "Ethernet" -Confirm:$false
   Start-Sleep -Seconds 5
   Enable-NetAdapter -Name "Ethernet" -Confirm:$false
   ```

### Step 3 — Renew IP address (DHCP)

Open **Command Prompt** as administrator and run:
```cmd
ipconfig /release
ipconfig /renew
```

Verify a valid IP was assigned:
```cmd
ipconfig /all
```
The IP should be in the `10.x.x.x` or `172.16.x.x` range for corporate network.

### Step 4 — Flush DNS cache

```cmd
ipconfig /flushdns
nbtstat -R
nbtstat -RR
netsh int ip reset
netsh winsock reset
```

Restart the device after running these commands.

### Step 5 — Check proxy configuration

1. Go to **Settings → Network & Internet → Proxy**.
2. If manually configured, verify it points to: `proxy.techint.com:8080`.
3. If the issue started after connecting to an external network, temporarily disable the manual proxy.

### Step 6 — Run Windows Network Diagnostics

1. Right-click the network icon in the system tray → **Troubleshoot problems**.
2. Follow the wizard's instructions.
3. If the wizard detects and fixes the issue, verify connectivity by opening a browser.

---

## When to escalate to the help desk

- The issue persists after all attempts.
- Multiple devices in the same office have the same issue (may be a switch or router problem).
- The network adapter doesn't appear in Device Manager (possible hardware failure).
- The device shows the error: **"No network hardware detected"**.

**Suggested priority when escalating:** High.

---
