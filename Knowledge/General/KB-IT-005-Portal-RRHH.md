# KB-IT-005: Acceso al Portal de RRHH (SAP SuccessFactors)

**Categoría:** Aplicaciones Internas  
**Impacto:** Medio  
**Tiempo estimado de resolución:** 10–20 minutos

---

## Descripción del problema

El usuario no puede acceder al portal de Recursos Humanos (`https://hcm.techint.com` / SAP SuccessFactors), recibe error de inicio de sesión, acceso denegado o el portal no carga correctamente.

---

## Causas más comunes

1. **Contraseña expirada** en SAP SuccessFactors (sistema independiente de Azure AD).
2. **Sesión activa en otro dispositivo** que bloquea nuevo inicio de sesión.
3. **Licencia de SAP no asignada** (usuarios nuevos o transferidos).
4. **Incompatibilidad del navegador** — SAP SuccessFactors requiere Microsoft Edge o Chrome.
5. **Configuración de zona horaria incorrecta** — puede causar errores de autenticación SAML.

---

## Pasos de diagnóstico y resolución

### Paso 1 — Verificar el navegador

SAP SuccessFactors requiere:
- **Microsoft Edge** (versión 109 o superior) ✅
- **Google Chrome** (versión 109 o superior) ✅
- **Mozilla Firefox** ❌ No soportado
- **Internet Explorer** ❌ No soportado

Cambiar al navegador correcto antes de continuar.

### Paso 2 — Deshabilitar el modo compatibilidad y extensiones

En Edge:
1. Ir a `edge://settings/defaultBrowser`.
2. Verificar que el modo IE esté desactivado para `hcm.techint.com`.
3. Deshabilitar extensiones (mismo procedimiento que KB-IT-004).

### Paso 3 — Limpiar caché

1. `Ctrl + Shift + Delete` → borrar todo el historial para "Todo el tiempo".
2. Reabrir el navegador.
3. Ir a `https://hcm.techint.com`.

### Paso 4 — Intentar restablecer contraseña de SAP

SAP SuccessFactors tiene su propio sistema de contraseñas (separado de Windows/Azure AD):
1. En la pantalla de login de SAP, clic en **"¿Olvidaste tu contraseña?"**.
2. Ingresar el email corporativo.
3. Revisar el correo corporativo para el enlace de restablecimiento (puede tardar hasta 5 minutos).
4. Si no llega el correo, revisar la carpeta de spam o correo no deseado.

### Paso 5 — Verificar zona horaria del equipo

1. Clic derecho en el reloj del sistema → **Ajustar fecha y hora**.
2. Verificar que la zona horaria sea correcta (por ejemplo: `(UTC-03:00) Buenos Aires` para Argentina).
3. Activar **Establecer zona horaria automáticamente**.

---

## Cuándo escalar a mesa de ayuda

- El usuario es nuevo (menos de 30 días) y nunca ha podido acceder.
- Mensaje: **"Your account does not have access to this company"**.
- El usuario tiene cambio de área o posición reciente y perdió accesos previos.
- El acceso fue revocado por inactividad y necesita reactivación por RRHH.

**Nota:** La asignación de licencias SAP SuccessFactors requiere aprobación del área de RRHH. IT no puede asignar acceso sin ese aval.

**Prioridad sugerida al escalar:** Media.

---

## Información a recopilar al escalar

- Email corporativo del usuario.
- Mensaje de error completo y captura de pantalla.
- Área/División en Techint.
- Si es usuario nuevo, fecha de ingreso.
- Si el problema es de acceso históricamente o es nuevo.
