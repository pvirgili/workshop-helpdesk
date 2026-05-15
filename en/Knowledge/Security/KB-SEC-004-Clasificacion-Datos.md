# KB-SEC-004: Information classification and sensitive data handling

**Category:** Cybersecurity / Policy  
**Impact:** High  
**Estimated resolution time:** Informational document

---

## Why classify information?

Not all information has the same value or risk. Information classification allows us to:
- Apply the right level of protection to each type of data.
- Comply with legal regulations (GDPR, Argentine Personal Data Protection Law, financial regulations).
- Reduce the risk of unauthorized disclosures.
- Establish clear responsibilities for each employee.

---

## Techint information classification levels

### Level 1 — Public

| | |
|---|---|
| **Definition** | Information that can be shared publicly without restriction. |
| **Examples** | Press releases, corporate website, published annual reports, publicly available job listings. |
| **Controls** | No special controls required. |
| **Label in documents** | No label required / `PUBLIC` |

---

### Level 2 — Internal use only

| | |
|---|---|
| **Definition** | Information intended for use by Techint employees only; its disclosure would cause no serious harm but goes beyond what should be public. |
| **Examples** | Internal manuals, internal procedures, project plans, organizational charts, non-sensitive internal emails. |
| **Controls** | Do not share outside the company without authorization; do not publish on external platforms. |
| **Label in documents** | `INTERNAL USE ONLY` |

---

### Level 3 — Confidential

| | |
|---|---|
| **Definition** | Information whose unauthorized disclosure could cause significant harm to Techint, clients, or employees. |
| **Examples** | Commercial contracts, client data, financial information not yet published, technical specifications, HHRR data (salaries, performance reviews), bid documents, IT security configurations. |
| **Controls** | Encryption required if stored in the cloud or sent by email; access restricted by role; not allowed on personal devices; requires confidentiality agreement for external sharing. |
| **Label in documents** | `CONFIDENTIAL` |

---

### Level 4 — Highly confidential / Restricted

| | |
|---|---|
| **Definition** | Most critical information. Unauthorized access would have serious legal, financial, or reputational consequences. |
| **Examples** | M&A negotiations, government contract details, personal data of high-risk individuals, access keys to critical systems, SOC forensic reports. |
| **Controls** | Access restricted to a reduced list of specifically authorized people; access audit required; encryption mandatory; prohibited on any portable device without specific authorization; regulated access to physical or digital documents. |
| **Label in documents** | `HIGHLY CONFIDENTIAL` |

---

## How to handle sensitive information

### Email
- **Level 3–4:** Use the "Encrypt" or "Confidential" button in Outlook before sending.
- **Level 4:** Avoid email if possible; use secure collaboration platforms (Teams Secure Channels).
- External sending of Level 3–4 information requires written authorization from a manager.

### Files and documents
- **Level 3–4:** Store only in authorized SharePoint spaces or enterprise OneDrive.
- Do not save in personal desktop folders, personal cloud, or USB drives (except IT-approved encrypted ones).
- Apply sensitivity labels in Microsoft 365 (available from the toolbar in Office).

### Meetings and conversations
- Do not discuss Level 3–4 information in public or easily overheard places.
- For virtual meetings with external parties discussing confidential topics: enable lobbies in Teams, do not record without consent.

### Printing
- Level 3–4 documents should be printed on protected printers (PIN required at the printer).
- Destroy using shredders available in IT areas and HHRR.

---

## Microsoft Purview information protection labels

Techint uses **Microsoft Purview** for automated classification:

| Label | Applies to |
|---|---|
| Public | Level 1 documents |
| Internal Use Only | Level 2 documents |
| Confidential | Level 3 documents |
| Highly Confidential | Level 4 documents |

When you apply a label in Office:
1. Open the document → **Home → Sensitivity** (or Information Protection button).
2. Select the appropriate level.
3. The document will automatically have appropriate encryption and access restrictions applied.

---

## Reporting a classification violation

If you observe that someone is mishandling sensitive information:
- **Internal team:** Talk directly with the manager.
- **SOC / Cybersecurity:** `soc@techint.com` (confidential report).
- **Ethics channel:** `https://intranet.techint.com/etica` (anonymous reporting).

---

## Contact

- **IT Security:** `soc@techint.com` / extension #7777
- **DPO (Data Protection Officer):** `dpo@techint.com`
- **Microsoft Purview support:** IT Help Desk extension #5000
