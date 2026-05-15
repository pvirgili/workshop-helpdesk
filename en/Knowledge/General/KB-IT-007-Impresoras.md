# KB-IT-007: Corporate printer issues

**Category:** Hardware / Printing  
**Impact:** Low  
**Estimated resolution time:** 10–20 minutes

---

## Problem description

The printer is not printing, shows as offline, print jobs are stuck in the queue, or print quality is poor.

---

## Most common causes

1. Print Spooler service stopped.
2. Jobs stuck in the print queue.
3. Printer disconnected from the network or powered off.
4. Outdated or corrupt driver.
5. Out of paper or paper jam.
6. Toner or cartridge empty.

---

## Diagnostic and resolution steps

### Step 1 — Check the printer's physical status

1. Verify the printer is powered on (green indicator light).
2. Verify paper is correctly loaded.
3. Check for a paper jam (open the front/rear cover depending on the model).
4. Check the toner level from the printer's panel or its software.

### Step 2 — Check printer network connectivity

1. On the printer's panel, print a **network configuration page** (press and hold the configuration button for 3 seconds on most models).
2. Verify it has an assigned IP address.
3. From the computer, check connectivity:
   ```cmd
   ping [printer_IP_address]
   ```
4. If it doesn't respond to ping → the printer is disconnected from the network. Restart the printer and wait 2 minutes.

### Step 3 — Clear the print queue

**Automatic method (recommended):**
1. Open PowerShell as administrator.
2. Run:
   ```powershell
   Stop-Service -Name Spooler -Force
   Remove-Item "$env:SystemRoot\System32\spool\PRINTERS\*" -Recurse -Force
   Start-Service -Name Spooler
   ```

**Manual method:**
1. Open **Services** (search "Services" in the Start menu).
2. Find **Print Spooler** → right-click → **Stop**.
3. Open File Explorer → navigate to `C:\Windows\System32\spool\PRINTERS`.
4. Delete all files in that folder (not the subfolders).
5. Return to **Services** → **Print Spooler** → **Start**.

### Step 4 — Reinstall the printer driver

1. Go to **Settings → Bluetooth & devices → Printers & scanners**.
2. Select the printer → click **Remove**.
3. Click **Add device** → Windows will search for the printer automatically.
4. If not found, install the driver manually from the IT Portal:
   `https://intranet.techint.com/it/drivers-impresoras`

---

## Techint network printers (main models)

| Floor/Area | Model | IP |
|---|---|---|
| Floor 3 — Buenos Aires | HP LaserJet M507 | 10.10.3.25 |
| Floor 4 — Buenos Aires | Ricoh SP 5300DN | 10.10.4.30 |
| Floor 5 — Buenos Aires | Canon imageRUNNER 2630i | 10.10.5.15 |
| San Nicolás — Plant | HP OfficeJet Pro 9010 | 172.16.1.50 |

---

## When to escalate to the help desk

- Persistent paper jam that cannot be resolved manually.
- Hardware failure (strange noises, permanent panel errors).
- Need to add a new printer to a device.
- Network printer is not responding from any device.

**Suggested priority when escalating:** Low (user can print from another network printer in the meantime).

---

## Information to gather when escalating

- Printer name or IP address.
- Printer model.
- Error message on the printer panel or on the computer.
- Floor/location.
