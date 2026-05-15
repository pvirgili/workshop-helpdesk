# KB-IT-006: Password reset and account access issues

**Category:** Security / Identity  
**Impact:** High  
**Estimated resolution time:** 5–15 minutes

---

## Problem description

The user cannot log in to their Windows account or corporate applications due to an incorrect password, expired password, locked account, or MFA (multi-factor authentication) issues.

---

## Problem types and solutions

### Case A: Windows/Azure AD Password

#### Self-service (no IT needed) — SSPR
Techint has **Self-Service Password Reset (SSPR)** enabled:

1. Go to `https://aka.ms/sspr` from any browser.
2. Enter the corporate email (e.g.: `firstname.lastname@techint.com`).
3. Verify identity with:
   - Registered phone (SMS or call), OR
   - Microsoft Authenticator app, OR
   - Alternative email.
4. Create a new password that meets the requirements.
5. Wait 2 minutes before attempting to log in.

**Techint password requirements:**
- Minimum 12 characters.
- At least 1 uppercase, 1 lowercase, 1 number, 1 special character.
- Cannot be the same as the last 8 passwords used.
- Cannot contain the username.

#### If SSPR doesn't work
- The user did not register verification methods beforehand.
- Solution: contact the help desk with a valid ID for a manual reset.

---

### Case B: Locked Windows account

The account locks after **5 consecutive failed attempts** due to security policy.

**Automatic unlock:** The account unlocks on its own after **30 minutes**.

**Immediate unlock:** Only the IT team can do this. Contact the help desk.

---

### Case C: MFA — Code not arriving or no access to phone

1. **Try another method**: on the MFA screen, look for the "Use a different method" option.
2. **If the phone number changed**: contact the help desk to register the new phone.
3. **If the phone was lost**: escalate urgently to IT — the lost device must be disabled in Azure AD immediately for security reasons.

---

### Case D: SAP / legacy system password

Systems such as SAP SuccessFactors, SAP ERP and other legacy systems **do not sync** with Azure AD.  
Each system has its own recovery mechanism. See the specific article for each system or escalate to the help desk.

---

## Password change policy

- Passwords expire every **90 days**.
- Windows warns 14 days in advance.
- If the user works 100% remotely and doesn't connect to the VPN, they may not see the warning. Recommendation: change the password before it expires using `Ctrl+Alt+Del → Change a password`.

---

## When to escalate to the help desk

- SSPR doesn't work or the user didn't register verification methods.
- The account is locked and the user can't wait 30 minutes.
- The MFA device (phone) was lost.
- Possible security breach (someone else accessed the account).

**Suggested priority when escalating:** Critical if there is a possible security breach. High in all other cases.

---

## Information to gather when escalating

- Corporate email.
- Type of issue: expired, locked, forgotten password, MFA.
- Available MFA verification method.
- Last successful access (approximate date).
