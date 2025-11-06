# 📱 ACTIVIDAD 12 - 🔐 Autenticación Biométrica

## 🎯 Objetivo

📚 En esta actividad deberás poner a prueba lo que aprendiste en el tema sensor.

## ### 8. 🛍️ Especificaciones técnicas de la aplicación

## 🎯 Objetivo

🔐 Desarrollar una aplicación Android que permita al usuario autenticarse mediante su huella digital.

## 🖥️ Interfaz

-  📱 La aplicación tendrá una interfaz sencilla e intuitiva.
-  🔘 Se utilizará un Button para que el usuario inicie el proceso de autenticación.
-  👆 Se utilizará un sensor de huella digital para capturar la huella del usuario.
-  💬 Se mostrará un mensaje al usuario indicando si la autenticación fue exitosa o no.

## ⚙️ Funcionalidades

-  🔐 **Autenticación por huella digital**: la aplicación utilizará la API de Android para la autenticación por huella digital para capturar la huella del usuario y compararla con la huella almacenada en el dispositivo.
-  ✅ **Validación de huella**: la aplicación validará que la huella capturada sea válida y coincida con la huella del usuario.
-  💬 **Mensaje de éxito o error**: se mostrará un mensaje al usuario indicando si la autenticación fue exitosa o no.nicial

### 1. 📁 Creación del repositorio

-  🆕 Crea un nuevo repositorio en GitHub con el nombre `Actividad12`
-  📝 Inicializa el repositorio con un archivo README.md básico
-  💻 Clona el repositorio a tu máquina local

### 2. 👥 Configuración de colaboradores

-  ⚙️ En GitHub, ve a Settings → Manage access
-  ➕ Agrega al usuario `hasanyfa` como colaborador con permisos de escritura
-  ✅ Asegúrate de que la invitación sea aceptada

## 🎨 Configuración del proyecto Android

### 3. 🎨 Diseño y estilos

**a) 🎨 Paleta de colores (`res/values/colors.xml`)**

-  🌈 Visita [Coolors.co](https://coolors.co/) para generar una paleta cohesiva
-  🎯 Define mínimo 8 colores que evoquen comunicación y alerta:
   -  🔵 Colores primarios (2-3 colores)
   -  🟡 Colores secundarios (2-3 colores)
   -  🟢 Colores de acento/terciarios (2-3 colores)
   -  ⚪ Colores de fondo y texto
-  💡 Ejemplo de estructura:

```xml
<color name="primary_blue">#2196F3</color>
<color name="primary_dark">#1976D2</color>
<color name="accent_orange">#FF9800</color>
```

**b) 🔤 Tipografía (`res/font/`)**

-  📥 Descarga una fuente apropiada de [Google Fonts](https://fonts.google.com/)
-  ⭐ Recomendaciones: Roboto, Open Sans, Lato (legibles y modernas)
-  📂 Agrega los archivos .ttf a la carpeta `res/font/`

**c) 🎭 Tema principal (`res/values/themes.xml`)**

-  🎨 Aplica los colores definidos a los componentes del tema
-  🔤 Configura la fuente personalizada
-  📋 Define estilos para componentes específicos (botones, listas, notificaciones)

## 🔄 Flujo de trabajo con Git

### 4. 🌱 Creación de rama de desarrollo

⚡ Antes de realizar cambios, crea una rama específica para el desarrollo:

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

-  🌐 Ve a tu repositorio en GitHub
-  🆕 Crea un nuevo Pull Request desde `feature/configuracion-inicial` hacia `main`
-  📝 Agrega una descripción detallada de los cambios realizados
-  👤 Asigna a `hasanyfa` como revisor
-  🏷️ Añade etiquetas apropiadas (enhancement, documentation, etc.)

**c) ⏳ Esperar aprobación**

-  👀 El revisor evaluará tu código y dejará comentarios si es necesario
-  🔧 Realiza las correcciones solicitadas si las hay
-  ✅ Una vez aprobado, podrás hacer merge

### 6. ✅ Merge y sincronización

**a) 🔗 Realizar merge**

-  ✅ Una vez aprobado el PR, realiza el merge a la rama main
-  🗑️ Elimina la rama feature después del merge exitoso

**b) 🔄 Sincronizar repositorio local**

```bash
# 🔀 Cambiar a rama main
git checkout main

# 🔍 Verificar actualizaciones remotas
git fetch origin

# ⬇️ Descargar cambios
git pull origin main

# 🆕 Crear nueva rama para el desarrollo principal
git checkout -b desarrollo
```

## 📝 Documentación técnica

### 7. 📄 README.md completo

📚 Crea un archivo `README.md` profesional con la siguiente estructura:

```markdown
# 📱 Actividad 12 - 🔐 App de Autenticación Biométrica

## 📋 Descripción

[Descripción breve del proyecto]

## 🎯 Objetivos de aprendizaje

-  🔌 Integración con servicios del dispositivo
-  📡 Implementación de Broadcast Receivers
-  ⚡ Manejo eficiente de hilos en Android

## 🛠️ Tecnologías utilizadas

-  🤖 Android SDK API 28
-  ☕ Java
-  📡 Broadcast Receivers
-  🔔 Notification Manager

## 📱 Funcionalidades

[Lista de características implementadas]

**❓ Preguntas de reflexión técnica:**

🤔 Responde de manera detallada y fundamentada las siguientes preguntas:

1. 🔄 ¿Qué diferencia hay entre un sensor de movimiento basado en hardware y uno basado en software?
2. 📊 ¿Cómo se puede acceder a los datos del sensor de movimiento en una aplicación Android?
3. 📱 Menciona tres ejemplos de aplicaciones que utilizan el sensor de movimiento.
4. 💭 Reflexión personal del tema (mínimo 50 palabras).
```

## 📱 Desarrollo de la aplicación

### 8. 🛍️ Especificaciones técnicas de la aplicación

## Objetivo
Desarrollar una aplicación Android que permita al usuario autenticarse mediante su huella digital.

## Interfaz

-  La aplicación tendrá una interfaz sencilla e intuitiva.
-  Se utilizará un Button para que el usuario inicie el proceso de autenticación.
-  Se utilizará un sensor de huella digital para capturar la huella del usuario.
-  Se mostrará un mensaje al usuario indicando si la autenticación fue exitosa o no.

## Funcionalidades

-  Autenticación por huella digital: la aplicación utilizará la API de Android para la autenticación por huella digital para capturar la huella del usuario y compararla con la huella almacenada en el dispositivo.
-  Validación de huella: la aplicación validará que la huella capturada sea válida y coincida con la huella del usuario.
-  Mensaje de éxito o error: se mostrará un mensaje al usuario indicando si la autenticación fue exitosa o no.
