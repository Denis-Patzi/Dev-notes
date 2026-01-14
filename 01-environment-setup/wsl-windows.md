# 🚀 Cómo instalar y configurar WSL en Windows (Guía práctica)

Esta guía te acompañará paso a paso para instalar el Subsistema de Windows para Linux (WSL) en Windows 10/11, configurar Ubuntu y conectar Visual Studio Code. Incluye comandos listos para copiar, comprobaciones y notas útiles.

> ⚠️ Antes de empezar: haz copia de seguridad de tus datos importantes y asegúrate de ejecutar los comandos en una consola con permisos de Administrador cuando se indica.

---

## 1) Comprobar virtualización (requisito)

- Abre el Administrador de tareas → pestaña Rendimiento → CPU.
- Comprueba que en la sección de la CPU la virtualización aparezca como "Habilitada".

Si aparece "Deshabilitada", debes activarla desde la BIOS/UEFI de tu equipo (el proceso depende del fabricante; busca un tutorial específico para tu modelo).

---

## 2) Activar las características de Windows necesarias

Puedes hacerlo desde la interfaz gráfica (Panel de control → Programas → Activar o desactivar características de Windows) marcando:

- Virtual Machine Platform
- Windows Subsystem for Linux

Reinicia el equipo después de activarlas.

Si prefieres hacerlo por línea de comandos (PowerShell como Administrador), copia y ejecuta cada bloque por separado:

```powershell
# Habilita la Plataforma de Máquina Virtual
 dism /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

```powershell
# Habilita el Subsistema de Windows para Linux
 dism /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

```powershell
# Reinicia Windows (ejecuta esto manualmente si prefieres)
 shutdown /r /t 5
```

---

## 3) Instalar WSL y una distribución (Windows 11)

En Windows 11 (y en Windows 10 con ciertas actualizaciones) puedes instalar WSL con un único comando.

```powershell
# Ejecutar en PowerShell / Terminal (Admin)
 wsl --install
```

El comando descarga e instala WSL y, por defecto, instala una distribución (por ejemplo, Ubuntu). Sigue las instrucciones en pantalla. Si te pide reiniciar, reinicia y vuelve a ejecutar el comando si es necesario.

Si quieres instalar una distribución específica (por ejemplo Ubuntu 24.04 LTS):

```powershell
# Lista distribuciones disponibles
 wsl --list --online
```

```powershell
# Instala una distribución específica
 wsl --install -d Ubuntu-24.04
```

---

## 4) Instalar WSL en Windows 10 (alternativa)

Si tu Windows 10 no soporta el comando anterior, instala la distribución desde Microsoft Store:

1. Abre Microsoft Store.
2. Busca "Ubuntu" y elige la versión que quieras (ej. "Ubuntu 24.04 LTS").
3. Instálala y ábrela.

Al iniciar la primera vez, te pedirá crear un usuario UNIX y una contraseña.

---

## 5) Primer arranque y creación de usuario

Cuando la instalación termine, al abrir la distro por primera vez verás un prompt para crear un usuario UNIX:

- Escribe el nombre de usuario (sin mayúsculas si prefieres seguir la nota anterior).
- Escribe la contraseña (al teclear no verás caracteres, es normal) y confírmala.

Si la distro no pide usuario o quieres abrir una sesión manualmente, ejecuta:

```powershell
# Abrir la distro Ubuntu desde Windows
 wsl.exe -d Ubuntu
```

Para salir de la sesión WSL:

```powershell
# Salir de la sesión WSL
 exit
```

---

## 6) Conectar VS Code a WSL y extensiones recomendadas

1. Instala Visual Studio Code si no lo tienes: https://code.visualstudio.com/
2. Abre VS Code y ve a Extensiones.
3. Instala la extensión "Remote - WSL" (Microsoft).

En la esquina inferior izquierda aparecerá el icono de Remote. Haz clic y selecciona "Connect to WSL" para abrir una ventana de VS Code conectada a tu distribución.

Extensiones útiles dentro de WSL / proyectos web:

```text
- Live Server (Ritwick Dey)
- Prettier - Code formatter (Prettier)
- ES7+ React/Redux/React-Native snippets (opcional si usas React)
```

Consejo: desde la terminal WSL puedes abrir el proyecto en VS Code con:

```bash
# Abrir el directorio actual en VS Code (ejecutar dentro de WSL)
 code .
```

---

## 7) Actualizar el sistema Linux (recomendado)

Tras instalar la distro, actualiza los paquetes:

```bash
# Actualiza la lista de paquetes
 sudo apt update
```

```bash
# Instala actualizaciones disponibles
 sudo apt upgrade -y
```

Esto puede tardar varios minutos dependiendo de las actualizaciones pendientes.

---

## 8) Comandos y comprobaciones útiles

```powershell
# Mostrar las distribuciones instaladas
 wsl --list --verbose
```

```powershell
# Establecer una distro por defecto
 wsl --set-default <NombreDistro>
```

```powershell
# Actualizar WSL (si hay actualizaciones del kernel WSL)
 wsl --update
```

```powershell
# Reiniciar el servicio WSL
 wsl --shutdown
```

---

## Problemas comunes y soluciones rápidas

- Si WSL no arranca o da error, reinicia Windows y asegúrate de que las características estén habilitadas.
- Si la virtualización aparece deshabilitada, actívala en la BIOS.
- Si la distribución no aparece en la lista, instalala desde Microsoft Store o usa `wsl --install -d <distro>`.

---

*Última actualización: Enero 2026*

