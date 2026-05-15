# KB-IT-003: El mouse o teclado no funciona

**Categoría:** Hardware  
**Impacto:** Medio  
**Tiempo estimado de resolución:** 5–15 minutos

---

## Descripción del problema

El mouse (ratón) o teclado no responde, funciona de forma intermitente o tiene comportamiento inesperado (doble clic, teclas pegadas, cursor que salta).

---

## Causas más comunes

1. Batería baja en dispositivos inalámbricos.
2. Receptor USB (dongle) desconectado o en mal contacto.
3. Driver del dispositivo desactualizado o corrupto.
4. Conflicto de USB (demasiados dispositivos en un hub USB sin potencia suficiente).
5. Configuración de accesibilidad activa (teclas de filtro, teclas lentas o cursor del mouse activado).
6. Falla física del dispositivo.

---

## Pasos de diagnóstico y resolución

### Para mouse o teclado inalámbrico

#### Paso 1 — Verificar batería
- Cambiar las pilas/baterías aunque parezcan nuevas.
- Para dispositivos recargables: cargar por al menos 30 minutos antes de volver a probar.

#### Paso 2 — Verificar el receptor USB (dongle)
1. Desconectar el dongle USB del equipo.
2. Connectarlo a un puerto USB diferente (preferentemente en el equipo directamente, no en un hub).
3. Esperar 10 segundos para que Windows lo reconozca.

#### Paso 3 — Re-emparejar el dispositivo
- Apagar y encender el mouse/teclado.
- Presionar el botón de emparejamiento (suele estar en la parte inferior del dispositivo).
- Si es Logitech con receptor Unifying: usar Logitech Unifying Software para reemparejar.

### Para mouse o teclado USB con cable

#### Paso 1 — Probar en otro puerto USB
- Desconectar y conectar en un puerto USB diferente.
- Preferir puertos USB en el equipo sobre puertos en un hub o docking station.

#### Paso 2 — Probar en otro equipo
- Conectar el dispositivo en otro equipo para determinar si el problema es del dispositivo o del puerto.

### Para cualquier tipo de dispositivo

#### Paso 3 — Reinstalar el driver

1. Abrir **Administrador de dispositivos**.
2. Expandir **Ratones y otros dispositivos señaladores** o **Teclados**.
3. Clic derecho en el dispositivo → **Desinstalar dispositivo** (marcar "Eliminar software del controlador").
4. Desconectar el dispositivo → reconectar → Windows instalará el driver automáticamente.

#### Paso 4 — Verificar configuración de accesibilidad

1. Ir a **Configuración → Accesibilidad → Teclado**.
2. Verificar que **Teclas de filtro**, **Teclas lentas** y **Teclas de alternancia** estén desactivadas.
3. Ir a **Accesibilidad → Mouse** → verificar que **Teclas de mouse** (control del cursor con numpad) esté desactivado.

#### Paso 5 — Verificar actualizaciones de Windows

Algunos drivers de mouse/teclado se entregan vía Windows Update:
1. **Configuración → Windows Update → Buscar actualizaciones**.
2. Revisar si hay actualizaciones de driver opcionales en **Opciones avanzadas → Actualizaciones opcionales**.

---

## Cuándo escalar a mesa de ayuda (requerimiento de hardware)

- El dispositivo no funciona en ningún equipo (falla de hardware confirmada → necesita reemplazo).
- El mouse tiene doble clic persistente (falla del microswitch → reemplazo garantía o requerimiento nuevo).
- La docking station no reconoce ningún dispositivo conectado.

**Para solicitar un mouse o teclado nuevo**, usar el proceso de requerimiento de hardware (ver KB-IT-009-Renovacion-Equipo).

**Prioridad sugerida al escalar:** Baja-Media (usuario puede usar el teclado del equipo o un mouse de respaldo).

---

## Información a recopilar al escalar

- Marca y modelo del dispositivo.
- Tipo de conexión: USB, inalámbrico RF, Bluetooth.
- Si el problema aparece en otro equipo también.
- Hace cuánto tiempo tiene el problema.
