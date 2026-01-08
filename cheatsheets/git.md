# 🧩 Cheat sheet Git — comandos rápidos y flujo de trabajo

Guía corta, ordenada y visual desde lo más básico hasta lo avanzado. Con comandos separados y explicaciones claras para usar día a día.

---

## ✅ Contrato rápido
- Entrada: repositorio Git local (o URL remoto).
- Salida: cambios versionados, ramas organizadas y remoto sincronizado.
- Errores comunes: conflictos de merge, errores de autenticación, pushes rechazados.

---

## 🚀 Empezar (configuración mínima)
```bash
# Configura tu identidad (solo la primera vez)
git config --global user.name "Tu Nombre"
git config --global user.email "tu@correo.com"
```

```bash
# Clonar un repo remoto
git clone https://github.com/usuario/proyecto.git
```

---

## 🔰 Básico — estado, añadir, commitear y enviar
```bash
# Ver el estado
git status
```

```bash
# Añadir archivos al staging
git add archivo.txt
git add .    # añade todos los cambios
```

```bash
# Crear un commit con mensaje claro
git commit -m "Explica qué y por qué"
```

```bash
# Subir la rama actual al remoto
git push origin nombre-de-la-rama
```

---

## 🌿 Ramas — crear, listar y cambiar
```bash
# Crear y cambiar a una nueva rama
git checkout -b nombre-de-la-rama
```

```bash
# Listar ramas locales
git branch
```

```bash
# Listar ramas remotas
git branch -r
```

```bash
# Ver todas las ramas (local + remoto)
git branch -a
```

---

## 🔁 Actualizar ramas y sincronizar
```bash
# Traer cambios del remoto y fusionar en la rama actual
git pull origin nombre-de-la-rama
```

Consejo: antes de crear una rama nueva, haz `git pull origin main` para partir de la última versión.

---

## 🔀 Fusionar ramas (merge) — flujo típico
```bash
# Cambiar a la rama de destino (ej. main)
git checkout main
```

```bash
# Fusionar la rama feature en main
git merge nombre-de-la-rama
```

```bash
# Subir los cambios fusionados
git push origin main
```

---

## 🔧 Resolver conflictos (pasos compactos)
1. Git marcará los archivos en conflicto.
2. Edita y resuelve manualmente las secciones marcadas (<<<< <<<<).
3. Marcar como resuelto y añadir:
```bash
git add ruta/al/archivo-en-conflicto
```
4. Finalizar con commit y push:
```bash
git commit -m "Resuelto conflicto: breve explicación"
git push origin main
```

---

## 🧰 Intermedio — stash, fetch y rebase
```bash
# Guardar cambios temporalmente
git stash save "mensaje opcional"
# Recuperar último stash
git stash pop
```

```bash
# Traer objetos y referencias desde remoto sin merge automático
git fetch origin
```

```bash
# Rebase interactivo para limpiar commits antes de merge
git checkout feature
git rebase -i main
```

---

## 🏁 Avanzado — reset, reflog, cherry-pick y bisect
```bash
# Reset suave (mover HEAD, mantener cambios en working dir)
git reset --soft HEAD~1
```

```bash
# Reset duro (PELIGRO: descarta cambios)
git reset --hard HEAD~1
```

```bash
# Recuperar commits perdidos usando reflog
git reflog
git checkout <hash>
```

```bash
# Aplicar un commit específico en la rama actual
git cherry-pick <hash-del-commit>
```

```bash
# Git bisect para encontrar el commit que introdujo un bug
git bisect start
git bisect bad
git bisect good <hash-estable>
# seguir el proceso hasta identificar el commit
```

---

## 📡 Operaciones remotas y mantenimiento
```bash
# Listar referencias remotas
git ls-remote --heads origin
```

```bash
# Enviar todas las ramas
git push --all origin
```

```bash
# Borrar una rama remota
git push origin --delete nombre-de-la-rama
```

---

## 💡 Alias útiles (configura en .gitconfig)
```bash
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
```

---

## 🧾 Buenas prácticas y consejos
- Mensajes de commit claros: qué cambiaste y por qué.
- Haz `pull` antes de empezar a trabajar en una rama compartida.
- Usa PRs para revisar cambios en equipo.
- Mantén ramas pequeñas y con propósito único.
- Rebase interactivo para limpiar el historial antes de publicar.

---

## 🛠 Troubleshooting rápido
- Push rechazado: `git pull --rebase origin nombre-de-la-rama` y luego `git push`.
- Deshacer último commit sin borrar cambios:
```bash
git reset --soft HEAD~1
```
- Forzar push (usar con cuidado):
```bash
git push --force-with-lease origin nombre-de-la-rama
```

---

## Recursos rápidos
- Ver historial visual: `git log --oneline --graph --all`
- Documentación oficial: https://git-scm.com/docs

---

*Última actualización: Enero 2026*