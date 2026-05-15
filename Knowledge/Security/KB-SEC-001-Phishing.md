# KB-SEC-001: Cómo identificar y reportar un correo de phishing

**Categoría:** Ciberseguridad  
**Impacto:** Crítico  
**Tiempo estimado de resolución:** 5–10 minutos

---

## Descripción del problema

El usuario recibe un correo electrónico sospechoso que podría ser un intento de phishing: suplantación de identidad para robar credenciales, datos financieros o instalar malware.

---

## Señales de un correo de phishing

1. **Remitente sospechoso** — el dominio no coincide con la empresa supuesta (ej: `soporte@techint-seguridad.xyz` en lugar de `@techint.com`).
2. **Urgencia excesiva** — mensajes como "Su cuenta será bloqueada en 2 horas", "Acción inmediata requerida".
3. **Enlaces dudosos** — al pasar el mouse sobre el enlace, la URL real no coincide con el texto visible.
4. **Adjuntos inesperados** — archivos `.zip`, `.exe`, `.docm` (macros), `.html` de remitentes no esperados.
5. **Errores de ortografía y gramática** — textos mal traducidos o con errores evidentes.
6. **Solicitud de credenciales** — ningún departamento de Techint pedirá contraseñas por email.
7. **Remitente interno pero contenido inusual** — puede ser una cuenta comprometida.

---

## Qué hacer si se recibe un correo sospechoso

### Paso 1 — NO interactuar

- **No hacer clic** en ningún enlace del correo.
- **No abrir** archivos adjuntos.
- **No responder** al remitente.
- **No reenviar** el correo a compañeros (para evitar propagación accidental).

### Paso 2 — Reportar con el botón de Outlook

1. En Outlook (escritorio o web), seleccionar el correo sospechoso.
2. En la barra de herramientas, hacer clic en **"Reportar phishing"** (icono de escudo con señal de alerta).
3. Confirmar el reporte. El correo será enviado automáticamente al equipo de seguridad (SOC) para análisis.
4. El correo se moverá automáticamente a la carpeta de correo no deseado.

### Paso 3 — Si no se ve el botón de reporte

1. Reenviar el correo **como adjunto** a: `soc@techint.com`
   - En Outlook: clic derecho sobre el correo → **Reenviar como dato adjunto**.
2. Agregar en el cuerpo: "Reporto este correo como sospechoso de phishing."
3. Eliminar el correo original de la bandeja de entrada.

### Paso 4 — Si se hizo clic en un enlace o se ingresaron credenciales

**Acción inmediata (los primeros 15 minutos son críticos):**

1. **Cambiar la contraseña** inmediatamente desde `https://aka.ms/sspr`.
2. **Llamar al SOC** al interno **#7777** o enviar mensaje a `soc-urgente@techint.com` con asunto "Compromiso de cuenta".
3. **No apagar el equipo** — el SOC puede necesitar analizarlo en caliente.
4. **Desconectar de la red** si se sospecha de malware (quitar cable de red o desactivar WiFi).
5. El SOC realizará:
   - Revocación de sesiones activas en Azure AD.
   - Revisión de reglas de reenvío en el buzón.
   - Análisis forense del dispositivo si se descargó un archivo.

---

## Campañas de simulación de phishing

Techint realiza **simulaciones trimestrales de phishing** a través de la plataforma KnowBe4:

- Si el usuario cae en una simulación, **no hay sanción**, pero se le asigna un módulo de capacitación obligatorio de 15 minutos.
- Los resultados son anónimos a nivel individual y se reportan de forma agregada por departamento.
- Los empleados que reportan correctamente las simulaciones acumulan **puntos de reconocimiento** en el programa de ciberseguridad.

---

## Estadísticas de referencia (Techint 2025)

| Métrica | Valor |
|---|---|
| Correos de phishing bloqueados por mes | ~45,000 |
| Tasa de clic en simulaciones (Q4 2025) | 8.3% |
| Tiempo promedio de reporte por usuarios | 4.2 minutos |
| Cuentas comprometidas por phishing (2025) | 12 casos |

---

## Contacto

- **SOC (Security Operations Center):** interno #7777 / `soc@techint.com`
- **Reporte de phishing (automatizado):** botón "Reportar phishing" en Outlook
- **Horario SOC:** 24/7 (emergencias) / Lun–Vie 8:00–20:00 (consultas generales)
