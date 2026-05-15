# KB-IT-004: Error al acceder al Sistema de Gestión de Vacaciones (HR Vacaciones)

**Categoría:** Aplicaciones Internas  
**Impacto:** Medio  
**Tiempo estimado de resolución:** 5–20 minutos

---

## Descripción del problema

El usuario no puede acceder al portal de gestión de vacaciones y licencias de Techint (`https://vacaciones.techint.com`). Los errores más frecuentes son: error 403 Acceso denegado, pantalla en blanco, bucle de inicio de sesión o mensaje de sesión expirada.

---

## Causas más comunes

1. **Error 403 – Acceso denegado**: la sesión de Azure AD expiró o el usuario no tiene la licencia de sistema asignada.
2. **Bucle de login / redirige continuamente**: cookies o caché del navegador corrompidas.
3. **Pantalla en blanco o no carga**: extensiones del navegador bloquean el contenido.
4. **"Your account is not enabled for this application"**: el usuario no tiene asignado el rol en Azure AD Enterprise Application.
5. **MFA solicitado repetidamente**: dispositivo no registrado como de confianza.

---

## Pasos de diagnóstico y resolución

### Paso 1 — Limpiar caché y cookies del navegador

**En Microsoft Edge:**
1. Presionar `Ctrl + Shift + Delete`.
2. Rango de tiempo: **Todo el tiempo**.
3. Marcar: Historial, Cookies y datos de sitio, Archivos en caché.
4. Clic en **Borrar ahora**.
5. Cerrar y reabrir el navegador.
6. Intentar acceder nuevamente a `https://vacaciones.techint.com`.

**En Google Chrome:**
1. Mismo atajo `Ctrl + Shift + Delete`.
2. Mismos pasos.

### Paso 2 — Probar en modo incógnito / privado

1. Abrir Edge: `Ctrl + Shift + N` | Chrome: `Ctrl + Shift + N`.
2. Navegar a `https://vacaciones.techint.com`.
3. Si funciona en modo incógnito → el problema está en las extensiones o caché (ver Paso 3).
4. Si tampoco funciona en modo incógnito → pasar al Paso 4.

### Paso 3 — Deshabilitar extensiones del navegador

1. En Edge: `edge://extensions/` | Chrome: `chrome://extensions/`.
2. Deshabilitar todas las extensiones temporalmente.
3. Recargar la página de vacaciones.
4. Si funciona, habilitar extensiones de a una para identificar cuál bloquea el acceso.
   - Extensiones que suelen causar problemas: uBlock Origin, AdGuard, Privacy Badger.

### Paso 4 — Cerrar sesión de Azure AD y volver a iniciar

1. Ir a `https://myapps.microsoft.com`.
2. Clic en el avatar/nombre de usuario (arriba a la derecha) → **Cerrar sesión**.
3. Cerrar el navegador completamente (revisar que no haya ventanas abiertas en la barra de tareas).
4. Reabrir navegador e ir a `https://vacaciones.techint.com`.
5. Iniciar sesión nuevamente con las credenciales corporativas.

### Paso 5 — Verificar sesión SSO en `portal.office.com`

1. Ir a `https://portal.office.com` y verificar que el inicio de sesión funcione correctamente.
2. Si `portal.office.com` tampoco funciona, el problema es de las credenciales (ver KB-IT-006-Contraseñas).

---

## Cuándo escalar a mesa de ayuda

- Error **403** persiste después de limpiar caché y cerrar sesión.
- Mensaje: **"Your account is not enabled for this application"** → IT debe asignar el rol en Azure AD (no es resolvible por el usuario).
- El usuario es nuevo o fue recientemente promovido/transferido de área (puede necesitar aprovisionamiento de acceso).
- Las aprobaciones de vacaciones están pendientes y hay urgencia de negocio.

**Prioridad sugerida al escalar:** Media.

---

## Información a recopilar al escalar

- URL exacta y mensaje de error completo (captura de pantalla).
- Navegador y versión.
- Usuario de Azure AD (correo electrónico corporativo).
- Si el problema comenzó recientemente o siempre fue así.
- Si hay algún cambio reciente: contraseña nueva, equipo nuevo, cambio de área.
