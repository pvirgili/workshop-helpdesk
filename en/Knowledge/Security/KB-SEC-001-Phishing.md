# KB-SEC-001: How to identify and report a phishing email

**Category:** Cybersecurity  
**Impact:** Critical  
**Estimated resolution time:** 5–10 minutes

---

## Problem description

The user receives a suspicious email that could be a phishing attempt: identity impersonation to steal credentials, financial data, or install malware.

---

## Signs of a phishing email

1. **Suspicious sender** — the domain doesn't match the supposed company (e.g., `support@techint-security.xyz` instead of `@techint.com`).
2. **Excessive urgency** — messages like "Your account will be locked in 2 hours", "Immediate action required".
3. **Suspicious links** — when hovering over the link, the actual URL doesn't match the visible text.
4. **Unexpected attachments** — `.zip`, `.exe`, `.docm` (macros), `.html` files from unexpected senders.
5. **Spelling and grammar errors** — poorly translated text or obvious mistakes.
6. **Credential requests** — no Techint department will ask for passwords by email.
7. **Internal sender but unusual content** — may be a compromised account.

---

## What to do if you receive a suspicious email

### Step 1 — DO NOT interact

- **Do not click** on any link in the email.
- **Do not open** attachments.
- **Do not reply** to the sender.
- **Do not forward** the email to colleagues (to avoid accidental spreading).

### Step 2 — Report using the Outlook button

1. In Outlook (desktop or web), select the suspicious email.
2. In the toolbar, click **"Report phishing"** (shield icon with alert signal).
3. Confirm the report. The email will be automatically sent to the security team (SOC) for analysis.
4. The email will automatically move to the junk mail folder.

### Step 3 — If you don't see the report button

1. Forward the email **as an attachment** to: `soc@techint.com`
   - In Outlook: right-click the email → **Forward as Attachment**.
2. Add in the body: "I am reporting this email as a suspected phishing attempt."
3. Delete the original email from the inbox.

### Step 4 — If you clicked a link or entered credentials

**Immediate action (the first 15 minutes are critical):**

1. **Change your password** immediately at `https://aka.ms/sspr`.
2. **Call the SOC** at extension **#7777** or send a message to `soc-urgente@techint.com` with subject "Account compromise".
3. **Do not turn off the device** — the SOC may need to analyze it live.
4. **Disconnect from the network** if malware is suspected (unplug the network cable or disable WiFi).
5. The SOC will:
   - Revoke active sessions in Azure AD.
   - Review forwarding rules in the mailbox.
   - Perform forensic analysis of the device if a file was downloaded.

---

## Phishing simulation campaigns

Techint runs **quarterly phishing simulations** through the KnowBe4 platform:

- If the user falls for a simulation, **there is no penalty**, but a mandatory 15-minute training module is assigned.
- Results are individual-anonymous and reported in aggregate by department.
- Employees who correctly report simulations earn **recognition points** in the cybersecurity program.

---

## Reference statistics (Techint 2025)

| Metric | Value |
|---|---|
| Phishing emails blocked per month | ~45,000 |
| Click rate in simulations (Q4 2025) | 8.3% |
| Average user report time | 4.2 minutes |
| Accounts compromised by phishing (2025) | 12 cases |

---

## Contact

- **SOC (Security Operations Center):** extension #7777 / `soc@techint.com`
- **Phishing report (automated):** "Report phishing" button in Outlook
- **SOC hours:** 24/7 (emergencies) / Mon–Fri 8:00–20:00 (general inquiries)
