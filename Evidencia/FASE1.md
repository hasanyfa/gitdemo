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
-  Agrega al usuario que será tu pareja como colaborador con permisos de escritura
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
-  Añade etiquetas apropiadas (enhancement, documentation, etc.)

**c) ⏳ Esperar aprobación**

-  El revisor evaluará tu código y dejará comentarios si es necesario
-  Realiza las correcciones solicitadas si las hay
-  Una vez aprobado, podrás hacer merge

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

Crea un archivo `README.md` profesional con la siguiente estructura:

```markdown
# 📱 Actividad 8 - App de Notificaciones SMS

## 📋 Descripción

[Descripción breve del proyecto]

## 🎯 Objetivos de aprendizaje

-  Integración con servicios del dispositivo
-  Implementación de Broadcast Receivers
-  Manejo eficiente de hilos en Android

## 🛠️ Tecnologías utilizadas

-  Android SDK API 28
-  Java
-  Broadcast Receivers
-  Notification Manager

## 📱 Funcionalidades

[Lista de características implementadas]
```

**❓ Preguntas de reflexión técnica:**

Responde de manera detallada y fundamentada las siguientes preguntas:

1. **🔋 Integración con servicios del dispositivo:**
   ¿Cómo se pueden desarrollar aplicaciones que se integren con los servicios del dispositivo, como la batería, los mensajes o las notificaciones, de forma eficiente y segura, considerando diferentes tipos de servicios, permisos y la experiencia del usuario?

2. **📡 Broadcast Intents y Receivers:**
   ¿Cómo se pueden utilizar Broadcast Intents y Broadcast Receivers para comunicar diferentes aplicaciones entre sí de forma segura y eficiente, considerando diferentes tipos de acciones, datos y la experiencia del usuario?

3. **🧵 Manejo de hilos:**
   ¿Cómo se pueden utilizar hilos en Android para mejorar la eficiencia y la capacidad de respuesta de una aplicación, considerando diferentes tipos de tareas, la sincronización de datos y la experiencia del usuario?

4. **💭 Reflexión personal:**
   Escribe una reflexión personal sobre los conceptos aprendidos (mínimo 50 palabras). Incluye:
   -  Desafíos enfrentados durante el desarrollo
   -  Conceptos que te resultaron más interesantes
   -  Aplicaciones prácticas en proyectos futuros

## 📱 Desarrollo de la aplicación

### 8. 🛍️ Especificaciones técnicas de la aplicación

**📋 Funcionalidades principales:**

**a) 📞 Vista principal con lista de contactos**

-  Implementa un `RecyclerView` o `ListView` para mostrar números de teléfono
-  Permite agregar/eliminar números de la lista
-  Interfaz intuitiva para gestionar contactos monitoreados

**b) 📨 Servicio BroadcastReceiver para SMS**

-  Crea un `BroadcastReceiver` que escuche el intent `SMS_RECEIVED`
-  Implementa el manejo seguro de permisos (`RECEIVE_SMS`)
-  Procesa mensajes entrantes de forma eficiente

**c) 🔔 Sistema de notificaciones**

-  Genera notificaciones cuando lleguen SMS de números monitoreados
-  Implementa diferentes tipos de notificación:
   -  Toast messages para feedback inmediato
   -  Logging detallado para debugging
   -  Notificaciones del sistema para alertas importantes

**d) 🧵 Manejo de hilos**

-  Utiliza hilos apropiados para operaciones no bloqueantes
-  Implementa `AsyncTask` o `ExecutorService` para tareas en segundo plano
-  Asegura que las actualizaciones de UI se realicen en el hilo principal

**🎨 Especificaciones de diseño:**

**a) 🖼️ Interfaz de usuario**

-  Diseño moderno siguiendo Material Design Guidelines
-  Navegación intuitiva y accesible
-  Componentes responsivos para diferentes tamaños de pantalla

**b) 🎨 Paleta de colores temática**

-  Colores que evoquen comunicación y alerta
-  Contraste adecuado para accesibilidad
-  Consistencia visual en toda la aplicación

**c) 📝 Tipografía y legibilidad**

-  Fuente legible en todos los tamaños
-  Jerarquía tipográfica clara
-  Espaciado apropiado entre elementos
