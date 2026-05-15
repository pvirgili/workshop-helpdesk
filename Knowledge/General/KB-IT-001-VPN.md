# KB-IT-001: No me puedo conectar a la VPN

**Categoría:** Conectividad  
**Impacto:** Alto  
**Tiempo estimado de resolución:** 15–30 minutos

---

## Descripción del problema

El cliente VPN de Techint (GlobalProtect) no logra establecer conexión, muestra error de autenticación, timeout o simplemente no conecta.

---

## Causas más comunes

1. **Credenciales expiradas o incorrectas** — la contraseña de red cambió recientemente.
2. **Cliente GlobalProtect desactualizado** — versión mínima requerida: 6.2.x.
3. **Conflicto con otra VPN** — Cisco AnyConnect, WireGuard u otra VPN activa en paralelo.
4. **Firewall o antivirus bloqueando el tráfico** — puertos UDP 4501 y 443 deben estar abiertos.
5. **Certificado de máquina vencido** — ocurre en equipos sin sincronización de dominio hace más de 30 días.
6. **DNS corporativo no resuelve el gateway** — ocurre en redes con DNS customizado (hoteles, aeropuertos).

---

## Pasos de diagnóstico y resolución

### Paso 1 — Verificar credenciales

Confirmar que el usuario recuerda su contraseña de red. Si expiró:
- Ir a `https://aka.ms/sspr` (Self-Service Password Reset de Techint).
- Si SSPR no funciona, contactar mesa de ayuda con documento de identidad.

### Paso 2 — Verificar versión del cliente

1. Abrir GlobalProtect → ícono en la bandeja del sistema.
2. Ir a **Acerca de** (About) → verificar versión.
3. Si es anterior a 6.2.0: descargar el instalador actualizado desde el Portal IT:  
   `https://intranet.techint.com/it/vpn-installer`
4. Desinstalar versión anterior → reiniciar → instalar nueva versión.

### Paso 3 — Cerrar otras VPNs activas

1. Verificar en la bandeja del sistema si hay otro cliente VPN activo.
2. Desconectar y deshabilitar cualquier otro cliente VPN.
3. Intentar conectar GlobalProtect nuevamente.

### Paso 4 — Verificar puertos con el router/firewall local

Desde una red corporativa o red de datos del celular (no WiFi del problema):
1. Probar conectar GlobalProtect desde la red de datos del celular como hotspot.
2. Si conecta por hotspot pero no por WiFi → el router o firewall local bloquea los puertos.
3. Solución: usar otra red, o contactar al proveedor de internet para abrir puertos UDP 4501 y TCP 443.

### Paso 5 — Reinstalar el cliente desde cero

1. Desinstalar GlobalProtect desde **Panel de Control → Agregar o quitar programas**.
2. Eliminar carpetas residuales:
   - `C:\Program Files\Palo Alto Networks\GlobalProtect`
   - `C:\ProgramData\Palo Alto Networks`
3. Reiniciar el equipo.
4. Instalar la versión más reciente desde `https://intranet.techint.com/it/vpn-installer`.
5. Al configurar, usar el gateway: `vpn.techint.com`.

### Paso 6 — Renovar certificado de máquina (IT requerido)

Si el equipo lleva más de 30 días sin conectarse al dominio corporativo:
1. Conectar el equipo a la red de oficina (cable o WiFi corporativo).
2. Reiniciar sesión en Windows con credenciales de dominio.
3. Esperar 5 minutos para que la política de grupo (GPO) se aplique.
4. Intentar conectar VPN nuevamente.

---

## Cuándo escalar a mesa de ayuda

- El problema persiste después de todos los pasos anteriores.
- El usuario ve el error: **"Authentication failed – Certificate error"**.
- El equipo fue prestado, reasignado o recuperado de otro usuario.
- El equipo lleva más de 6 meses sin ir a una oficina.

**Prioridad sugerida al escalar:** Alta (el usuario no puede trabajar remotamente).

---

## Información a recopilar al escalar

- Sistema operativo y versión de Windows/macOS.
- Versión de GlobalProtect instalada.
- Mensaje de error exacto (captura de pantalla).
- Red desde la que intenta conectar (WiFi domicilio, datos de celular, hotel, etc.).
- Último día que la VPN funcionó correctamente.
