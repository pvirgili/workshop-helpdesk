# KB-SEC-004: Clasificación de información y manejo de datos sensibles

**Categoría:** Ciberseguridad / Gobernanza de datos  
**Impacto:** Alto  
**Tiempo estimado de resolución:** N/A (política permanente)

---

## Descripción

Todos los empleados de Techint deben clasificar y manejar la información corporativa según su nivel de sensibilidad. Esta política aplica a documentos, correos, archivos en SharePoint/OneDrive, presentaciones y cualquier dato generado o recibido en el contexto laboral.

---

## Niveles de clasificación

| Nivel | Etiqueta | Color | Descripción | Ejemplos |
|---|---|---|---|---|
| **1 — Público** | `PÚBLICO` | 🟢 Verde | Información destinada a ser compartida externamente | Comunicados de prensa, información en la web pública, folletos comerciales |
| **2 — Interno** | `INTERNO` | 🟡 Amarillo | Información para uso dentro de Techint, sin restricción por área | Newsletters internos, políticas generales, organigramas |
| **3 — Confidencial** | `CONFIDENCIAL` | 🟠 Naranja | Información sensible, acceso limitado a áreas específicas | Reportes financieros, datos de clientes, planes de negocio, contratos |
| **4 — Restringido** | `RESTRINGIDO` | 🔴 Rojo | Información altamente sensible, acceso mínimo necesario | Datos de M&A, información de patentes antes de registro, datos salariales individuales, auditorías internas |

---

## Cómo clasificar documentos

### En Microsoft Office (Word, Excel, PowerPoint)

1. Abrir el documento.
2. En la barra superior, hacer clic en **"Sensitivity"** (Sensibilidad).
3. Seleccionar la etiqueta correspondiente: Público, Interno, Confidencial o Restringido.
4. La etiqueta se aplicará automáticamente como:
   - Marca de agua visual en el documento.
   - Encabezado/pie de página con la clasificación.
   - Metadata protegida (Azure Information Protection).

### En correos de Outlook

1. Al redactar un correo, hacer clic en **"Sensitivity"** en la barra superior.
2. Seleccionar la clasificación.
3. Para correos **Confidencial** o **Restringido**:
   - Se activa automáticamente el cifrado (Azure RMS).
   - Se bloquea la opción de reenvío (para nivel Restringido).
   - Se bloquea la copia a direcciones externas.

### En SharePoint y OneDrive

1. Seleccionar el archivo o carpeta.
2. Clic en **"Detalles"** (panel derecho).
3. En **"Sensitivity label"**, seleccionar la etiqueta.
4. Los permisos se ajustarán automáticamente según la clasificación.

---

## Reglas de manejo por nivel

### Público
- ✅ Se puede compartir externamente sin restricción.
- ✅ Se puede publicar en redes sociales corporativas.
- ✅ No requiere cifrado.

### Interno
- ✅ Se puede compartir dentro de Techint sin restricción.
- ⚠️ No compartir externamente sin aprobación del área de Comunicaciones.
- ✅ No requiere cifrado obligatorio.

### Confidencial
- ⚠️ Solo compartir con personas que necesiten la información para su trabajo.
- ❌ No compartir externamente sin aprobación del dueño de la información y Legal.
- ✅ Cifrado automático en tránsito y en reposo.
- ❌ No imprimir sin justificación (se registra en logs de auditoría).
- ❌ No almacenar en dispositivos USB no cifrados.

### Restringido
- ⚠️ Acceso solo con aprobación explícita del responsable del dato.
- ❌ No compartir externamente bajo ninguna circunstancia sin aprobación del CISO.
- ✅ Cifrado obligatorio en todo momento.
- ❌ No imprimir.
- ❌ No almacenar fuera de SharePoint/OneDrive corporativo.
- ❌ No discutir en áreas públicas, cafetería o transportes.
- ✅ Auditoría completa de accesos habilitada.

---

## Etiquetado por defecto

- Todos los documentos nuevos creados en Office 365 tienen etiqueta **"Interno"** por defecto.
- Los correos nuevos tienen etiqueta **"Interno"** por defecto.
- El usuario **debe** cambiar la etiqueta si el contenido requiere mayor o menor clasificación.

---

## Incumplimiento

El mal manejo de información clasificada puede resultar en:

1. **Primer incidente:** Capacitación obligatoria + notificación al gerente.
2. **Segundo incidente:** Revisión con RRHH + restricción temporal de accesos.
3. **Incidentes graves:** Según el Código de Conducta de Techint, puede derivar en sanciones disciplinarias.

---

## Preguntas frecuentes

**¿Qué pasa si envío un correo Confidencial a alguien externo por error?**  
Si el correo tiene etiqueta Confidencial, el cifrado impide que el externo lo lea sin aprobación. Notificar al SOC igualmente para registrar el incidente.

**¿Puedo guardar documentos Confidenciales en mi escritorio local?**  
No. Los documentos Confidenciales y Restringidos deben almacenarse en OneDrive/SharePoint donde se aplican las políticas de DLP y backup automático.

**¿Las etiquetas aplican a archivos en Google Drive o Dropbox?**  
Techint no autoriza el uso de Google Drive, Dropbox ni servicios de almacenamiento cloud externos para datos corporativos. Solo se permite OneDrive for Business y SharePoint.

---

## Contacto

- **Equipo de Gobernanza de Datos:** `datos@techint.com`
- **CISO Office:** `ciso@techint.com`
- **Capacitación:** módulo "Clasificación de Datos" en `https://intranet.techint.com/learning`
