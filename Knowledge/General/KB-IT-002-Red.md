# KB-IT-002: Sin conexión a internet o red corporativa

**Categoría:** Conectividad  
**Impacto:** Alto  
**Tiempo estimado de resolución:** 10–20 minutos

---

## Descripción del problema

El equipo no tiene acceso a internet, a la red corporativa o la conectividad es muy lenta/inestable.

---

## Causas más comunes

1. Adaptador de red deshabilitado o driver corrupto.
2. Configuración de IP estática incorrecta (el DHCP no asignó dirección).
3. Caché DNS corrompida.
4. Proxy corporativo mal configurado.
5. Cable de red desconectado o dañado (para conexión por cable).
6. Problema con el router/switch de la oficina o domicilio.

---

## Pasos de diagnóstico y resolución

### Paso 1 — Verificar el estado físico de la conexión

**Para conexión por cable:**
- Verificar que el cable RJ45 esté bien conectado al equipo y al switch/router.
- Verificar que el LED del puerto de red esté encendido (verde o ámbar).
- Probar con otro cable si hay disponible.

**Para WiFi:**
- Verificar que el WiFi no esté deshabilitado (tecla Fn+F2 o ícono en bandeja).
- Verificar que el nombre de la red (SSID) sea el correcto: `Techint-Corp` o `Techint-Guest`.

### Paso 2 — Deshabilitar y rehabilitar el adaptador de red

1. Abrir **Administrador de dispositivos** (clic derecho en Inicio → Administrador de dispositivos).
2. Expandir **Adaptadores de red**.
3. Clic derecho en el adaptador → **Deshabilitar dispositivo** → esperar 5 segundos → **Habilitar dispositivo**.
4. Alternativamente desde PowerShell:
   ```powershell
   Disable-NetAdapter -Name "Ethernet" -Confirm:$false
   Start-Sleep -Seconds 5
   Enable-NetAdapter -Name "Ethernet" -Confirm:$false
   ```

### Paso 3 — Renovar dirección IP (DHCP)

Abrir **Símbolo del sistema** como administrador y ejecutar:
```cmd
ipconfig /release
ipconfig /renew
```

Verificar que se asignó una IP válida:
```cmd
ipconfig /all
```
La IP debe estar en el rango `10.x.x.x` o `172.16.x.x` para red corporativa.

### Paso 4 — Limpiar caché DNS

```cmd
ipconfig /flushdns
nbtstat -R
nbtstat -RR
netsh int ip reset
netsh winsock reset
```

Reiniciar el equipo después de estos comandos.

### Paso 5 — Verificar configuración del proxy

1. Ir a **Configuración → Red e Internet → Proxy**.
2. Si está configurado manualmente, verificar que apunte a: `proxy.techint.com:8080`.
3. Si el problema comenzó después de conectarse a una red externa, deshabilitar el proxy temporal manualmente.

### Paso 6 — Verificar con diagnóstico de red de Windows

1. Clic derecho en el ícono de red en la bandeja → **Diagnosticar problemas**.
2. Seguir las instrucciones del asistente.
3. Si el asistente detecta y repara el problema, verificar conectividad abriendo un navegador.

---

## Cuándo escalar a mesa de ayuda

- El problema persiste después de todos los intentos.
- Múltiples equipos en la misma oficina tienen el mismo problema (puede ser el switch o router).
- El adaptador de red no aparece en el Administrador de dispositivos (posible falla de hardware).
- El equipo muestra error: **"No hay hardware de red detectado"**.

**Prioridad sugerida al escalar:** Alta.

---

## Información a recopilar al escalar

- Tipo de conexión: cable o WiFi.
- IP asignada (resultado de `ipconfig /all`).
- Mensaje de error exacto del sistema operativo.
- Si otros equipos en la misma red tienen el mismo problema.
- Resultado del comando `ping 8.8.8.8` (si hay respuesta o no).
