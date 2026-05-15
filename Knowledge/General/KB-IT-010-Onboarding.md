# KB-IT-010: Onboarding IT para empleados nuevos

**Categoría:** Onboarding  
**Impacto:** Alto  
**Tiempo estimado de resolución:** 1–3 días hábiles de preparación

---

## Descripción

Guía para el equipo de IT y para nuevos empleados sobre el proceso de aprovisionamiento de equipos y accesos en el primer día de trabajo en Techint.

---

## Proceso pre-onboarding (IT)

IT debe recibir la solicitud de provisioning con al menos **5 días hábiles de anticipación** antes del ingreso del nuevo empleado.

La solicitud debe incluir:
- Nombre completo
- Email corporativo asignado por RRHH
- Área y proyecto asignado
- País y sede
- Responsable directo
- Fecha de inicio
- Perfil de equipo requerido (ver KB-IT-009)

---

## Checklist para el nuevo empleado — Primer día

### Equipo y acceso básico

- [ ] Recibir el equipo corporativo configurado.
- [ ] Iniciar sesión con las credenciales temporales enviadas por email a la casilla personal.
- [ ] Cambiar la contraseña temporal al primer inicio de sesión (requisito de seguridad).
- [ ] Registrar métodos de autenticación MFA en `https://aka.ms/MFASetup`:
  - App Microsoft Authenticator (recomendado).
  - Teléfono celular (SMS o llamada como backup).

### Registrar métodos SSPR

Ir a `https://aka.ms/ssprsetup` para registrar los métodos de recuperación de contraseña:
- Email alternativo personal (recomendado como backup).
- Teléfono celular.

### Instalar el cliente VPN

1. Descargar GlobalProtect desde: `https://intranet.techint.com/it/vpn-installer`.
2. Instalar y configurar con gateway: `vpn.techint.com`.
3. Iniciar sesión con credenciales corporativas.

### Aplicaciones corporativas

Todas las aplicaciones licenciadas se encuentran en `https://myapps.microsoft.com`:
- Microsoft 365 (Outlook, Teams, SharePoint, OneDrive).
- Sistema de gestión de vacaciones.
- Portal de RRHH (SAP SuccessFactors) — acceso se activa en las primeras 48hs.
- SAP ERP — según perfil de la posición.

### Configurar email en Outlook

El email corporativo es automáticamente aprovisionado. Abrir Outlook → seguir el asistente de configuración automática.

---

## Accesos estándar que todo empleado recibe el primer día

| Sistema | Acceso provisionado automáticamente |
|---|---|
| Microsoft 365 (Exchange, Teams, SharePoint, OneDrive) | ✅ Día 1 |
| Intranet de Techint | ✅ Día 1 |
| Sistema de gestión de vacaciones | ✅ Día 1 |
| SAP SuccessFactors (RRHH) | ✅ 48hs |
| VPN GlobalProtect | ✅ Día 1 |
| SAP ERP / sistemas operativos | ⚠️ Según rol, requiere solicitud |
| Acceso a sistemas de planta | ⚠️ Requiere capacitación de seguridad |

---

## Si algo no funciona el primer día

1. Contactar al responsable directo o a la mesa de ayuda IT.
2. Mesa de ayuda IT tiene prioridad alta para incidencias de empleados nuevos.
3. Teléfono: `+54 11 4018-XXXX` (opción 1 → opción 3: nuevos empleados).
4. Email: `it-newjoiner@techint.com`.

---

## Cuándo el problema es un incidente vs. un requerimiento

| Situación | Tipo |
|---|---|
| No llega el equipo el primer día | **Incidente** (urgente) |
| El equipo llegó pero no está configurado | **Incidente** |
| No puede iniciar sesión con las credenciales temporales | **Incidente** |
| Necesita acceso a un sistema adicional del estándar | **Requerimiento** |
| Necesita equipo adicional (segunda pantalla, headset) | **Requerimiento** |
