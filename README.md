# 📌 Guía Básica de Git – Cheat Sheet

## ⚙️ Configuración inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --list
```

## 📂 Crear repositorio

```bash
git init
git clone https://github.com/usuario/repositorio.git
```

## 📝 Flujo básico

```bash
git status
git add archivo.txt
git add .
git commit -m "Mensaje"
git push origin main
```

## 🌿 Manejo de ramas

```bash
git branch nombre-rama
git checkout nombre-rama
git checkout -b nombre-rama
git merge nombre-rama
git branch -d nombre-rama
```

## 👥 Trabajo en equipo

```bash
git pull
git fetch
```

👉 Si hay conflictos, resolver manualmente y hacer:

```bash
git add archivo.txt
git commit -m "Conflicto resuelto"
```

## ✅ Buenas prácticas

-  Usa mensajes claros en los commits.
-  Haz `pull` antes de `push`.
-  Crea ramas para cada nueva función o bugfix.
-  Elimina ramas que ya no uses después del merge.
