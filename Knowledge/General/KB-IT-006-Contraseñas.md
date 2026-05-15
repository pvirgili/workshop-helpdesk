# KB-IT-006: Reseteo de contraseña y problemas de acceso a cuenta

**Categoría:** Seguridad / Identidad  
**Impacto:** Alto  
**Tiempo estimado de resolución:** 5–15 minutos

---

## Descripción del problema

El usuario no puede iniciar sesión en su cuenta de Windows o en aplicaciones corporativas por contraseña incorrecta, contraseña expirada, cuenta bloqueada o problemas con MFA (autenticación multifactor).

---

## Tipos de problemas y soluciones

### Caso A: Contraseña de Windows/Azure AD

#### Autoservicio (sin IT) — SSPR
Techint tiene habilitado el **Self-Service Password Reset (SSPR)**:

1. Ir a `https://aka.ms/sspr` desde cualquier navegador.
2. Ingresar el email corporativo (ej: `nombre.apellido@techint.com`).
3. Verificar identidad con:
   - Teléfono registrado (SMS o llamada), O
   - App Microsoft Authenticator, O
   - Email alternativo.
4. Crear una nueva contraseña que cumpla los requisitos.
5. Esperar 2 minutos antes de intentar iniciar sesión.

**Requisitos de contraseña de Techint:**
- Mínimo 12 caracteres.
- Al menos 1 mayúscula, 1 minúscula, 1 número, 1 carácter especial.
- No puede ser igual a las últimas 8 contraseñas utilizadas.
- No puede contener el nombre de usuario.

#### Si SSPR no funciona
- El usuario no registró métodos de verificación previamente.
- Solución: contactar mesa de ayuda con documento de identidad para reset manual.

---

### Caso B: Cuenta de Windows bloqueada

La cuenta se bloquea después de **5 intentos fallidos** consecutivos por política de seguridad.

**Desbloqueo automático:** La cuenta se desbloquea sola después de **30 minutos**.

**Desbloqueo inmediato:** Solo puede hacerlo el equipo de IT. Contactar mesa de ayuda.

---

### Caso C: MFA — No llega el código o no tengo acceso al teléfono

1. **Intentar con otro método**: en la pantalla de MFA, buscar opción "Usar un método diferente".
2. **Si el teléfono cambió**: contactar mesa de ayuda para registrar el nuevo teléfono.
3. **Si se perdió el teléfono**: escalar con urgencia a IT — se debe deshabilitar el dispositivo perdido en Azure AD inmediatamente por seguridad.

---

### Caso D: Contraseña de SAP / sistemas legacy

Sistemas como SAP SuccessFactors, SAP ERP y otros legados **no sincronizan** con Azure AD.  
Cada sistema tiene su propio mecanismo de recuperación. Ver artículo específico de cada sistema o escalar a mesa de ayuda.

---

## Política de cambio de contraseña

- Las contraseñas expiran cada **90 días**.
- Windows avisa con 14 días de anticipación.
- Si el usuario trabaja 100% remoto y no conecta a VPN, puede que no vea el aviso. Recomendación: cambiar la contraseña antes de que expire usando `Ctrl+Alt+Del → Cambiar contraseña`.

---

## Cuándo escalar a mesa de ayuda

- SSPR no funciona o el usuario no registró métodos de verificación.
- La cuenta está bloqueada y el usuario no puede esperar 30 minutos.
- Se perdió el dispositivo MFA (teléfono).
- Posible compromiso de seguridad (alguien más accedió a la cuenta).

**Prioridad sugerida al escalar:** Crítica si hay posible compromiso de seguridad. Alta en los demás casos.

---

## Información a recopilar al escalar

- Email corporativo.
- Tipo de problema: expiró, bloqueada, olvidó contraseña, MFA.
- Método de verificación MFA disponible.
- Último acceso exitoso (fecha aproximada).
