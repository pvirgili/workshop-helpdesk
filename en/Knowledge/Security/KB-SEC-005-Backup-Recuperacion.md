# KB-SEC-005: Backup and file recovery

**Category:** Data Management / Cybersecurity  
**Impact:** High  
**Estimated resolution time:** 15 minutes – 4 hours (depending on file size and location)

---

## Problem description

The user accidentally deleted a file, overwrote it, or experienced data loss due to a hardware or malware incident and needs to recover their information.

---

## Techint backup infrastructure

### Corporate files — SharePoint and OneDrive

| Parameter | Value |
|---|---|
| Storage location | Microsoft 365 cloud (SharePoint Online / OneDrive for Business) |
| Version history | 500 versions per file |
| Retention for deleted files | 93 days in the Recycle Bin |
| Backup type | Automatic, continuous (no manual action needed) |
| Geographic redundancy | 3 copies in geographically distributed Azure data centers |

### Local files (device)

| Parameter | Value |
|---|---|
| Solution | Microsoft OneDrive (automatic sync) |
| Corporate policy | Work files must be saved in OneDrive or SharePoint |
| Local files NOT in OneDrive | NOT backed up — no recovery if device fails |

> ⚠️ **Warning:** Files saved only on the desktop or local C: drive (not synced to OneDrive) **cannot be recovered** in case of device failure, format, or ransomware. Make sure to save all important files in OneDrive or SharePoint.

### Corporate servers

| Parameter | Value |
|---|---|
| Solution | Veeam Backup & Replication |
| Backup frequency | Every 4 hours (RPO: 4 hours) |
| Retention | 30 days of daily backups / 12 months of monthly backups |
| Recovery time objective (RTO) | 4 hours (critical systems) |
| Geographic backup | Replication to secondary data center (Monterrey) |

---

## How to recover files in SharePoint / OneDrive

### Option A — Recover from Recycle Bin (deleted files)

1. Go to `https://portal.office.com` → **OneDrive**.
2. In the left panel, click **Recycle Bin**.
3. Find the deleted file.
4. Right-click → **Restore**.
5. The file will return to its original location.

> Files in the Recycle Bin are kept for **93 days**. After that, they are automatically deleted.

### Option B — Recover a previous version of a file (overwritten)

1. Go to OneDrive or SharePoint and locate the file.
2. Right-click on the file → **Version History**.
3. A list of all saved versions will appear (with date and author).
4. Click **Restore** on the desired version, or **Download** if you want to compare first.

### Option C — Recover a SharePoint site or library

If an entire library or document was deleted:
1. Contact the IT Help Desk: `helpdesk@techint.com`.
2. Provide: library URL, approximate deletion date, documents to be recovered.
3. IT can restore at the site or library level from the Microsoft 365 admin console.

---

## How to recover files from corporate servers (on-premises)

For files stored in shared network folders (\\\\techint-fs01 or similar):

1. Open Windows Explorer → navigate to the folder containing the deleted file.
2. Right-click on the folder → **Restore previous versions**.
3. A list of available shadow copies will appear (taken every 4 hours).
4. Select a version and click **Restore** or **Open** to copy specific files.

If previous versions are not available:
1. Open a ticket with the IT Help Desk: `helpdesk@techint.com`.
2. Specify: exact path of the file/folder, approximate date of last seen, file description.
3. IT will manage recovery through Veeam. Estimated time: 2–4 hours.

---

## Recovering after ransomware

If ransomware has encrypted files, **do not try to recover yourself**:

1. Isolate the device (see KB-SEC-002).
2. Notify the SOC immediately: extension #7777.
3. The SOC will:
   - Determine the scope of the encryption.
   - Restore from the most recent valid backup.
   - Verify integrity before reconnecting the device.

Techint's policy is **not to pay ransoms**. Backups allow recovery with minimal data loss.

---

## Best practices to avoid data loss

1. **Always save to OneDrive or SharePoint**, not to local C:\.
2. **Don't turn off OneDrive sync** — the blue cloud icon must appear in the taskbar.
3. **Do not delete shared files** without confirming with the team first.
4. **Before modifying critical documents**, create a copy with a clear version name.
5. **Reports anomalous file changes** (extensions, permissions) to the SOC.

---

## Contact

- **IT Help Desk (file recovery):** `helpdesk@techint.com` / extension #5000
- **SOC (ransomware or malware incident):** `soc@techint.com` / extension #7777
- **Hours:** Mon–Fri 8:00–20:00 / 24/7 for critical incidents
