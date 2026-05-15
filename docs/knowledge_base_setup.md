# Guía: Configuración de Knowledge Base en Azure AI Search para Microsoft Foundry

> **Contexto:** Este documento describe, paso a paso, cómo preparar la infraestructura de Azure AI Search que sirve como base de conocimiento para los agentes del workshop. Al finalizar, tendrás dos índices vectoriales (`index-helpdesk-security` e `index-helpdesk-general`) conectados como una única Knowledge Base dentro de Microsoft Foundry.

---

## Prerequisitos

- Suscripción de Azure activa con permisos de **Owner** o **Contributor + User Access Administrator**
- Proyecto de **Microsoft Foundry** ya creado en [https://ai.azure.com](https://ai.azure.com)
- CLI de Azure instalada (`az --version`) o acceso al portal de Azure
- Archivos de la carpeta `Knowledge/` de este repositorio disponibles localmente

---

## Paso 0 — Crear el Storage Account y subir los archivos de conocimiento

El Storage Account actúa como la fuente de documentos que AI Search va a indexar.

### 0.1 Crear el Storage Account

En el portal de Azure:

1. Navega a **Crear un recurso → Storage account**.
2. Completa los campos:
   | Campo | Valor sugerido |
   |---|---|
   | Suscripción | Tu suscripción |
   | Grupo de recursos | `rg-helpdesk-workshop` |
   | Nombre | `sthelpdesk<sufijo_único>` (ej. `sthelpdesk0514`) |
   | Región | East US 2 (o la misma región de tu Foundry) |
   | Redundancia | LRS (suficiente para workshop) |
3. En la pestaña **Avanzado**, habilita **Hierarchical namespace** solo si planeas usar Data Lake Gen2. Para este workshop, déjalo deshabilitado.
4. Haz clic en **Revisar y crear → Crear**.

> **Importante:** Usar la misma región para todos los recursos (Storage, AI Search y Foundry) minimiza la latencia y evita cargos de transferencia de datos.

### 0.2 Crear los contenedores (blobs)

Dentro del Storage Account recién creado:

1. Ve a **Contenedores → + Contenedor**.
2. Crea el contenedor `general` con acceso privado.
3. Repite y crea el contenedor `security` con acceso privado.

### 0.3 Subir los archivos de la Knowledge Base

**Opción A — Desde el portal de Azure (arrastra y suelta):**

1. Entra al contenedor `general` y sube todos los archivos de `Knowledge/General/`:
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
2. Entra al contenedor `security` y sube todos los archivos de `Knowledge/Security/`:
   - `KB-SEC-001-Phishing.md`
   - `KB-SEC-002-Malware-Ransomware.md`
   - `KB-SEC-003-BYOD-Dispositivos-Personales.md`
   - `KB-SEC-004-Clasificacion-Datos.md`
   - `KB-SEC-005-Backup-Recuperacion.md`
   - `KB-SEC-006-WiFi-Redes-Publicas.md`

**Opción B — Desde la CLI de Azure:**

```bash
# Variables
STORAGE_ACCOUNT="sthelpdesk0514"
RG="rg-helpdesk-workshop"

# Subir archivos General
az storage blob upload-batch \
  --account-name $STORAGE_ACCOUNT \
  --destination general \
  --source ./Knowledge/General \
  --auth-mode login

# Subir archivos Security
az storage blob upload-batch \
  --account-name $STORAGE_ACCOUNT \
  --destination security \
  --source ./Knowledge/Security \
  --auth-mode login
```

---

## Paso 1 — Crear el recurso Azure AI Search

1. En el portal de Azure, navega a **Crear un recurso → AI Search** (también aparece como *Azure Cognitive Search*).
2. Completa los campos:
   | Campo | Valor sugerido |
   |---|---|
   | Suscripción | Tu suscripción |
   | Grupo de recursos | `rg-helpdesk-workshop` |
   | Nombre del servicio | `srch-helpdesk-workshop` |
   | Región | **La misma que el Storage Account** |
   | Plan de tarifa | **Basic** (suficiente para workshop; usa Standard para producción) |
3. Haz clic en **Revisar y crear → Crear**.

> **Nota sobre el plan de tarifa:** El plan Basic soporta hasta 15 índices y 2 GB de almacenamiento de índice, suficiente para el workshop. En producción con documentos extensos y múltiples idiomas, considera **Standard S1** o superior.

---

## Paso 2 — Activar la Identidad Administrada (Managed Identity)

Para que AI Search pueda acceder al Storage Account de forma segura —sin credenciales— es necesario activar su **identidad administrada asignada por el sistema (System-Assigned Managed Identity)**.

1. Dentro del recurso `srch-helpdesk-workshop`, ve a **Configuración → Identidad**.
2. En la pestaña **Asignada por el sistema**, cambia el estado a **Activado**.
3. Haz clic en **Guardar** y confirma el diálogo.
4. Una vez guardado, anota el **Id. de objeto (principal)** que se genera — lo necesitarás para asignar permisos en el Storage Account.

---

## Paso 3 — Asignación de roles RBAC

Para que el flujo funcione de extremo a extremo se necesitan tres asignaciones de roles:

| Quién | Sobre qué recurso | Rol | Para qué |
|---|---|---|---|
| Managed Identity de AI Search | Storage Account | **Storage Blob Data Reader** | AI Search lee los archivos del blob para indexar |
| Managed Identity del proyecto Foundry | AI Search | **Search Index Data Reader** | Foundry consulta los índices durante la inferencia |
| Managed Identity del proyecto Foundry | AI Search | **Search Service Contributor** | Foundry puede listar índices y fuentes de conocimiento |

### 3.1 Rol para que AI Search lea el Storage Account

1. Ve al **Storage Account** (`sthelpdesk0514`).
2. Selecciona **Control de acceso (IAM) → + Agregar asignación de roles**.
3. Busca y selecciona **Storage Blob Data Reader**.
4. En "Asignar acceso a", selecciona **Identidad administrada**.
5. Haz clic en **+ Seleccionar miembros**, elige la suscripción y filtra por **AI Search**; selecciona `srch-helpdesk-workshop`.
6. Guarda.

### 3.2 Roles para que Foundry acceda a AI Search

Primero, identifica la Managed Identity del proyecto Foundry:

1. En [https://ai.azure.com](https://ai.azure.com), abre tu proyecto.
2. Ve a **Configuración del proyecto → Identidad administrada** y copia el **Id. de objeto**.

Luego, en el recurso de **AI Search** (`srch-helpdesk-workshop`):

1. Selecciona **Control de acceso (IAM) → + Agregar asignación de roles**.
2. Asigna el rol **Search Index Data Reader** a la Managed Identity del proyecto Foundry.
3. Repite y asigna también **Search Service Contributor** a la misma identidad.

> **¿Por qué estos dos roles?** `Search Index Data Reader` permite ejecutar consultas sobre los índices. `Search Service Contributor` permite a Foundry listar los índices disponibles y conectarlos como Knowledge Sources desde el propio portal de Foundry.

---

## Paso 4 — Definir los modelos de Embeddings y Completions para Agentic Retrieval

Azure AI Search con **Agentic Retrieval** requiere dos tipos de modelos:

| Modelo | Propósito | Recomendación |
|---|---|---|
| **Embedding** | Vectorizar los documentos y las consultas para búsqueda semántica | `text-embedding-3-large` (dimensión 3072) o `text-embedding-ada-002` (dimensión 1536) |
| **Completion / Chat** | Reformular consultas, razonar sobre los resultados y sintetizar respuestas en el flujo de Agentic Retrieval | `gpt-4o` o `gpt-4o-mini` |

### 4.1 Verificar que los modelos están desplegados en tu proyecto Foundry

1. En [https://ai.azure.com](https://ai.azure.com), ve a **Implementaciones del modelo**.
2. Confirma que tienes activos:
   - Un deployment de `text-embedding-3-large` (o `text-embedding-ada-002`). Anota el **nombre del deployment**.
   - Un deployment de `gpt-4o` o `gpt-4o-mini`. Anota el **nombre del deployment**.
3. Si no existen, créalos desde **+ Implementar modelo** con cuota suficiente (al menos 100K TPM para embeddings y 60K TPM para el chat en un workshop).

> **Nota:** Los nombres de deployment son los que vas a referenciar al configurar el indexador y el Agentic Retrieval en los pasos siguientes.

---

## Paso 5 — Crear los índices e ingerir documentos desde el blob

Usaremos el **Import and vectorize data** wizard de AI Search, que crea automáticamente el data source, el índice vectorial, el skillset de embeddings y el indexador en un solo flujo.

### 5.1 Índice `index-helpdesk-security` (blob: `security`)

1. En el recurso AI Search, haz clic en **Importar y vectorizar datos**.
2. **Origen de datos:** Selecciona **Azure Blob Storage**.
   - Elige el Storage Account `sthelpdesk0514`.
   - Selecciona el contenedor **`security`**.
   - Autenticación: **Identidad administrada**.
3. **Vectorizar el texto:**
   - Selecciona **Azure OpenAI**.
   - Elige el recurso de Azure OpenAI conectado a tu proyecto Foundry.
   - Selecciona el deployment de embeddings (ej. `text-embedding-3-large`).
   - Marca la casilla **"Activar Agentic Retrieval"** si aparece, y selecciona el deployment de chat (ej. `gpt-4o-mini`) para las reformulaciones de consulta.
4. **Configuración del índice:**
   - Nombre del índice: **`index-helpdesk-security`**
   - Deja las opciones de chunk size en su valor predeterminado (2048 tokens) o ajusta a 512 tokens si los documentos son cortos.
5. **Programación del indexador:** Selecciona **Una vez** para el workshop (en producción usa **Cada hora** o **Diariamente**).
6. Revisa y haz clic en **Crear**.
7. Espera a que el indexador termine. Puedes ver el progreso en **Indexadores → index-helpdesk-security-indexer**. Deben aparecer **6 documentos** procesados correctamente.

### 5.2 Índice `index-helpdesk-general` (blob: `general`)

Repite exactamente el mismo proceso:

1. Haz clic nuevamente en **Importar y vectorizar datos**.
2. Origen: blob `general` del mismo Storage Account.
3. Embeddings: mismo deployment de `text-embedding-3-large`.
4. Agentic Retrieval: mismo deployment de `gpt-4o-mini`.
5. Nombre del índice: **`index-helpdesk-general`**
6. Ejecutar: **Una vez**.
7. Espera a que el indexador termine. Deben aparecer **10 documentos** procesados correctamente.

### Verificar los índices

En el recurso AI Search, ve a **Índices** y confirma que aparecen ambos:

| Índice | Documentos esperados |
|---|---|
| `index-helpdesk-security` | 6 |
| `index-helpdesk-general` | 10 |

Puedes hacer una búsqueda de prueba con el **Explorador de búsqueda** usando una consulta como `"VPN no conecta"` sobre `index-helpdesk-general` para validar que los documentos están correctamente indexados.

---

## Paso 6 — Crear las Knowledge Sources en Microsoft Foundry

Una **Knowledge Source** en Foundry es la conexión entre un índice de AI Search y tu proyecto.

1. En [https://ai.azure.com](https://ai.azure.com), abre tu proyecto.
2. En el menú lateral izquierdo, ve a **Knowledge** (o **Base de conocimiento**).
3. Haz clic en **+ Nueva knowledge source** (o **+ Add knowledge source**).
4. Selecciona **Azure AI Search** como tipo de origen.
5. Elige el servicio `srch-helpdesk-workshop` de la lista (Foundry lo detecta gracias a los roles RBAC asignados en el Paso 3).

**Knowledge Source 1 — Seguridad:**

| Campo | Valor |
|---|---|
| Nombre | `ks-helpdesk-security` |
| Índice de AI Search | `index-helpdesk-security` |
| Campo de contenido | `chunk` (o el campo de texto que generó el indexador) |
| Campo de vector | `text_vector` (o similar, según el esquema del índice) |

Haz clic en **Guardar**.

**Knowledge Source 2 — General:**

Repite el proceso:

| Campo | Valor |
|---|---|
| Nombre | `ks-helpdesk-general` |
| Índice de AI Search | `index-helpdesk-general` |
| Campo de contenido | `chunk` |
| Campo de vector | `text_vector` |

Haz clic en **Guardar**.

---

## Paso 7 — Crear la Knowledge Base unificada

Una **Knowledge Base** en Foundry agrupa múltiples Knowledge Sources bajo un único recurso que los agentes pueden usar como contexto de recuperación.

1. Dentro de la sección **Knowledge**, haz clic en **+ Nueva knowledge base** (o **+ Create knowledge base**).
2. Completa los campos:
   | Campo | Valor |
   |---|---|
   | Nombre | `kb-helpdesk` |
   | Descripción | `Base de conocimiento del HelpDesk IT de BCI — incidentes generales y seguridad` |
3. En **Knowledge Sources**, haz clic en **+ Agregar** y selecciona:
   - `ks-helpdesk-security`
   - `ks-helpdesk-general`
4. En **Configuración de recuperación**:
   - **Modo de búsqueda:** Híbrido (vectorial + texto completo) — recomendado
   - **Número de resultados (Top-K):** 5
   - **Agentic Retrieval:** Habilitado (usa el deployment `gpt-4o-mini` configurado en el indexador)
5. Haz clic en **Crear**.

### Probar la Knowledge Base

Desde la propia Knowledge Base en Foundry puedes hacer una consulta de prueba:

- `"El usuario no puede conectarse a la VPN desde casa"` → debería retornar resultados de `index-helpdesk-general`
- `"Recibí un correo sospechoso con un enlace"` → debería retornar resultados de `index-helpdesk-security`

---

## Resumen de recursos creados

| Recurso | Tipo | Nombre |
|---|---|---|
| Storage Account | Azure Storage | `sthelpdesk0514` |
| Contenedor General | Blob Container | `general` |
| Contenedor Security | Blob Container | `security` |
| Servicio de búsqueda | Azure AI Search | `srch-helpdesk-workshop` |
| Índice General | AI Search Index | `index-helpdesk-general` |
| Índice Security | AI Search Index | `index-helpdesk-security` |
| Knowledge Source General | Foundry Knowledge Source | `ks-helpdesk-general` |
| Knowledge Source Security | Foundry Knowledge Source | `ks-helpdesk-security` |
| Knowledge Base | Foundry Knowledge Base | `kb-helpdesk` |

---

## Diagrama de arquitectura

```
Knowledge/General/*.md ──────┐
                              ▼
                    Azure Blob Storage
Knowledge/Security/*.md ─────┤   ├─ contenedor: general
                              └─ contenedor: security
                                        │
                            (indexador + embeddings)
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
                              Agente de Incidentes
                           (gpt-4o + Agentic Retrieval)
```

---

## Troubleshooting frecuente

| Síntoma | Causa probable | Solución |
|---|---|---|
| El indexador falla con error 403 | La Managed Identity de AI Search no tiene el rol `Storage Blob Data Reader` sobre el Storage Account | Revisa el Paso 3.1 |
| Foundry no lista el servicio AI Search | La Managed Identity de Foundry no tiene `Search Service Contributor` en el recurso AI Search | Revisa el Paso 3.2 |
| Los índices aparecen vacíos (0 documentos) | Los archivos no se subieron al contenedor correcto | Verifica que los `.md` están en `general/` y `security/` respectivamente |
| Las respuestas del agente no usan la KB | La Knowledge Base no está asociada al agente en Foundry | Abre el agente → pestaña Knowledge → agrega `kb-helpdesk` |
| Error de cuota en el modelo de embeddings | El deployment de `text-embedding-3-large` tiene cuota insuficiente | Aumenta TPM en **Implementaciones del modelo** o usa `text-embedding-ada-002` |
