# 🔋 Optimización y Cuidado de Batería

Guía práctica y visual para extender la vida útil de las baterías de litio: límites de carga, alertas tempranas y acciones rápidas para mantener la batería en su "zona feliz" (20%–80%).

---

## TL;DR
- Mantén la batería entre 20% y 80% cuándo sea posible. ⚖️
- Configura la notificación de batería baja al 20–25%. 🔔
- Usa las utilidades del fabricante (MyASUS, Lenovo Vantage, etc.) o alternativas ligeras como G-Helper. 🛠️

---

## 1. Limitar la Carga al 80% (Cuidado de Ciclos)

Mantener la batería al 100% mientras está conectada genera estrés en las celdas de litio. Lo ideal es limitarla al 80% (o 60% si el equipo está casi siempre enchufado).

### Método para ASUS (ROG/TUF/Vivobook) 🧾
Dado que Windows no tiene esta función nativa, se debe usar el controlador/APP del fabricante:

1. Abrir la aplicación **MyASUS**.
2. Ir a **Personalización** > **Energía y Rendimiento**.
3. Buscar **ASUS Battery Health Charging**.
4. Seleccionar:
   - **Modo Equilibrio:** Carga hasta el 80% (Ideal para uso mixto). ✅
   - **Modo Máxima Duración:** Carga hasta el 60% (Ideal si siempre está enchufada). ⚡

> Alternativa ligera: **G-Helper** (Open Source). Es una alternativa minimalista a Armoury Crate/MyASUS que permite fijar el límite de carga con un slider sin consumir recursos en segundo plano.

---

## 2. Configurar Alerta de Batería Baja (Panel de Control) 🔔

Por defecto, Windows avisa al 10% o 5%, lo cual es muy bajo. Lo ideal es recibir el aviso al **20% o 25%** para poder conectar el cargador a tiempo.

### Pasos para modificar la alerta:

1. Presiona `Win + R` y escribe:

```cmd
powercfg.cpl
```
2. En tu plan de energía seleccionado, haz clic en **"Cambiar la configuración del plan"**.
3. Clic en **"Cambiar la configuración avanzada de energía"**.
4. Desplázate hasta el final y despliega **Batería**.
5. Modifica los siguientes valores:

| Configuración | Valor Recomendado | Descripción |
| :--- | :---: | :--- |
| **Nivel de batería baja** | **25%** | Punto donde Windows lanzará la primera advertencia. |
| **Notificación de batería baja** | **Activado** | Asegura que salga el aviso visual. |
| **Acción de batería crítica** | **Hibernar** | Mejor que "Suspender" para no perder datos si se apaga. |

---

## ¿Por qué hacer esto? 🧪

Las baterías de iones de litio se degradan más rápido si se agotan por debajo del 20% con frecuencia o si se mantienen al 100% con calor constante. Mantenerlas entre **20% - 80%** es el mejor compromiso entre autonomía y longevidad.

---

## Acciones rápidas (copiar y ejecutar) ⚙️

Genera un informe de batería y revisa el estado actual:

```powershell
# Genera un informe de batería en el escritorio
powercfg /batteryreport /output "%USERPROFILE%\Desktop\battery-report.html"
```
```powershell
# Genera un informe de energía para diagnosticar consumos (requiere permisos)
powercfg /energy /output "%USERPROFILE%\Desktop\energy-report.html"
```

Consejo: abre el `battery-report.html` en tu navegador y revisa el historial de capacidad diseñada vs capacidad actual.

---

## Consejos prácticos y mantenimiento ✅
- Si vas a guardar el equipo largo tiempo, deja la batería al ~40% y guárdalo en un lugar fresco. 🧊
- Evita calor continuo: si trabajas intensamente en cargas largas, quita la batería cuando sea posible (solo en equipos con batería extraíble) o ventila el equipo. 🌬️
- No dejes la batería al 100% todo el tiempo; si trabajas constantemente enchufado, elige el modo de conservación del fabricante. 🔁
- Calibra la batería cada 3–6 meses: carga al 100%, deja descargar hasta ~5–7% y vuelve a cargar al 100% (esto ayuda a corregir lecturas del sistema). ⚙️

---

## Recursos y referencia 📚
- Busca el panel/APP del fabricante: MyASUS, Lenovo Vantage, Dell Power Manager, HP Support Assistant.
- G-Helper — alternativa ligera para ASUS (buscar en GitHub).
- Comando útil: `powercfg /batteryreport` (Windows) para ver historial detallado.

---

*Última actualización: Enero 2026*
