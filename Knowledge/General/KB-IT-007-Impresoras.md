# KB-IT-007: Problemas con impresoras corporativas

**Categoría:** Hardware / Impresión  
**Impacto:** Bajo  
**Tiempo estimado de resolución:** 10–20 minutos

---

## Descripción del problema

La impresora no imprime, está desconectada, los trabajos quedan en cola sin procesarse o la calidad de impresión es deficiente.

---

## Causas más comunes

1. Servicio de cola de impresión (Print Spooler) detenido.
2. Trabajos atascados en la cola de impresión.
3. Impresora desconectada de la red o apagada.
4. Driver desactualizado o corrupto.
5. Sin papel o con papel atascado.
6. Tóner o cartucho agotado.

---

## Pasos de diagnóstico y resolución

### Paso 1 — Verificar estado físico de la impresora

1. Verificar que la impresora esté encendida (luz indicadora verde).
2. Verificar que haya papel cargado correctamente.
3. Revisar si hay un atasco de papel (abrir la tapa frontal/trasera según modelo).
4. Verificar el nivel de tóner desde el panel de la impresora o su software.

### Paso 2 — Verificar conectividad de la impresora en red

1. En el panel de la impresora, imprimir una **página de configuración de red** (manteniendo presionado el botón de configuración por 3 segundos en la mayoría de los modelos).
2. Verificar que tenga dirección IP asignada.
3. Desde el equipo, verificar conectividad:
   ```cmd
   ping [IP_de_la_impresora]
   ```
4. Si no responde al ping → la impresora está desconectada de la red. Reiniciar la impresora y esperar 2 minutos.

### Paso 3 — Limpiar la cola de impresión

**Método automático (recomendado):**
1. Abrir PowerShell como administrador.
2. Ejecutar:
   ```powershell
   Stop-Service -Name Spooler -Force
   Remove-Item "$env:SystemRoot\System32\spool\PRINTERS\*" -Recurse -Force
   Start-Service -Name Spooler
   ```

**Método manual:**
1. Abrir **Servicios** (buscar "Servicios" en el menú Inicio).
2. Encontrar **Cola de impresión** (Print Spooler) → clic derecho → **Detener**.
3. Abrir el Explorador de archivos → ir a `C:\Windows\System32\spool\PRINTERS`.
4. Eliminar todos los archivos de esa carpeta (no las subcarpetas).
5. Volver a **Servicios** → **Cola de impresión** → **Iniciar**.

### Paso 4 — Reinstalar el driver de la impresora

1. Ir a **Configuración → Bluetooth y dispositivos → Impresoras y escáneres**.
2. Seleccionar la impresora → clic en **Eliminar**.
3. Clic en **Agregar dispositivo** → Windows buscará la impresora automáticamente.
4. Si no la encuentra, instalar el driver manualmente desde el portal IT:
   `https://intranet.techint.com/it/drivers-impresoras`

---

## Impresoras de red de Techint (principales modelos)

| Piso/Área | Modelo | IP |
|---|---|---|
| Piso 3 — Buenos Aires | HP LaserJet M507 | 10.10.3.25 |
| Piso 4 — Buenos Aires | Ricoh SP 5300DN | 10.10.4.30 |
| Piso 5 — Buenos Aires | Canon imageRUNNER 2630i | 10.10.5.15 |
| San Nicolás — Planta | HP OfficeJet Pro 9010 | 172.16.1.50 |

---

## Cuándo escalar a mesa de ayuda

- Atasco de papel persistente que no se puede resolver manualmente.
- Falla de hardware (ruidos extraños, errores permanentes en el panel).
- Necesidad de agregar una nueva impresora a un equipo.
- La impresora de red no responde desde ningún equipo.

**Prioridad sugerida al escalar:** Baja (puede imprimir desde otra impresora de red mientras tanto).

---

## Información a recopilar al escalar

- Nombre o IP de la impresora.
- Modelo de la impresora.
- Mensaje de error en el panel de la impresora o en el equipo.
- Piso/ubicación.
