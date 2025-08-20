# Guía de Git para Android Studio - Paso a Paso

## 📱 Configuración Inicial del Proyecto

### 1. Crear proyecto en Android Studio

-  Abre Android Studio
-  File → New → New Project
-  Configura el nombre del proyecto, paquete y ubicación
-  Selecciona la API mínima y finaliza la creación

### 2. Configurar .gitignore

-  Copia el archivo `.gitignore` en la carpeta raíz del proyecto
-  **¿Por qué?** Este archivo evita subir archivos innecesarios como compilaciones, configuraciones locales, etc.

## 🌐 Configuración del Repositorio Remoto

### 3. Crear repositorio en GitHub

1. Ve a [github.com](https://github.com)
2. Click en el botón **"New repository"**
3. Nombra tu repositorio (ej: `mi-app-android`)
4. **NO** marques "Initialize this repository with a README"
5. Click **"Create repository"**
6. **Copia la URL** del repositorio que aparece (ej: `https://github.com/usuario/mi-app-android.git`)

## 💻 Comandos de Terminal en Android Studio

### 4. Configuración inicial de Git (SOLO LA PRIMERA VEZ)

Abre la terminal en Android Studio: **View → Tool Windows → Terminal**

```bash
# Inicializar repositorio Git local
git init

# Configurar tu identidad (reemplaza con tus datos)
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@gmail.com"

# Agregar todos los archivos al staging area
git add .

# Crear el primer commit
git commit -m "Primer commit - Proyecto inicial"

# Cambiar la rama principal a 'main'
git branch -M main

# Conectar con el repositorio remoto (reemplaza con tu URL)
git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git

# Subir los cambios por primera vez
git push -u origin main
```

## 🔄 Flujo de Trabajo Diario

### 5. Para las siguientes veces (después de hacer cambios):

```bash
# 1. Verificar qué archivos han cambiado
git status

# 2. Agregar archivos modificados al staging area
git add .
# También puedes agregar archivos específicos:
# git add nombre_archivo.java

# 3. Crear un commit con mensaje descriptivo
git commit -m "Descripción clara de los cambios realizados"

# 4. Subir los cambios al repositorio remoto
git push origin main
```

## 🔧 Comandos Útiles Adicionales

### Verificar el estado de tu repositorio:

```bash
git status          # Ver archivos modificados
git log --oneline   # Ver historial de commits
git remote -v       # Ver repositorios remotos configurados
```

### Si cometes errores:

```bash
# Deshacer cambios en un archivo (antes de git add)
git checkout -- nombre_archivo.java

# Deshacer el último commit (mantiene los cambios)
git reset --soft HEAD~1

# Ver diferencias antes de hacer commit
git diff
```

## ⚠️ Consejos Importantes

1. **Mensajes de commit claros**:

   -  ✅ "Agregada funcionalidad de login"
   -  ❌ "cambios varios"

2. **Commits frecuentes**: Haz commits pequeños y frecuentes en lugar de uno grande

3. **Antes de push**: Siempre verifica con `git status` qué vas a subir

4. **Backup**: Git es tu respaldo, úsalo frecuentemente

## 🚨 Solución de Problemas Comunes

### Error: "fatal: not a git repository"

```bash
# Asegúrate de estar en la carpeta correcta del proyecto
pwd
# Si no estás en la carpeta del proyecto, navega a ella
cd ruta/a/tu/proyecto
```

### Error: "failed to push"

```bash
# Primero descarga los cambios remotos
git pull origin main
# Luego intenta subir de nuevo
git push origin main
```

### Error: "merge conflict"

1. Abre los archivos en conflicto
2. Busca las marcas `<<<<<<<`, `=======`, `>>>>>>>`
3. Edita manualmente para resolver el conflicto
4. Guarda el archivo
5. `git add archivo_resuelto.java`
6. `git commit -m "Resuelto conflicto de merge"`
