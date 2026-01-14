# 🔧 Comandos de Hardware (Windows PowerShell)

> ⚠️ Nota: Microsoft ha comenzado a deprecar `WMIC` en Windows 11. Se recomienda usar `Get-CimInstance` en PowerShell.

---

## 🚀 Inicio rápido
1. Abre PowerShell como **Administrador**.
2. Copia el bloque que necesites y pégalo en la consola.
3. Si quieres ver todas las propiedades disponibles de una clase: `Get-CimInstance -ClassName <Clase> | Select-Object *`.

---

## 🧠 1) Memoria RAM

### ⚡ Ver velocidad actual (MHz) y configuración por módulo
Muestra la velocidad real, capacidad y ranura de cada módulo.
```powershell
Write-Host "--- DATOS DE LA MEMORIA (MÓDULOS) ---" -ForegroundColor Cyan
Get-CimInstance -ClassName Win32_PhysicalMemory |
  Format-Table BankLabel, @{Name='Size(GB)';Expression={[math]::Round($_.Capacity/1GB,2)}}, Speed, ConfiguredClockSpeed -AutoSize
```

### 📦 Ver capacidad máxima soportada y número de ranuras
`MaxCapacity` está en KB: el comando siguiente lo convierte a GB y muestra slots.
```powershell
Write-Host "--- DATOS DE LA MEMORIA (CAPACIDAD MÁXIMA / SLOTS) ---" -ForegroundColor Cyan
$info = Get-CimInstance -ClassName Win32_PhysicalMemoryArray
Write-Host "MaxCapacity(GB):" -NoNewline; Write-Host ([math]::Round($info.MaxCapacity/1024/1024,2)) -ForegroundColor Yellow
Write-Host "MemoryDevices (slots):" -NoNewline; Write-Host $info.MemoryDevices -ForegroundColor Yellow
```

> Tip: `MemoryDevices` es la cantidad de ranuras (slots). Si MaxCapacity es 65536 -> 64 GB.

---

## 🧩 2) Procesador (CPU)

### 🏷️ Ver modelo, núcleos y velocidad
Muestra nombre comercial, núcleos físicos y lógicos y velocidad máxima reportada.
```powershell
Write-Host "--- DATOS DEL PROCESADOR ---" -ForegroundColor Cyan
Get-CimInstance -ClassName Win32_Processor |
  Format-List Name, MaxClockSpeed, NumberOfCores, NumberOfLogicalProcessors
```

---

## 🖥️ 3) Placa base (Motherboard)

### 🆔 Fabricante, modelo y número de serie
Útil para buscar drivers, manuales o compatibilidad de componentes.
```powershell
Write-Host "--- DATOS DE LA PLACA BASE ---" -ForegroundColor Cyan
Get-CimInstance -ClassName Win32_BaseBoard | Format-List Manufacturer, Product, SerialNumber
```

---

## 📝 4) Información general del sistema

### 💻 Fabricante, modelo y tipo de sistema
Identifica el equipo completo (ej. laptop o desktop) y arquitectura.
```powershell
Write-Host "--- DATOS DEL EQUIPO ---" -ForegroundColor Cyan
Get-CimInstance -ClassName Win32_ComputerSystem | Format-List Manufacturer, Model, SystemType
```

---

## 💡 Trucos y consejos rápidos
- Usa `| Out-GridView` para una vista interactiva y filtrable: `Get-CimInstance ... | Out-GridView`.
- Para ver todas las propiedades: `Get-CimInstance -ClassName Win32_Processor | Select-Object *`.
- Si no devuelve nada: ejecuta PowerShell como Admin y verifica servicios WMI/CIM.
- Para copiar resultados en texto simple: `Get-CimInstance ... | Format-Table -AutoSize | Out-String`.

---

## ✅ Resumen (cheat-sheet)
- RAM: `Win32_PhysicalMemory` y `Win32_PhysicalMemoryArray`
- CPU: `Win32_Processor`
- Motherboard: `Win32_BaseBoard`
- Sistema: `Win32_ComputerSystem`

---


*Última actualización: Enero 2026*