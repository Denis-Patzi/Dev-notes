# ⚡ Configuración de energía y overclocking — Raspberry Pi 5

Guía práctica y segura para ajustar la entrega de corriente USB y aplicar overclock en Raspberry Pi 5. Incluye pasos con comandos listos para copiar, comprobaciones y consejos de seguridad.

> ⚠️ Aviso importante: modificar la configuración de energía y overclockear puede dañar el hardware o provocar inestabilidad si no se hace correctamente. Usa una fuente de alimentación de calidad y un sistema de refrigeración adecuado (Active Cooler recomendado).

---

## 📌 Resumen rápido
- Forzar mayor corriente USB: `usb_max_current_enable=1` en `/boot/firmware/config.txt` o cambiar el parámetro EEPROM `PSU_MAX_CURRENT`.
- Overclocking: editar parámetros en `/boot/firmware/config.txt` (arm_freq, gpu_freq, over_voltage_delta), siempre con refrigeración y pruebas.
- Haz siempre una copia de seguridad antes de tocar archivos de arranque.

---

## 📝 Problema identificado — Parpadeo de pantalla

- Síntoma principal: parpadeo (flicker) o pérdida momentánea de imagen en la pantalla conectada a la Raspberry Pi. Puede venir acompañado de:
  - Desconexiones intermitentes de dispositivos USB (teclado, ratón, cámaras).
  - Mensajes de undervoltage en logs o por `vcgencmd get_throttled`.
  - Reinicios inesperados o inestabilidad bajo cargas altas.

Este documento describe cómo diagnosticar y mitigar el problema cuando está relacionado con la alimentación (cargador y/o cable), usando una microSD con Raspberry Pi OS.

---

## 🔌 Detalle técnico: cargadores 5V/3A vs 5V/5A y por qué importan

- Cargador 5V/3A (genérico): capacidad teórica limitada; suele fallar en picos de demanda si el cable o el cargador no tiene la calidad adecuada.
- Cargador 5V/5A (genérico): capacidad teórica mayor, pero si no implementa Power Delivery (PD) correctamente o si el cable es de mala calidad, la tensión real en la placa puede caer.
- Factor crítico: calidad del cable (calibre, longitud) y compatibilidad PD. Muchos problemas de flicker se deben a caídas de tensión en el conector (por debajo de ~4.8 V) o a reset/disconnects en el bus USB.

Consecuencia: la Pi detecta condiciones de undervoltage y puede activar protecciones (throttling) o registrar eventos que coinciden con el parpadeo.

---

## 🔁 Cambio propuesto (qué se modifica)

1) En `config.txt` de arranque: añadir `usb_max_current_enable=1` para permitir una política de consumo USB menos restrictiva (mitigación temporal).

2) En la EEPROM (si procede): ajustar `PSU_MAX_CURRENT` (valor en mA, por ejemplo `5000`) para indicar que la fuente puede entregar más corriente. Esto requiere backup y cautela.

Importante: ambos cambios son mitigaciones de firmware/arranque — no sustituyen una fuente/cable inseguro. Úsalos para diagnóstico o como solución temporal hasta disponer de buena fuente/cable.

---



## 🌟 SOP rápido (hazlo al ver el fondo de Raspberry Pi OS)

Problema: parpadeo de pantalla (flicker) y/o desconexiones USB tras cambiar cargador.

Causa habitual: caída de tensión por cargador/cable inadecuado (5V/3A vs 5V/5A, PD, calidad del cable).

Cambio propuesto (temporal): forzar la EEPROM a aceptar hasta 5A con `PSU_MAX_CURRENT=5000`.

Pasos (hazlos exactamente en este orden):

1) Abrir la terminal (icono negro) y ejecutar:

```bash
sudo rpi-eeprom-config -e
```

2) En el editor nano, ve al final y añade exactamente (respeta mayúsculas):

```text
PSU_MAX_CURRENT=5000
```

3) Guardar y salir: Ctrl+O → Enter → Ctrl+X

3.1) (OPCIONAL) Verificar y hacer backup de EEPROM antes de aplicar

```bash
# Guardar copia de la configuración EEPROM actual (por si hace falta restaurar)
sudo rpi-eeprom-config > ~/rpi-eeprom-config-backup.txt
# Comprobar estado de throttling/undervoltage
vcgencmd get_throttled
```

4) Aplicar y reiniciar (CRÍTICO):

```bash
sudo rpi-eeprom-update -a
sudo reboot
```

---

*Última actualización: Enero 2026*