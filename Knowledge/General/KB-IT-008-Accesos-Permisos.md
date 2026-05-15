# KB-IT-008: Solicitud de acceso a sistemas o permisos

**Categoría:** Gestión de Accesos  
**Impacto:** Variable  
**Tiempo estimado de resolución:** 1–3 días hábiles

---

## Descripción del problema / Requerimiento

El usuario necesita acceso a un sistema corporativo, carpeta de red, aplicación o recurso al que actualmente no tiene permisos.

---

## Proceso de solicitud de acceso

Todos los accesos a sistemas corporativos de Techint siguen el proceso de **Gestión de Identidades y Accesos (IAM)** y requieren aprobación del responsable de área.

### Paso 1 — Determinar qué acceso se necesita

Identificar claramente:
- **Sistema**: SAP, SharePoint, carpeta de red, aplicación específica, etc.
- **Tipo de acceso**: solo lectura, lectura/escritura, administrador.
- **Justificación de negocio**: por qué se necesita el acceso.

### Paso 2 — Solicitar aprobación del responsable de área

**El acceso NO puede ser otorgado sin aprobación del responsable directo.**

El proceso estándar:
1. El empleado envía un email a su responsable directo solicitando el acceso.
2. El responsable reenvía la aprobación al equipo de IT: `it-accesos@techint.com`.
3. IT procesa la solicitud en un plazo de **1–3 días hábiles** según el sistema.

### Paso 3 — Usar el Portal de Autoservicio de Accesos (para sistemas habilitados)

Para los siguientes sistemas, el empleado puede solicitar acceso directamente:
- **Microsoft 365 Groups / Teams**: solicitud desde `https://myaccess.microsoft.com`.
- **SharePoint sites**: solicitar acceso desde el propio sitio (botón "Solicitar acceso").
- **Aplicaciones Azure AD**: solicitar desde `https://myapps.microsoft.com` → "Solicitar acceso a una aplicación".

El responsable recibirá la solicitud por email para aprobar o rechazar.

---

## Sistemas y tiempos de aprovisionamiento

| Sistema | Tiempo estimado de aprovisionamiento | Requiere aprobación de |
|---|---|---|
| Microsoft 365 / Azure AD | 4–8 horas | Responsable directo |
| SAP ERP | 2–3 días hábiles | Responsable directo + Finanzas/Control |
| SAP SuccessFactors (RRHH) | 1–2 días hábiles | RRHH |
| SharePoint sitios internos | 1–4 horas | Owner del sitio |
| Carpetas de red (file shares) | 1 día hábil | Responsable directo |
| Sistemas de planta / SCADA | 3–5 días hábiles | Responsable + Seguridad Industrial |
| Citrix / aplicaciones remotas | 1–2 días hábiles | Responsable directo |

---

## Requerimientos urgentes

Si el acceso es urgente (bloquea trabajo crítico de producción o seguridad):
1. Contactar directamente a la mesa de ayuda: `+54 11 4018-XXXX` (opción 1).
2. Indicar el nivel de urgencia y el impacto en el negocio.
3. IT coordinará aprobación express con el responsable de área.

---

## Cuándo escalar a mesa de ayuda

- La solicitud de acceso lleva más de 3 días hábiles sin respuesta.
- Acceso urgente que bloquea operaciones críticas.
- Errores técnicos al activar un acceso ya aprobado.

**Prioridad sugerida:** Media (Normal). Alta si bloquea operaciones.
