# KB-SEC-006: Uso seguro de WiFi corporativo, doméstico y redes públicas

**Categoría:** Ciberseguridad / Conectividad  
**Impacto:** Medio  
**Tiempo estimado de resolución:** 10–20 minutos

---

## Descripción

Guía de seguridad para la conexión a redes WiFi desde equipos corporativos y dispositivos BYOD. Cubre las redes WiFi de las oficinas de Techint, redes domésticas (trabajo remoto) y redes públicas (hoteles, aeropuertos, cafeterías).

---

## Redes WiFi en oficinas de Techint

### Redes disponibles

| Red | Uso | Seguridad |
|---|---|---|
| **TECHINT-CORP** | Equipos corporativos unidos al dominio | WPA3-Enterprise (802.1X con certificado de máquina) |
| **TECHINT-GUEST** | Visitantes y dispositivos BYOD no registrados | WPA2-PSK con portal cautivo, internet only |
| **TECHINT-IOT** | Impresoras, displays, dispositivos IoT | Red aislada, sin acceso a recursos corporativos |

### Conexión a TECHINT-CORP

1. Los equipos corporativos se conectan **automáticamente** — el certificado de máquina se instala durante el enrollment.
2. Si no conecta automáticamente:
   - Verificar que el equipo está unido al dominio: `dsregcmd /status` → debe decir "AzureAdJoined: YES".
   - Verificar que el certificado de máquina no expiró: `certlm.msc` → Personal → Certificates → buscar "TECHINT-WIFI".
   - Si el certificado expiró, contactar IT para re-enrollment.

### Conexión a TECHINT-GUEST

1. Conectar a la red **TECHINT-GUEST**.
2. Abrir el navegador — se redirigirá al **portal cautivo**.
3. Opciones de autenticación:
   - **Empleado:** ingresar email corporativo → recibe código temporal por SMS/email.
   - **Visitante:** solicitar credenciales temporales en recepción (validez: 8 horas).
4. **Limitaciones:** Solo internet, sin acceso a servidores internos, SharePoint o impresoras.

---

## Trabajo remoto — Red doméstica

### Requisitos mínimos para la red del hogar

| Aspecto | Requisito |
|---|---|
| **Protocolo WiFi** | WPA2-AES o WPA3 (no usar WEP ni WPA-TKIP) |
| **Contraseña del router** | Mínimo 12 caracteres, no usar la contraseña por defecto del ISP |
| **Firmware del router** | Actualizado a la última versión disponible |
| **SSID (nombre de red)** | No incluir información personal (ej: no usar "Casa-García-5B") |
| **Acceso admin del router** | Cambiar las credenciales por defecto (admin/admin) |
| **Red de invitados** | Recomendado: separar la red de trabajo de la de dispositivos del hogar |

### Verificar seguridad de la red doméstica

1. Acceder a la configuración del router: generalmente `192.168.1.1` o `192.168.0.1`.
2. Verificar el tipo de cifrado en la sección WiFi/Wireless → debe ser **WPA2-AES** o **WPA3**.
3. Si usa WEP o WPA-TKIP: cambiar inmediatamente o contactar al proveedor de internet.

### Usar siempre la VPN

- **Obligatorio:** Conectar la VPN corporativa (GlobalProtect) antes de acceder a cualquier recurso de Techint.
- La VPN cifra todo el tráfico entre el equipo y la red de Techint.
- Ver **KB-IT-001** si hay problemas con la VPN.

---

## Redes públicas (hoteles, aeropuertos, cafeterías)

### Riesgos principales

| Riesgo | Descripción |
|---|---|
| **Man-in-the-Middle (MitM)** | Un atacante intercepta el tráfico entre el equipo y el router |
| **Evil Twin** | Red falsa con el mismo nombre que la red legítima |
| **Sniffing** | Captura de tráfico no cifrado en la red |
| **Portal cautivo malicioso** | Páginas de login falsas que roban credenciales |

### Reglas de seguridad en redes públicas

1. **SIEMPRE activar la VPN** antes de hacer cualquier cosa.
2. **NUNCA acceder a recursos corporativos sin VPN** — ni siquiera para "solo revisar el email".
3. **Verificar el nombre exacto de la red** — preguntar al personal del hotel/aeropuerto.
4. **No aceptar certificados sospechosos** — si el navegador muestra una advertencia de certificado, desconectar inmediatamente.
5. **Desactivar la conexión automática** a redes abiertas:
   - Windows: **Configuración → Red → WiFi → Propiedades de red conocida → Desactivar "Conectar automáticamente"**.
6. **Desactivar la compartición de archivos** en redes públicas:
   - Windows: **Configuración → Red → Perfil de red → Público → Desactivar detección de red y uso compartido**.
7. **Preferir datos móviles** (hotspot del celular) sobre WiFi pública cuando sea posible.

### Si no se puede conectar la VPN desde una red pública

1. Verificar que los puertos UDP 4501 y TCP 443 no estén bloqueados por la red.
2. Si están bloqueados:
   - Usar el **hotspot del celular** como alternativa.
   - Si no hay datos móviles: contactar IT para configurar la VPN en modo TCP (más lento pero evade más restricciones).

---

## Qué hacer si se sospecha de una red comprometida

1. **Desconectar WiFi inmediatamente.**
2. **Cambiar la contraseña corporativa** desde el celular (datos móviles) en `https://aka.ms/sspr`.
3. **Notificar al SOC:** interno #7777 / `soc@techint.com`.
4. Describir:
   - Nombre de la red a la que se conectó.
   - Ubicación (hotel, aeropuerto, nombre del establecimiento).
   - Si se ingresaron credenciales corporativas en alguna página durante la conexión.
5. El SOC verificará si hubo accesos sospechosos a la cuenta.

---

## Checklist rápida para viajeros

- [ ] VPN instalada y probada antes del viaje.
- [ ] Hotspot del celular habilitado como alternativa.
- [ ] Equipo actualizado con los últimos parches de seguridad.
- [ ] Disco cifrado con BitLocker activo.
- [ ] Conocer el número del SOC: **#7777**.
- [ ] Backup reciente de archivos importantes en OneDrive.

---

## Contacto

- **Problemas de VPN:** ver KB-IT-001 / `helpdesk@techint.com` / interno #5000
- **SOC (incidentes de seguridad):** interno #7777 / `soc@techint.com`
- **Configuración de red doméstica:** `helpdesk@techint.com`
