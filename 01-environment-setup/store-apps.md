# 🛍️ Aplicaciones Esenciales (Microsoft Store)

Colección curada de utilidades desde Microsoft Store (y Winget) para productividad, personalización y gestión del sistema en Windows — rápida, práctica y lista para instalar. ✨

---

## 🚀 Productividad y flujo de trabajo
Herramientas que hacen el día a día más ágil.

| Aplicación | ¿Por qué usarla? | Comando (winget) |
| :--- | :--- | :--- |
| **QuickLook** | Previsualiza archivos con la barra espaciadora (como macOS). Imprescindible para revisar archivos sin abrir apps. | `winget install PaddyXu.QuickLook` |
| **GlideX** | Permite usar tablets o móviles como segunda pantalla / espejo; útil en setups ASUS ROG. | *Instalar desde Microsoft Store* |

---

## 🎨 Personalización (Look & Feel)
Dale estilo al escritorio sin sacrificar rendimiento.

| Aplicación | ¿Qué hace? | Comando (winget) |
| :--- | :--- | :--- |
| **TranslucentTB** | Controla la apariencia de la barra de tareas (transparente, acrílico, difuminado). | `winget install TranslucentTB.TranslucentTB` |
| **Lively Wallpaper** | Fondos animados y reactivos (audio/mouse). Buen recurso para pantallas principales. | `winget install DaniJohn.LivelyWallpaper` |

---

## 🛠️ Gestión del sistema y hardware
Apps que ayudan a mantener el equipo en forma y gestionar periféricos.

| Aplicación | Útil para... | Comando (winget) |
| :--- | :--- | :--- |
| **Microsoft PC Manager** | Limpieza de sistema, gestión de procesos y rendimiento sin bloatware añadido. | `winget install Microsoft.PCManager` |
| **Twinkle Tray** | Controla brillo de monitores externos (DDC/CI) desde la bandeja — esencial para setups multi-monitor. | `winget install XanderBaatz.TwinkleTray` |

---

## ⚡ Comando rápido: Instalar todo de golpe (Winget)
Copia y pega en PowerShell (ejecutar como Administrador). Omitir apps que no estén en Winget (ej. GlideX si solo está en MS Store).

```powershell
# Ejecuta en PowerShell como Administrador
winget install PaddyXu.QuickLook --accept-package-agreements --accept-source-agreements
winget install TranslucentTB.TranslucentTB --accept-package-agreements --accept-source-agreements
winget install DaniJohn.LivelyWallpaper --accept-package-agreements --accept-source-agreements
winget install Microsoft.PCManager --accept-package-agreements --accept-source-agreements
winget install XanderBaatz.TwinkleTray --accept-package-agreements --accept-source-agreements
```

> Nota: winget puede fallar si no tienes permisos o si alguna app cambió de identificador; instala manualmente desde Microsoft Store si es necesario.

---

## 💡 Tips de uso y notas personales
- QuickLook: perfecto para revisar rápidamente imágenes, PDFs y Markdown. Presiona espacio para cerrar la vista.
- GlideX: en mi ASUS ROG Strix funciona muy bien para convertir una tablet en segundo monitor; puede requerir permisos o instalación adicional.
- Twinkle Tray: si usas monitores externos, es casi obligatorio — Windows no siempre gestiona brillo externo correctamente.
- Lively Wallpaper: consume recursos según el tipo de fondo; usa fondos ligeros si priorizas rendimiento.

---

## 🧾 Extras y seguimiento
- Si quieres, puedo generar un script `setup/install-store-apps.ps1` que detecte qué ya está instalado y ejecute solo lo que falta.
- ¿Quieres una versión en inglés o una sección con alternativas Open Source? Dime y la añado.

---

*Última actualización: Enero 2026*
