# PROYECTO DE DESARROLLO DE APLICACIONES MÓVILES EN ANDROID

## FASE 1

### 🎯 Objetivo

Desarrollar una aplicación Android que integre todos los concocimientos aprendidos en el primer y segundo parcial, por lo menos debe de tener aplicados del tema 4 al tema 10. Los temas son:

-

### 🚀 Configuración inicial

### 1. 📁 Creación del repositorio

-  Crea un nuevo repositorio en GitHub con el nombre `Actividad08`
-  Inicializa el repositorio con un archivo README.md básico
-  Clona el repositorio a tu máquina local

### 2. 👥 Configuración de colaboradores

-  En GitHub, ve a Settings → Manage access
-  Agrega al usuario `hasanyfa` como colaborador con permisos de lectura
-  Agrega al usuario que será compañero de equipo como colaborador con permisos de escritura
-  Asegúrate de que la invitación sea aceptada

## 🎨 Configuración del proyecto Android

### 3. 🎨 Diseño y estilos

**a) 🎨 Paleta de colores (`res/values/colors.xml`)**

-  Visita [Coolors.co](https://coolors.co/) para generar una paleta cohesiva
-  Define mínimo 8 colores que evoquen comunicación y alerta:
   -  Colores primarios (2-3 colores)
   -  Colores secundarios (2-3 colores)
   -  Colores de acento/terciarios (2-3 colores)
   -  Colores de fondo y texto
-  Ejemplo de estructura:

```xml
<color name="primary_blue">#2196F3</color>
<color name="primary_dark">#1976D2</color>
<color name="accent_orange">#FF9800</color>
```

**b) 🔤 Tipografía (`res/font/`)**

-  Descarga una fuente apropiada de [Google Fonts](https://fonts.google.com/)
-  Recomendaciones: Roboto, Open Sans, Lato (legibles y modernas)
-  Agrega los archivos .ttf a la carpeta `res/font/`

**c) 🎭 Tema principal (`res/values/themes.xml`)**

-  Aplica los colores definidos a los componentes del tema
-  Configura la fuente personalizada
-  Define estilos para componentes específicos (botones, listas, notificaciones)

## 🔄 Flujo de trabajo con Git

### 4. 🌱 Creación de rama de desarrollo

Antes de realizar cambios, crea una rama específica para el desarrollo:

```bash
git checkout -b feature/configuracion-inicial
```

### 5. 📬 Pull Request y revisión de código

**a) 📤 Subir cambios**

```bash
git add .
git commit -m "feat: configuración inicial del proyecto - colores, fuentes y temas"
git push origin feature/configuracion-inicial
```

**b) 🔍 Crear Pull Request**

-  Ve a tu repositorio en GitHub
-  Crea un nuevo Pull Request desde `feature/configuracion-inicial` hacia `main`
-  Agrega una descripción detallada de los cambios realizados
-  Asigna a `hasanyfa` como revisor
-  Asigna a tu compañero como revisor
-  Añade etiquetas apropiadas (enhancement, documentation, etc.)

**c) ⏳ Esperar aprobación**

-  Su compañero deberá evaluar tu código y dejará comentarios si es necesario
-  Realiza las correcciones solicitadas si las hay
-  Una vez aprobado, podrás hacer merge
   \*\* La aprobación únicamente será de tu compañero de equipo

### 6. ✅ Merge y sincronización

**a) 🔗 Realizar merge**

-  Una vez aprobado el PR, realiza el merge a la rama main
-  Elimina la rama feature después del merge exitoso

**b) 🔄 Sincronizar repositorio local**

```bash
# Cambiar a rama main
git checkout main

# Verificar actualizaciones remotas
git fetch origin

# Descargar cambios
git pull origin main

# Crear nueva rama para el desarrollo principal
git checkout -b desarrollo
```

## 📝 Documentación técnica

### 7. 📄 README.md completo

Crea un archivo `README.md` profesional con la descripción de su aplicación.
