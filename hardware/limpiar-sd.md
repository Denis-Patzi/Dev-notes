# 🧼 Limpiar y reparar una tarjeta microSD (Windows)

Este documento explica dos métodos para recuperar o limpiar una tarjeta microSD en Windows: el método "nuclear" con DiskPart (borrado total) y una reparación lógica con CHKDSK. Incluye advertencias, comandos listos para copiar y consejos prácticos.

> ⚠️ Antes de empezar: copia tus archivos si quieres conservarlos. El Método 1 borra todo en la tarjeta.

---

## 📌 Contenido rápido

- Método 1 — Restablecimiento de fábrica (DiskPart): borra y formatea la tarjeta (recomendado si vas a reinstalar un sistema como Raspberry Pi OS).
- Método 2 — Reparación de errores (CHKDSK): intenta reparar sin borrar si sólo hay problemas lógicos.
- Consejos extra: herramientas alternativas, comprobaciones y cómo identificar daño físico.

---

## Método 1 — Restablecimiento de fábrica (DiskPart) 💣

Este es el método "nuclear". Úsalo si no te importa perder los archivos y quieres que la tarjeta vuelva a un estado limpio.

Pasos:

1. Conecta la microSD al PC.
2. Abre el Símbolo del sistema como Administrador: pulsa Windows + R, escribe `cmd` y presiona Ctrl + Shift + Enter.
3. En la consola escribe `diskpart` y presiona Enter.
4. Lista los discos:

```powershell
list disk
```

- Importante: identifica tu tarjeta por el tamaño (GB). En ejemplos anteriores podía aparecer como `Disk 1` (~58 GB). Asegúrate de no seleccionar el disco equivocado.

5. Selecciona la tarjeta (sustituye X por el número correcto):

```powershell
select disk X
```

6. (Opcional pero recomendado) Quita el modo de sólo lectura por software:

```powershell
attributes disk clear readonly
```

7. Limpia el disco (esto borra todas las particiones):

```powershell
clean
```

- Si funciona verás: "DiskPart succeeded in cleaning the disk".

8. Crea una partición primaria:

```powershell
create partition primary
```

9. Formatea la tarjeta. Para 64GB usa exFAT:

```powershell
format fs=exfat quick
```

- Si la tarjeta es de 32GB o menos, podrías usar `format fs=fat32 quick`.

10. Asigna una letra para que Windows la reconozca:

```powershell
assign
```

11. Sal de diskpart:

```powershell
exit
```

Notas rápidas:
- Usamos `exFAT` para tarjetas de 64GB por compatibilidad y limitaciones de FAT32. Si vas a preparar una tarjeta para Raspberry Pi, el Pi Imager normalmente reasigna las particiones necesarias al escribir la imagen.
- Si planificas usar la tarjeta con Raspberry Pi manualmente, recuerda que la partición de arranque debe ser FAT32.

---

## Método 2 — Reparación de errores (CHKDSK) 🔧

Úsalo si quieres intentar arreglar errores lógicos sin borrar todo. No siempre funciona si hay corrupción severa o daño físico.

1. Abre CMD como Administrador.
2. Ejecuta (reemplaza `E:` por la letra asignada a tu tarjeta):

```powershell
chkdsk E: /f /r
```

Significado de los parámetros:
- `/f` — corrige errores en el sistema de archivos.
- `/r` — localiza sectores defectuosos e intenta recuperar la información.

Este proceso puede tardar varios minutos u horas según el tamaño y el estado. Si se queda pegado o muestra muchos errores, la tarjeta puede estar físicamente dañada.

---

## 🛠️ Herramientas alternativas y recomendaciones

- SD Formatter (herramienta oficial de SD Association) — facilita formateos limpios y seguros.
- Raspberry Pi Imager — para grabar imágenes del sistema (recomendado para Pi). Este programa se encarga de particionar y formatear correctamente.
- H2testw (Windows) o F3 (Linux/Mac) — para verificar capacidad real y sectores defectuosos (detecta tarjetas falsas).

---

## 🧾 Diagnóstico y pasos finales

- Si tras DiskPart o CHKDSK la tarjeta sigue con problemas:
  - Prueba en otro lector o equipo.
  - Comprueba si aparece en Administración de discos (diskmgmt.msc).
  - Usa H2testw/F3 para ver si hay sectores defectuosos o capacidad falsa.
  - Si hay sectores físicos dañados o la tarjeta falla constantemente, es más seguro reemplazarla.

