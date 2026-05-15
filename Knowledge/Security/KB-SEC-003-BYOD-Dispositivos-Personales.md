# KB-SEC-003: Política de uso de dispositivos personales (BYOD)

**Categoría:** Ciberseguridad / Políticas  
**Impacto:** Medio  
**Tiempo estimado de resolución:** 20–45 minutos (registro inicial)

---

## Descripción

Techint permite el uso de dispositivos personales (smartphones, tablets, laptops) para acceder a recursos corporativos bajo el programa **BYOD (Bring Your Own Device)**, siempre que cumplan con los requisitos de seguridad establecidos.

---

## Dispositivos permitidos y no permitidos

### Permitidos bajo BYOD
- **Smartphones:** iOS 16+ / Android 13+ con parches de seguridad al día.
- **Tablets:** iPad OS 16+ / Android 13+ / Windows 11.
- **Laptops personales:** Windows 11 Pro/Enterprise o macOS 13+ (Ventura o superior).

### No permitidos
- Dispositivos con **root/jailbreak**.
- Sistemas operativos sin soporte (**Windows 10**, Android 12 o inferior, iOS 15 o inferior).
- Dispositivos **compartidos** con otros miembros de la familia.
- **Chromebooks** (no soportan los agentes MDM requeridos).

---

## Proceso de registro de dispositivo BYOD

### Paso 1 — Solicitar el alta BYOD

1. Ir al **Portal de Autoservicio IT:** `https://intranet.techint.com/it/byod`
2. Completar el formulario:
   - Tipo de dispositivo (smartphone, tablet, laptop).
   - Marca, modelo y sistema operativo.
   - Número de serie o IMEI.
   - Aceptación de la **Política de Uso Aceptable (PUA)**.
3. El equipo de IT aprobará la solicitud en **24–48 horas laborales**.

### Paso 2 — Instalar Microsoft Intune Company Portal

1. Descargar **Company Portal** desde la tienda de aplicaciones:
   - iOS: App Store
   - Android: Google Play Store
   - Windows: Microsoft Store
2. Iniciar sesión con la cuenta corporativa de Techint.
3. Seguir el asistente de registro del dispositivo.

### Paso 3 — Cumplir con los requisitos de compliance

El dispositivo debe pasar las siguientes verificaciones automáticas:

| Requisito | Detalle |
|---|---|
| Sistema operativo | Versión mínima según lista de permitidos |
| Cifrado de disco | BitLocker (Windows) / FileVault (macOS) / Cifrado nativo (iOS/Android) |
| PIN/biometría | Mínimo PIN de 6 dígitos o autenticación biométrica |
| Antivirus | Microsoft Defender o antivirus aprobado (solo laptops) |
| Parches de seguridad | Actualizaciones con máximo 30 días de antigüedad |
| Sin root/jailbreak | Verificación automática |

### Paso 4 — Acceder a recursos corporativos

Una vez registrado y en compliance, se puede acceder a:
- **Email corporativo** (Outlook).
- **Microsoft Teams**.
- **OneDrive for Business** (solo lectura desde dispositivos BYOD).
- **SharePoint** (navegador).
- **Aplicaciones aprobadas** en Company Portal.

---

## Restricciones en dispositivos BYOD

### Qué puede hacer IT en el dispositivo personal
- **Aplicar políticas de seguridad** (PIN, cifrado, actualizaciones).
- **Borrado selectivo** de datos corporativos (no datos personales) en caso de:
  - Baja del empleado.
  - Pérdida o robo del dispositivo.
  - Incumplimiento de políticas.

### Qué NO puede hacer IT
- **No puede ver** fotos, mensajes personales, historial de navegación personal.
- **No puede instalar** aplicaciones sin consentimiento.
- **No puede hacer borrado total** del dispositivo (solo borrado selectivo corporativo).

---

## Pérdida o robo de dispositivo BYOD

1. **Notificar inmediatamente** al SOC: interno #7777 / `soc-urgente@techint.com`.
2. El SOC ejecutará **borrado selectivo remoto** de datos corporativos vía Intune.
3. El usuario debe:
   - Cambiar su contraseña corporativa en `https://aka.ms/sspr`.
   - Hacer denuncia policial si fue robo.
   - Bloquear el dispositivo con el servicio del fabricante (Find My iPhone, Find My Device).

---

## Desvinculación del programa BYOD

Para dar de baja un dispositivo del programa BYOD:

1. Abrir **Company Portal** en el dispositivo.
2. Ir a **Dispositivos** → seleccionar el dispositivo → **Quitar**.
3. Esto eliminará:
   - Perfil corporativo y políticas de Intune.
   - Acceso a email, Teams y SharePoint desde ese dispositivo.
   - Datos corporativos almacenados localmente.
4. **Los datos personales no se tocan.**

---

## Preguntas frecuentes

**¿Puedo usar mi laptop personal para trabajar desde casa?**  
Sí, siempre que esté registrada en BYOD y cumpla los requisitos de compliance. Sin embargo, para uso diario se recomienda solicitar un equipo corporativo (ver KB-IT-009).

**¿Techint paga algo por usar mi dispositivo personal?**  
No hay subsidio directo, pero el programa BYOD da acceso a licencias de Microsoft 365 Personal como beneficio.

**¿Puedo usar mi celular personal para MFA sin registrarlo en BYOD?**  
Sí. La app Microsoft Authenticator **no requiere** registro BYOD — solo requiere instalar la app y vincularla a la cuenta corporativa.

---

## Contacto

- **Portal BYOD:** `https://intranet.techint.com/it/byod`
- **Soporte Intune:** `helpdesk@techint.com` / interno #5000
- **SOC (pérdida/robo):** interno #7777
