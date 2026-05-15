# Guide: Knowledge Base Setup in Azure AI Search for Microsoft Foundry

> **Context:** This document describes, step by step, how to prepare the Azure AI Search infrastructure that serves as the knowledge base for the workshop agents. When finished, you will have two vector indexes (`index-helpdesk-security` and `index-helpdesk-general`) connected as a single Knowledge Base within Microsoft Foundry.

---

## Prerequisites

- Active Azure subscription with **Owner** or **Contributor + User Access Administrator** permissions
- **Microsoft Foundry** project already created at [https://ai.azure.com](https://ai.azure.com)
- Azure CLI installed (`az --version`) or access to the Azure portal
- Files from the `Knowledge/` folder of this repository available locally

---

## Step 0 — Create the Storage Account and upload the knowledge files

The Storage Account acts as the document source that AI Search will index.

### 0.1 Create the Storage Account

In the Azure portal:

1. Navigate to **Create a resource → Storage account**.
2. Fill in the fields:
   | Field | Suggested value |
   |---|---|
   | Subscription | Your subscription |
   | Resource group | `rg-helpdesk-workshop` |
   | Name | `sthelpdesk<unique_suffix>` (e.g. `sthelpdesk0514`) |
   | Region | East US 2 (or the same region as your Foundry project) |
   | Redundancy | LRS (sufficient for workshop) |
3. On the **Advanced** tab, enable **Hierarchical namespace** only if you plan to use Data Lake Gen2. For this workshop, leave it disabled.
4. Click **Review + create → Create**.

> **Important:** Using the same region for all resources (Storage, AI Search, and Foundry) minimizes latency and avoids data transfer charges.

### 0.2 Create the containers (blobs)

Inside the newly created Storage Account:

1. Go to **Containers → + Container**.
2. Create the `general` container with private access.
3. Repeat and create the `security` container with private access.

### 0.3 Upload the Knowledge Base files

**Option A — From the Azure portal (drag and drop):**

1. Enter the `general` container and upload all files from `Knowledge/General/`:
   - `KB-IT-001-VPN.md`
   - `KB-IT-002-Red.md`
   - `KB-IT-003-Hardware-Mouse-Teclado.md`
   - `KB-IT-004-App-Vacaciones.md`
   - `KB-IT-005-Portal-RRHH.md`
   - `KB-IT-006-Contraseñas.md`
   - `KB-IT-007-Impresoras.md`
   - `KB-IT-008-Accesos-Permisos.md`
   - `KB-IT-009-Renovacion-Equipo.md`
   - `KB-IT-010-Onboarding.md`
2. Enter the `security` container and upload all files from `Knowledge/Security/`:
   - `KB-SEC-001-Phishing.md`
   - `KB-SEC-002-Malware-Ransomware.md`
   - `KB-SEC-003-BYOD-Dispositivos-Personales.md`
   - `KB-SEC-004-Clasificacion-Datos.md`
   - `KB-SEC-005-Backup-Recuperacion.md`
   - `KB-SEC-006-WiFi-Redes-Publicas.md`

**Option B — From the Azure CLI:**

```bash
# Variables
STORAGE_ACCOUNT="sthelpdesk0514"
RG="rg-helpdesk-workshop"

# Upload General files
az storage blob upload-batch \
  --account-name $STORAGE_ACCOUNT \
  --destination general \
  --source ./Knowledge/General \
  --auth-mode login

# Upload Security files
az storage blob upload-batch \
  --account-name $STORAGE_ACCOUNT \
  --destination security \
  --source ./Knowledge/Security \
  --auth-mode login
```

---

## Step 1 — Create the Azure AI Search resource

1. In the Azure portal, navigate to **Create a resource → AI Search** (also appears as *Azure Cognitive Search*).
2. Fill in the fields:
   | Field | Suggested value |
   |---|---|
   | Subscription | Your subscription |
   | Resource group | `rg-helpdesk-workshop` |
   | Service name | `srch-helpdesk-workshop` |
   | Region | **Same as the Storage Account** |
   | Pricing tier | **Basic** (sufficient for workshop; use Standard for production) |
3. Click **Review + create → Create**.

> **Note on pricing tier:** The Basic tier supports up to 15 indexes and 2 GB of index storage, sufficient for the workshop. In production with extensive documents and multiple languages, consider **Standard S1** or higher.

---

## Step 2 — Enable the Managed Identity

For AI Search to securely access the Storage Account — without credentials — it is necessary to enable its **System-Assigned Managed Identity**.

1. Inside the `srch-helpdesk-workshop` resource, go to **Settings → Identity**.
2. On the **System assigned** tab, change the status to **On**.
3. Click **Save** and confirm the dialog.
4. Once saved, note the **Object (principal) ID** that is generated — you will need it to assign permissions on the Storage Account.

---

## Step 3 — RBAC role assignments

For the end-to-end flow to work, three role assignments are needed:

| Who | On which resource | Role | Purpose |
|---|---|---|---|
| AI Search Managed Identity | Storage Account | **Storage Blob Data Reader** | AI Search reads the blob files to index |
| Foundry project Managed Identity | AI Search | **Search Index Data Reader** | Foundry queries the indexes during inference |
| Foundry project Managed Identity | AI Search | **Search Service Contributor** | Foundry can list indexes and knowledge sources |

### 3.1 Role for AI Search to read the Storage Account

1. Go to the **Storage Account** (`sthelpdesk0514`).
2. Select **Access control (IAM) → + Add role assignment**.
3. Search for and select **Storage Blob Data Reader**.
4. Under "Assign access to", select **Managed identity**.
5. Click **+ Select members**, choose the subscription, and filter by **AI Search**; select `srch-helpdesk-workshop`.
6. Save.

### 3.2 Roles for Foundry to access AI Search

First, identify the Managed Identity of the Foundry project:

1. At [https://ai.azure.com](https://ai.azure.com), open your project.
2. Go to **Project settings → Managed identity** and copy the **Object ID**.

Then, in the **AI Search** resource (`srch-helpdesk-workshop`):

1. Select **Access control (IAM) → + Add role assignment**.
2. Assign the **Search Index Data Reader** role to the Foundry project Managed Identity.
3. Repeat and also assign **Search Service Contributor** to the same identity.

> **Why these two roles?** `Search Index Data Reader` allows running queries against the indexes. `Search Service Contributor` allows Foundry to list the available indexes and connect them as Knowledge Sources directly from the Foundry portal.

---

## Step 4 — Define the Embedding and Completion models for Agentic Retrieval

Azure AI Search with **Agentic Retrieval** requires two types of models:

| Model | Purpose | Recommendation |
|---|---|---|
| **Embedding** | Vectorize documents and queries for semantic search | `text-embedding-3-large` (dimension 3072) or `text-embedding-ada-002` (dimension 1536) |
| **Completion / Chat** | Rephrase queries, reason over results, and synthesize answers in the Agentic Retrieval flow | `gpt-4o` or `gpt-4o-mini` |

### 4.1 Verify that the models are deployed in your Foundry project

1. At [https://ai.azure.com](https://ai.azure.com), go to **Model deployments**.
2. Confirm you have active:
   - A deployment of `text-embedding-3-large` (or `text-embedding-ada-002`). Note the **deployment name**.
   - A deployment of `gpt-4o` or `gpt-4o-mini`. Note the **deployment name**.
3. If they don't exist, create them from **+ Deploy model** with sufficient quota (at least 100K TPM for embeddings and 60K TPM for chat in a workshop).

> **Note:** The deployment names are what you will reference when configuring the indexer and Agentic Retrieval in the following steps.

---

## Step 5 — Create indexes and ingest documents from the blob

We will use the **Import and vectorize data** wizard in AI Search, which automatically creates the data source, the vector index, the embedding skillset, and the indexer in a single flow.

### 5.1 Index `index-helpdesk-security` (blob: `security`)

1. In the AI Search resource, click **Import and vectorize data**.
2. **Data source:** Select **Azure Blob Storage**.
   - Choose the Storage Account `sthelpdesk0514`.
   - Select the **`security`** container.
   - Authentication: **Managed identity**.
3. **Vectorize the text:**
   - Select **Azure OpenAI**.
   - Choose the Azure OpenAI resource connected to your Foundry project.
   - Select the embeddings deployment (e.g. `text-embedding-3-large`).
   - Check the **"Enable Agentic Retrieval"** box if it appears, and select the chat deployment (e.g. `gpt-4o-mini`) for query rephrasing.
4. **Index configuration:**
   - Index name: **`index-helpdesk-security`**
   - Leave chunk size at its default value (2048 tokens) or adjust to 512 tokens if documents are short.
5. **Indexer schedule:** Select **Once** for the workshop (in production use **Hourly** or **Daily**).
6. Review and click **Create**.
7. Wait for the indexer to finish. You can view progress at **Indexers → index-helpdesk-security-indexer**. **6 documents** should appear as successfully processed.

### 5.2 Index `index-helpdesk-general` (blob: `general`)

Repeat the exact same process:

1. Click **Import and vectorize data** again.
2. Source: `general` blob from the same Storage Account.
3. Embeddings: same `text-embedding-3-large` deployment.
4. Agentic Retrieval: same `gpt-4o-mini` deployment.
5. Index name: **`index-helpdesk-general`**
6. Run: **Once**.
7. Wait for the indexer to finish. **10 documents** should appear as successfully processed.

### Verify the indexes

In the AI Search resource, go to **Indexes** and confirm that both appear:

| Index | Expected documents |
|---|---|
| `index-helpdesk-security` | 6 |
| `index-helpdesk-general` | 10 |

You can run a test search with the **Search Explorer** using a query like `"VPN not connecting"` on `index-helpdesk-general` to validate that the documents are correctly indexed.

---

## Step 6 — Create the Knowledge Sources in Microsoft Foundry

A **Knowledge Source** in Foundry is the connection between an AI Search index and your project.

1. At [https://ai.azure.com](https://ai.azure.com), open your project.
2. In the left sidebar, go to **Knowledge** (or **Knowledge base**).
3. Click **+ New knowledge source** (or **+ Add knowledge source**).
4. Select **Azure AI Search** as the source type.
5. Choose the `srch-helpdesk-workshop` service from the list (Foundry detects it thanks to the RBAC roles assigned in Step 3).

**Knowledge Source 1 — Security:**

| Field | Value |
|---|---|
| Name | `ks-helpdesk-security` |
| AI Search index | `index-helpdesk-security` |
| Content field | `chunk` (or the text field generated by the indexer) |
| Vector field | `text_vector` (or similar, depending on the index schema) |

Click **Save**.

**Knowledge Source 2 — General:**

Repeat the process:

| Field | Value |
|---|---|
| Name | `ks-helpdesk-general` |
| AI Search index | `index-helpdesk-general` |
| Content field | `chunk` |
| Vector field | `text_vector` |

Click **Save**.

---

## Step 7 — Create the unified Knowledge Base

A **Knowledge Base** in Foundry groups multiple Knowledge Sources under a single resource that agents can use as a retrieval context.

1. Within the **Knowledge** section, click **+ New knowledge base** (or **+ Create knowledge base**).
2. Fill in the fields:
   | Field | Value |
   |---|---|
   | Name | `kb-helpdesk` |
   | Description | `IT HelpDesk knowledge base for the workshop — general incidents and security` |
3. Under **Knowledge Sources**, click **+ Add** and select:
   - `ks-helpdesk-security`
   - `ks-helpdesk-general`
4. Under **Retrieval settings**:
   - **Search mode:** Hybrid (vector + full text) — recommended
   - **Number of results (Top-K):** 5
   - **Agentic Retrieval:** Enabled (uses the `gpt-4o-mini` deployment configured in the indexer)
5. Click **Create**.

### Test the Knowledge Base

From the Knowledge Base itself in Foundry you can run a test query:

- `"The user cannot connect to VPN from home"` → should return results from `index-helpdesk-general`
- `"I received a suspicious email with a link"` → should return results from `index-helpdesk-security`

---

## Summary of created resources

| Resource | Type | Name |
|---|---|---|
| Storage Account | Azure Storage | `sthelpdesk0514` |
| General container | Blob Container | `general` |
| Security container | Blob Container | `security` |
| Search service | Azure AI Search | `srch-helpdesk-workshop` |
| General index | AI Search Index | `index-helpdesk-general` |
| Security index | AI Search Index | `index-helpdesk-security` |
| General Knowledge Source | Foundry Knowledge Source | `ks-helpdesk-general` |
| Security Knowledge Source | Foundry Knowledge Source | `ks-helpdesk-security` |
| Knowledge Base | Foundry Knowledge Base | `kb-helpdesk` |

---

## Architecture diagram

```
Knowledge/General/*.md ──────┐
                              ▼
                    Azure Blob Storage
Knowledge/Security/*.md ─────┤   ├─ container: general
                              └─ container: security
                                        │
                            (indexer + embeddings)
                            text-embedding-3-large
                                        │
                              Azure AI Search
                         ┌──────────────┴──────────────┐
               index-helpdesk-general     index-helpdesk-security
                         └──────────────┬──────────────┘
                                        │
                              Microsoft Foundry
                         ┌──────────────┴──────────────┐
                  ks-helpdesk-general         ks-helpdesk-security
                         └──────────────┬──────────────┘
                                        │
                                  kb-helpdesk
                                        │
                              Incidents Agent
                           (gpt-4o + Agentic Retrieval)
```

---

## Common troubleshooting

| Symptom | Probable cause | Solution |
|---|---|---|
| Indexer fails with 403 error | AI Search Managed Identity does not have the `Storage Blob Data Reader` role on the Storage Account | Review Step 3.1 |
| Foundry does not list the AI Search service | Foundry Managed Identity does not have `Search Service Contributor` on the AI Search resource | Review Step 3.2 |
| Indexes appear empty (0 documents) | Files were not uploaded to the correct container | Verify that the `.md` files are in `general/` and `security/` respectively |
| Agent responses do not use the KB | The Knowledge Base is not associated with the agent in Foundry | Open the agent → Knowledge tab → add `kb-helpdesk` |
| Quota error on the embeddings model | The `text-embedding-3-large` deployment has insufficient quota | Increase TPM in **Model deployments** or use `text-embedding-ada-002` |
