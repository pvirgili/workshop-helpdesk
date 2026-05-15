# KB-IT-004: Error accessing the Vacation Management System (HR Vacaciones)

**Category:** Internal Applications  
**Impact:** Medium  
**Estimated resolution time:** 5–20 minutes

---

## Problem description

The user cannot access the Techint vacation and leave management portal (`https://vacaciones.techint.com`). The most common errors are: 403 Access Denied, blank screen, login loop, or session expired message.

---

## Most common causes

1. **Error 403 – Access Denied**: the Azure AD session expired or the user does not have the system license assigned.
2. **Login loop / continuous redirects**: corrupted browser cookies or cache.
3. **Blank screen or not loading**: browser extensions are blocking the content.
4. **"Your account is not enabled for this application"**: the user doesn't have the role assigned in the Azure AD Enterprise Application.
5. **MFA repeatedly requested**: device not registered as trusted.

---

## Diagnostic and resolution steps

### Step 1 — Clear browser cache and cookies

**In Microsoft Edge:**
1. Press `Ctrl + Shift + Delete`.
2. Time range: **All time**.
3. Check: Browsing history, Cookies and other site data, Cached images and files.
4. Click **Clear now**.
5. Close and reopen the browser.
6. Try accessing `https://vacaciones.techint.com` again.

**In Google Chrome:**
1. Same shortcut `Ctrl + Shift + Delete`.
2. Same steps.

### Step 2 — Try in Incognito / Private mode

1. Open Edge: `Ctrl + Shift + N` | Chrome: `Ctrl + Shift + N`.
2. Navigate to `https://vacaciones.techint.com`.
3. If it works in incognito → the issue is with extensions or cache (see Step 3).
4. If it doesn't work in incognito either → proceed to Step 4.

### Step 3 — Disable browser extensions

1. In Edge: `edge://extensions/` | Chrome: `chrome://extensions/`.
2. Temporarily disable all extensions.
3. Reload the vacation portal page.
4. If it works, enable extensions one by one to identify which one is blocking access.
   - Extensions that commonly cause issues: uBlock Origin, AdGuard, Privacy Badger.

### Step 4 — Sign out of Azure AD and sign back in

1. Go to `https://myapps.microsoft.com`.
2. Click the avatar/username (top right) → **Sign out**.
3. Close the browser completely (check there are no open windows in the taskbar).
4. Reopen the browser and go to `https://vacaciones.techint.com`.
5. Sign in again with corporate credentials.

### Step 5 — Verify SSO session at `portal.office.com`

1. Go to `https://portal.office.com` and verify that login works correctly.
2. If `portal.office.com` also doesn't work, the issue is with the credentials (see KB-IT-006-Passwords).

---

## When to escalate to the help desk

- **Error 403** persists after clearing cache and signing out.
- Message: **"Your account is not enabled for this application"** → IT must assign the role in Azure AD (not resolvable by the user).
- The user is new or was recently promoted/transferred (may need access provisioning).
- Vacation approvals are pending and there is business urgency.

**Suggested priority when escalating:** Medium.

---

## Information to gather when escalating

- Exact URL and full error message (screenshot).
- Browser and version.
- Azure AD user (corporate email).
- Whether the issue started recently or has always been the case.
- Any recent changes: new password, new device, department transfer.
