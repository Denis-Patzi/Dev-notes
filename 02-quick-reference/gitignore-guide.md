# 🛡️ Guía .gitignore — Mantén tu repo limpio y profesional

---
## TL;DR: 
Añade un `.gitignore` al inicio de tu proyecto para evitar subir archivos temporales, binarios o configuraciones locales (IDE). Esto mantiene el historial limpio y evita conflictos.

---
## ¿Qué es `.gitignore`? 🤔
Un archivo de texto llamado exactamente `.gitignore` indica a Git qué archivos o carpetas debe ignorar. Útil para: dependencias instaladas localmente, archivos de compilación, archivos de configuración del IDE, credenciales locales, etc.

---
## 1) Crear el archivo
En WebStorm (u otro IDE):
- Haz clic derecho en la carpeta raíz del proyecto (p. ej. `Dev-notes`).
- Nuevo > File
- Nombra el archivo `.gitignore` (asegúrate de incluir el punto al principio).

En VS Code: Ctrl+N → Guardar como `.gitignore`.

---
## 2) Contenido recomendado — ejemplos rápidos
Copia y pega los bloques que necesites según tu stack. Mantén sólo lo necesario.

### Básico / General
```text
# Sistema
.DS_Store
Thumbs.db

# Dependencias
node_modules/

# Coverage
coverage/

# Build
dist/
build/

# Entornos
.env

# Logs
logs/
*.log
npm-debug.log*
yarn-debug.log*

# Editor IDE
.vscode/
.idea/

```

### JetBrains (WebStorm, IntelliJ) — recomendado si usas WebStorm
```text
# JetBrains
.idea/
*.iml
out/
gen/
``` 

### Node.js (ampliado)
```text
# Node
node_modules/
npm-debug.log*
yarn-debug.log*
package-lock.json
.pnp.cjs
.pnp.js
```

### Python
```text
# Python
__pycache__/
*.py[cod]
venv/
.env
```

### Visual Studio / .NET (si aplica)
```text
# Visual Studio
*.user
*.suo
bin/
obj/
```

---
## 3) Cómo guardar y verificar
1. Guarda el archivo en la raíz del proyecto.
2. Abre tu herramienta Git (WebStorm/VSCode/Git CLI) y revisa la lista de archivos no versionados.
3. Elimina archivos no deseados del índice si ya fueron añadidos accidentalmente:

```powershell
# Si ya se añadieron al staging, quitar del índice pero conservar localmente
git rm -r --cached .
git add .
git commit -m "chore: add .gitignore and remove tracked files that should be ignored"
```

> Nota: ejecuta el comando desde la raíz del repo.

---
## Pro Tips 💡
- Mensaje de commit sugerido: `docs: add .gitignore to keep repository clean` o `chore: add .gitignore and remove IDE files`
- Si necesitas ignorar secretos, usa herramientas como git-crypt, Vault o variables de entorno, y NUNCA comites credenciales.
- Revisa `git status` antes de commitear para asegurarte que sólo subes lo que quieres.

## ¿Por qué esto importa? ✨
- Evitas commits ruidosos con archivos binarios o dependencias grandes.
- Facilitas colaboraciones (no todos usan el mismo IDE).
- Mantienes el repo ligero y más seguro.

---

Última actualización: Enero 2026 