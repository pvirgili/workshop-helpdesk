# KB-IT-005: HR Portal Access (SAP SuccessFactors)

**Category:** Internal Applications  
**Impact:** Medium  
**Estimated resolution time:** 10–20 minutes

---

## Problem description

The user cannot access the Human Resources portal (`https://hcm.techint.com` / SAP SuccessFactors) — they receive a login error, access denied, or the portal does not load correctly.

---

## Most common causes

1. **Expired password** in SAP SuccessFactors (system independent from Azure AD).
2. **Active session on another device** blocking a new login.
3. **SAP license not assigned** (new or transferred users).
4. **Browser incompatibility** — SAP SuccessFactors requires Microsoft Edge or Chrome.
5. **Incorrect time zone setting** — may cause SAML authentication errors.

---

## Diagnostic and resolution steps

### Step 1 — Verify the browser

SAP SuccessFactors requires:
- **Microsoft Edge** (version 109 or later) ✅
- **Google Chrome** (version 109 or later) ✅
- **Mozilla Firefox** ❌ Not supported
- **Internet Explorer** ❌ Not supported

Switch to the correct browser before continuing.

### Step 2 — Disable compatibility mode and extensions

In Edge:
1. Go to `edge://settings/defaultBrowser`.
2. Verify that IE mode is disabled for `hcm.techint.com`.
3. Disable extensions (same procedure as KB-IT-004).

### Step 3 — Clear cache

1. `Ctrl + Shift + Delete` → clear all history for "All time".
2. Reopen the browser.
3. Go to `https://hcm.techint.com`.

### Step 4 — Attempt to reset the SAP password

SAP SuccessFactors has its own password system (separate from Windows/Azure AD):
1. On the SAP login screen, click **"Forgot your password?"**.
2. Enter the corporate email.
3. Check the corporate email for the reset link (may take up to 5 minutes).
4. If the email doesn't arrive, check the spam or junk folder.

### Step 5 — Check the device's time zone

1. Right-click the system clock → **Adjust date/time**.
2. Verify the time zone is correct (for example: `(UTC-03:00) Buenos Aires` for Argentina).
3. Enable **Set time zone automatically**.

---

## When to escalate to the help desk

- The user is new (less than 30 days) and has never been able to access.
- Message: **"Your account does not have access to this company"**.
- The user has a recent area or position change and lost previous access.
- Access was revoked due to inactivity and needs reactivation by HR.

**Note:** SAP SuccessFactors license assignment requires HR department approval. IT cannot grant access without that authorization.

**Suggested priority when escalating:** Medium.

---

## Information to gather when escalating

- User's corporate email.
- Full error message and screenshot.
- Area/Division at Techint.
- If new user, start date.
- Whether the access issue is historical or new.