---

## 💡 Consejos útiles

- Haz backups frecuentes: las microSD tienen vida limitada (ciclos de escritura).
- Evita extraer la tarjeta sin expulsarla; esto reduce la corrupción.
- Si necesitas FAT32 para compatibilidad, hay herramientas que permiten formatear FAT32 en unidades >32GB (pero con limitaciones).

---

## 🔁 Rufus — la solución de ingeniería (fuerza bruta) ⚙️

¿DiskPart no puede tomar control del disco o Windows se enreda con particiones Linux? Rufus puede ser la "fuerza bruta" que necesitas: desmonta más agresivamente y reescribe la unidad. Úsalo con cuidado: borra todo, pero suele funcionar donde DiskPart no consigue el "handle".

📌 Mini‑cheat (pegable)

- Paso 1: Abrir Rufus como Administrador (portable OK)
- Paso 2: Seleccionar la microSD correcta (verifica tamaño)
- Paso 3: En "Elección de arranque" → elegir **No autoejecutable (Non-bootable)**
- Paso 4: Pulsar **EMPEZAR** (o elegir imagen y **DD image** si procede)
- Paso 5: Esperar y comprobar en Windows

---

### ✅ Antes de empezar (rápido)
- Verifica el tamaño de la unidad en Windows (¡no borres tu disco!).
- Quita el adaptador SD si tiene el bloqueo de escritura.
- Ten otro lector USB a mano por si el primero falla.
- Si hay datos importantes, intenta recuperación antes (Rufus sobrescribe todo).

### 🧭 Pasos detallados (con vida)
1) Descargar y abrir Rufus 🔽
- Web oficial: https://rufus.ie/ — la versión portable es perfecta.
- Ejecuta con clic derecho → "Ejecutar como administrador".

2) Seleccionar la microSD 📁
- En el campo "Dispositivo" selecciona la unidad (mira el tamaño y la letra).

3) Modo: No autoejecutable (Non-bootable) 🛡️
- Si solo quieres forzar limpieza/particionado -> en "Elección de arranque" elige **No autoejecutable (Non-bootable)**.
- Pulsa **EMPEZAR**. Rufus desmontará y eliminará las particiones antes de formatear.

4) Escribir imagen (opcional — para imágenes de Pi) 🖼️
- Pulsa **SELECCIONAR** y elige tu `.img` o `.iso`.
- Cuando aparezca la opción de modo de escritura, selecciona **Escribir en modo DD (DD image)** — escribe byte a byte, ideal para tablas corruptas.
- Confirma y pulsa **EMPEZAR**.

5) Finalizar y comprobar ✅
- Deja que termine. Al finalizar, comprueba si Windows monta la tarjeta y si los archivos/particiones están correctos.

---

### 🔧 Si aparece un error — acciones rápidas
- Error I/O repetido: prueba otro lector, otro puerto o otro PC; si persiste, hay daño físico probable.
- Acceso denegado / dispositivo ocupado: cierra el Explorador y apps que usen la unidad; vuelve a ejecutar Rufus como Admin.
- Unidad no detectada: reinicia Windows o prueba el lector en otro equipo.

### 🛠 Comando útil (limpieza previa con DiskPart)
Si quieres intentar limpiar la tabla de particiones antes de Rufus:

```powershell
diskpart
list disk
select disk X   # sustituye X por el número correcto
clean
```

> ⚠️ Atención: `clean` borra todo sin preguntar — asegúrate de la unidad.

### 🩺 Verificación de salud
- Ejecuta H2testw (Windows) o F3 (Linux/Mac) para verificar sectores defectuosos y capacidad real.

### 🔁 Alternativas
- balenaEtcher, Win32 Disk Imager o `dd` (Linux). El modo DD de Rufus es el equivalente a `dd`.

---

### ⚠️ Cierre práctico
Rufus es potente y a menudo recupera tarjetas con particiones que Windows no entiende. Pero no repara sectores físicos: si después de varios intentos (lectores/puertos/equipos) sigue fallando, reemplázala. Y siempre, siempre, revisa la unidad seleccionada antes de pulsar **EMPEZAR**.

---

*Última actualización: Enero 2026*