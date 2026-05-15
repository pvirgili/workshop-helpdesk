# KB-SEC-003: Personal device usage policy (BYOD)

**Category:** Cybersecurity / Policy  
**Impact:** Medium  
**Estimated resolution time:** 1–2 business days (enrollment process)

---

## What is BYOD?

**BYOD (Bring Your Own Device)** refers to the use of personal devices (phones, tablets, laptops) to access corporate resources (email, SharePoint, Teams).

Techint allows **limited** BYOD use under the conditions described in this document.

---

## What is and isn't allowed

### Mobile devices (smartphones and tablets) — ALLOWED with conditions

| Use case | Personal device | Corporate device |
|---|---|---|
| Microsoft Teams | ✅ Allowed | ✅ Allowed |
| Corporate email (Outlook) | ✅ With MDM enrollment | ✅ Full access |
| SharePoint / OneDrive (read) | ✅ With MDM enrollment | ✅ Full access |
| File editing and download | ⚠️ Limited by MAM policy | ✅ Full access |
| VPN GlobalProtect | ❌ Not allowed | ✅ Allowed |
| SAP ERP | ❌ Not allowed | ✅ Allowed |
| Sensitive system access | ❌ Not allowed | ✅ With MFA |

### Personal laptops or PCs — NOT ALLOWED

Techint does not allow personal computers to access corporate systems, **except** through a web browser to:
- Microsoft 365 web apps (Outlook, Teams, SharePoint).
- Techint intranet (read-only, public sections).

Corporate VPN **cannot** be installed on personal devices.

---

## How to enroll a personal mobile device (MDM)

If the user wants to access corporate email and Teams from their personal phone:

### iOS (iPhone/iPad)
1. Install the **Microsoft Intune Company Portal** app from the App Store.
2. Open the app → **Sign in** with the corporate account.
3. Follow the enrollment wizard.
4. Install the required **corporate configuration profile** when prompted.
5. Once enrolled, access Outlook and Teams with your corporate account.

### Android
1. Install **Microsoft Intune Company Portal** from the Play Store.
2. Follow the same process as iOS.
3. For Samsung devices with Knox: enhanced security will be configured automatically.

> ⚠️ **Note:** Enrollment does NOT give IT remote access to personal data, photos, or applications. The corporate profile only manages corporate apps and data.

---

## Data protection on personal devices

When a device is enrolled under MAM/MDM:

| Policy | Effect |
|---|---|
| Copy/paste between apps | Restricted between corporate and personal apps |
| Screenshots in corporate apps | Blocked (Teams, Outlook) |
| Corporate data download | Controlled — cannot be saved to personal gallery |
| Remote wipe in case of loss | Only the **corporate profile** is erased; personal data is NOT affected |
| Required device PIN | Minimum 6 digits or biometrics |

---

## What happens if the employee leaves the company?

When employment ends, IT will:
1. Remotely remove the corporate profile from the enrolled device.
2. All corporate accounts and data will be erased from the device.
3. Personal apps, personal photos, and personal data are not affected.

---

## Prohibited uses of personal devices

- Access corporate systems through jail-broken or rooted devices.
- Install unofficial or modified versions of corporate apps.
- Share corporate information through personal messaging apps (WhatsApp, Telegram, personal email).
- Use personal devices to store highly confidential information (Level 3 classification — see KB-SEC-004).

---

## Loss or theft of an enrolled personal device

1. Immediately report to the SOC: `soc@techint.com` / extension #7777.
2. IT will perform a **selective wipe** of the corporate profile.
3. Complete the loss report form: `https://intranet.techint.com/it/solicitudes/perdida-dispositivo`.

---

## Contact

- **IT Help Desk:** `helpdesk@techint.com` / extension #5000
- **SOC (loss or theft):** `soc@techint.com` / extension #7777
- **BYOD documentation:** `https://intranet.techint.com/it/politicas/byod`
