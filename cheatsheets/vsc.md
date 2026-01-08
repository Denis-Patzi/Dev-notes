# ⚡ Cheat sheet VS Code — atajos, comandos y tips rápidos

Guía práctica y visual con atajos y comandos útiles para usar Visual Studio Code eficientemente.

---

## 🧭 Abrir / cerrar ventanas y recargar

```bash
# Abrir una nueva ventana de VS Code
code --new-window
```

```bash
# Recargar la ventana actual (útil tras instalar extensiones)
code --reload-window
```

```bash
# Cerrar procesos de VS Code desde la terminal (Linux/Mac/Windows WSL)
pkill -f "code"
```

---

## 📂 Crear archivos y carpetas desde terminal

```bash
# Crear una carpeta
mkdir nombre_de_la_carpeta
```

```bash
# Crear archivos vacíos (Windows PowerShell: usa New-Item en vez de touch)
# En Git Bash o Linux:
touch index.html styles.css
```

---

## 🔎 Atajos esenciales (Windows)

- Ctrl+Shift+P — paleta de comandos (busca cualquier acción)
- Ctrl+P — abrir archivo rápido por nombre
- Ctrl+` — abrir terminal integrado
- Ctrl+B — alternar barra lateral
- Ctrl+F — buscar en el archivo
- Ctrl+H — reemplazar en el archivo
- Alt+F4 — cerrar la ventana

---

## 🧰 Extensiones recomendadas

- Live Server — vista previa en vivo para proyectos web
- Prettier — formateador de código
- ESLint — linting para JavaScript/TypeScript
- GitLens — supercarga las funciones de Git dentro de VS Code

---

## 🔗 Abrir proyecto en VS Code desde WSL

Dentro de WSL, abre el directorio actual en VS Code con:

```bash
# Ejecutar dentro de WSL
default
code .
```

Esto abrirá una ventana de VS Code conectada a la sesión WSL si tienes instalada la extensión Remote - WSL.

---

## 🛠 Comandos Git integrados desde terminal

```bash
# Mostrar historial de commits en una línea (útil para revisar rápido)
git log --oneline --graph --all
```

```bash
# Ver el estado
git status
```

```bash
# Añadir y commitear
git add .
git commit -m "mensaje"
```

---

## 💡 Tips rápidos
- Usa la paleta (Ctrl+Shift+P) para buscar funciones cuando no recuerdes atajos.
- Configura `editor.formatOnSave` para formateo automático con Prettier.
- Abre configuraciones con Ctrl+, (coma) para ajustar atajos y apariencia.
- Usa la vista de Source Control integrada para staging y commits rápidos.

---

*Última actualización: Enero 2026*



