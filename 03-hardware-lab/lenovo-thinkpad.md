# 🧭 Configuración Lenovo / ThinkPad

Ajustes prácticos y rápidos para corregir comportamientos de hardware en equipos Lenovo (ThinkPad, IdeaPad, Legion). Ideal para preparar un equipo nuevo o para configurar atajos y batería.

---

## TL;DR
- Intercambia Fn/Ctrl si usas atajos habitualmente. ⌨️
- Usa **Lenovo Vantage** para umbrales de batería y ajustes de energía. 🔋
- FnLock: `Fn + Esc` cambia el comportamiento rápido. 🔁
- Accede a la BIOS con `F1` al arrancar o con **Shift + Reiniciar** desde Windows. 🔧

---

## 1. Intercambiar teclas Fn y Ctrl (Swap Keys) 🔀

Históricamente, los ThinkPads tienen la tecla `Fn` en la esquina inferior izquierda (donde habitualmente va `Ctrl`). Si te molesta al usar atajos (Ctrl+C, Ctrl+V), cambia el comportamiento.

### Método A: Vía Software (Lenovo Vantage) 🧰
Recomendado si usas Windows y no quieres reiniciar.

1. Abre **Lenovo Vantage** (Microsoft Store).
2. Ve a **Dispositivo** > **Entrada y accesorios** (Input & Accessories).
3. Busca la sección **Teclado**.
4. Activa **Intercambiar las teclas Fn y Ctrl** (Fn and Ctrl Key swap).

> Nota: Lenovo Vantage suele detectar tu modelo y mostrar opciones adicionales de energía y batería.

### Método B: Vía BIOS / UEFI (Permanente) 🖥️
Útil si reinstalas el sistema, usas Linux o prefieres una configuración a nivel firmware.

1. Reinicia el equipo.
2. Presiona `F1` (en algunos modelos es `Enter` o `Fn+F1`) para entrar en la BIOS/UEFI.
3. Navega a **Config** > **Keyboard/Mouse**.
4. Activa **Fn and Ctrl Key swap**.
5. Guarda y sal (`F10`).

---

## 2. Bloqueo de teclas de Función (FnLock) 🔒

Si `F1`–`F12` disparan controles multimedia (brillo/volumen) y prefieres las teclas F tradicionales:

- Atajo rápido (la mayoría de modelos): `Fn + Esc`.
  - LED de `Esc` ENCENDIDO → F1–F12 normales.
  - LED de `Esc` APAGADO → teclas multimedia.

Si ese atajo no funciona, revisa Lenovo Vantage o la BIOS (busca "Action Keys Mode" o similar).

---

## 3. Umbral de Carga de Batería (Lenovo Vantage) ⚡

Lenovo permite limitar la carga para prolongar la vida útil de la batería.

1. Abre **Lenovo Vantage**.
2. Ve a **Energía** (Power).
3. Activa **Umbral de carga de la batería** (Battery Charge Threshold).
4. Configura valores recomendados:
   - Iniciar carga: 75%
   - Detener carga: 80% (buena práctica para conservar ciclos)

---

## Acciones rápidas 🔧 (lista para copiar / ejecutar)

- Forzar entrada a UEFI desde Windows (Shift + Reiniciar):

```text
Inicio → Mantén presionada la tecla Shift y selecciona Reiniciar → Solucionar problemas → Opciones avanzadas → Configuración de firmware UEFI → Reiniciar
```

- Atajo FnLock:

```text
Presiona Fn + Esc (verifica el estado del LED de Esc)
```

- Abrir Lenovo Vantage: búscalo en Microsoft Store o en el menú Inicio.

- Comprobación rápida del estado de energía/batería (Windows):

```powershell
# Genera un informe de batería en el Escritorio
powercfg /batteryreport /output "$env:USERPROFILE\Desktop\battery-report.html"
```

---

## Consejos y notas prácticas 📝
- Si usas Linux: el swap físico de Fn/Ctrl en BIOS es la forma más fiable (no depende de drivers Windows).
- Si compras un equipo para trabajo intensivo con atajos, cambia las teclas al principio para evitar costumbres incómodas.
- Mantén Lenovo Vantage actualizado para recibir mejoras de firmware y opciones de gestión de energía.

---

## Recursos 📚
- Lenovo Vantage — Microsoft Store
- Documentación Lenovo: busca el manual de tu modelo (ThinkPad/IdeaPad/Legion)

*Última actualización: Enero 2026*
