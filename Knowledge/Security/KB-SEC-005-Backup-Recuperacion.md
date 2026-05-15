# KB-SEC-005: Backup y recuperación de archivos

**Categoría:** Ciberseguridad / Continuidad  
**Impacto:** Alto  
**Tiempo estimado de resolución:** 5–60 minutos (según tipo de recuperación)

---

## Descripción del problema

El usuario necesita recuperar archivos eliminados, versiones anteriores de un documento, o restaurar datos después de un incidente (borrado accidental, corrupción, ransomware).

---

## Política de backup de Techint

### Datos en la nube (OneDrive / SharePoint)

| Aspecto | Detalle |
|---|---|
| **Frecuencia de backup** | Continuo (cada cambio se versiona automáticamente) |
| **Retención de versiones** | 500 versiones por archivo |
| **Papelera de reciclaje (1ª etapa)** | 93 días |
| **Papelera de reciclaje (2ª etapa)** | 93 días adicionales (solo IT puede acceder) |
| **Retención total de archivos eliminados** | 186 días (≈ 6 meses) |
| **Backup independiente (Veeam)** | Backup diario, retención 1 año |

### Datos en el equipo local

| Aspecto | Detalle |
|---|---|
| **Carpeta Documentos / Escritorio** | Sincronizada automáticamente con OneDrive (Known Folder Move) |
| **Otras carpetas locales** | ⚠️ **NO tienen backup**. El usuario es responsable. |
| **Disco D: o particiones secundarias** | ⚠️ **NO tienen backup**. |
| **Imagen del sistema** | Disponible para reimagen vía SCCM (último baseline + apps estándar) |

### Datos en carpetas compartidas de red (file servers)

| Aspecto | Detalle |
|---|---|
| **Frecuencia** | Backup incremental cada 4 horas (Veeam) |
| **Retención** | 30 días (diarios) + 12 meses (mensuales) + 3 años (anuales) |
| **RPO (Recovery Point Objective)** | 4 horas máximo |
| **Shadow Copies** | Habilitadas cada 2 horas en días laborales |

---

## Recuperar archivos eliminados

### Caso A: Archivo eliminado de OneDrive o SharePoint (últimos 93 días)

1. Ir a **OneDrive** (web: `https://techint-my.sharepoint.com`) o **SharePoint**.
2. En el menú lateral izquierdo, hacer clic en **"Papelera de reciclaje"**.
3. Buscar el archivo eliminado.
4. Seleccionar → **"Restaurar"**.
5. El archivo vuelve a su ubicación original.

### Caso B: Archivo eliminado hace más de 93 días (papelera 2ª etapa)

1. Contactar a IT: `helpdesk@techint.com` / interno #5000.
2. Proporcionar:
   - Nombre del archivo (aproximado).
   - Ubicación original (OneDrive personal o sitio de SharePoint).
   - Fecha aproximada de eliminación.
3. IT accederá a la papelera de 2ª etapa o al backup de Veeam.
4. **SLA:** Restauración dentro de 4 horas laborales.

### Caso C: Archivo local eliminado (no sincronizado con OneDrive)

1. Verificar la **Papelera de reciclaje de Windows** en el escritorio.
2. Si no está ahí y la carpeta estaba en una unidad de red (ej: `\\server\compartida`):
   - Clic derecho sobre la carpeta → **"Propiedades"** → pestaña **"Versiones anteriores"** (Shadow Copies).
   - Seleccionar la versión más reciente antes del borrado → **"Restaurar"**.
3. Si no hay Shadow Copies disponibles: contactar a IT para restauración desde backup.

---

## Recuperar versiones anteriores de un documento

### OneDrive / SharePoint

1. Ir al archivo en OneDrive o SharePoint.
2. Clic derecho → **"Historial de versiones"** (Version History).
3. Se mostrará la lista de versiones con fecha, hora y autor del cambio.
4. Seleccionar la versión deseada:
   - **"Restaurar"** → reemplaza la versión actual.
   - **"Abrir"** → ver la versión sin reemplazar (para comparar).

### Microsoft Office (Word, Excel, PowerPoint)

1. Abrir el archivo.
2. **Archivo** → **Información** → **Historial de versiones**.
3. Seleccionar la versión anterior para visualizarla.
4. Usar **"Restaurar"** o copiar manualmente el contenido necesario.

---

## Recuperación ante desastre (ransomware, corrupción masiva)

En caso de incidente grave que afecte múltiples archivos:

1. **Notificar al SOC** inmediatamente (ver KB-SEC-002).
2. El SOC coordinará con el equipo de infraestructura la restauración masiva.
3. **Opciones de restauración:**
   - **OneDrive:** Restauración completa del OneDrive a un punto en el tiempo (últimos 30 días) usando la función "Restore your OneDrive".
   - **SharePoint:** Restauración a nivel de sitio por el equipo de IT.
   - **File servers:** Restauración desde backup de Veeam (RPO: 4 horas).
4. **SLA para restauración masiva:** 4–24 horas según alcance del incidente.

---

## Buenas prácticas para proteger los datos

1. **Guardar TODO en OneDrive o SharePoint** — no en carpetas locales fuera de Documentos/Escritorio.
2. **No almacenar archivos importantes solo en el escritorio** si Known Folder Move no está habilitado (verificar con IT).
3. **No usar USBs como backup** — no son confiables y no tienen control de versiones.
4. **Verificar que la sincronización de OneDrive funcione** — el ícono azul de nube en la bandeja del sistema debe estar activo.
5. **Para proyectos críticos**, usar SharePoint con biblioteca de documentos versionada.

---

## Contacto

- **Restauración de archivos:** `helpdesk@techint.com` / interno #5000
- **SOC (incidentes de seguridad):** interno #7777
- **Portal de autoservicio OneDrive:** `https://techint-my.sharepoint.com`
