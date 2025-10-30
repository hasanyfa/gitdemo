# 📱 Actividad 10: Multimedia en Android# Multimedia

## 🔧 Requisitos Técnicosrequisitos:

android con java

-  **Plataforma**: Android con Javaapi 28

-  **API Level**: 28 (Android 9.0 - Pie)

-  **IDE**: Android Studio## Desarrollo

---Responde las siguientes preguntas en un archivo de tipo markdown y agregalo a tu proyecto.

¿Qué ventajas ofrece el uso de la clase VideoView para reproducir videos en una aplicación Android?

## 📝 Desarrollo Teórico¿Cuáles son los diferentes orígenes desde donde se puede reproducir audio y video en una aplicación Android?

Menciona al menos cuatro clases de Android que permiten acceder a los servicios multimedia y describe brevemente su función.

### Responde las siguientes preguntas en formato markdown:Reflexión personal del tema (mínimo 50 palabras).

Elabora el siguiente proyecto.

#### 1. 🎬 **¿Qué ventajas ofrece el uso de la clase VideoView para reproducir videos en una aplicación Android?**Desarrollar una aplicación Android que funcione como una galería de fotos con las siguientes características:

_[Espacio para tu respuesta]_## Interfaz

---La aplicación tendrá una interfaz sencilla e intuitiva.

Se utilizará un ViewPager para mostrar las fotos de forma horizontal.

#### 2. 📂 **¿Cuáles son los diferentes orígenes desde donde se puede reproducir audio y video en una aplicación Android?**Cada foto se mostrará en una tarjeta con un diseño atractivo.

Se mostrarán indicadores de posición para que el usuario sepa en qué foto se encuentra.

*[Espacio para tu respuesta]*Se incluirá un botón para navegar entre las fotos.

---## Funcionalidades

#### 3. 🛠️ **Menciona al menos cuatro clases de Android que permiten acceder a los servicios multimedia y describe brevemente su función.**Desplazamiento horizontal: el usuario podrá desplazarse por las fotos de forma horizontal deslizando el dedo sobre la pantalla.

Navegación por menú: el usuario podrá acceder a un menú que mostrará las fotos en miniatura. Desde este menú, el usuario podrá seleccionar una foto para verla en pantalla completa.

*[Espacio para tu respuesta]*Selección de fotos: el usuario podrá seleccionar una o varias fotos para realizar acciones como compartirlas o eliminarlas.

---## Elementos

#### 4. 💭 **Reflexión Personal del Tema** *(mínimo 50 palabras)*Tarjetas: se utilizarán tarjetas para mostrar cada foto. Las tarjetas tendrán un diseño atractivo que incluya la imagen, el título y la descripción de la foto.

Indicadores de posición: se mostrarán indicadores de posición para que el usuario sepa en qué foto se encuentra.

*[Espacio para tu reflexión personal]*Botón de navegación: se incluirá un botón para navegar entre las fotos.

---

## 🏗️ Proyecto Práctico: Galería de Fotos

### 📋 **Descripción General**

Desarrollar una aplicación Android que funcione como una **galería de fotos** moderna e intuitiva con navegación horizontal y funcionalidades avanzadas.

---

## 🎨 Diseño de Interfaz

### **Características Principales:**

-  ✅ **Interfaz sencilla e intuitiva**
-  ✅ **Diseño moderno y atractivo**
-  ✅ **Navegación fluida y responsiva**
-  ✅ **Compatibilidad con diferentes tamaños de pantalla**

### **Componentes de UI:**

#### 📱 **ViewPager para Navegación Horizontal**

-  Permite deslizar horizontalmente entre fotos
-  Transiciones suaves y naturales
-  Soporte para gestos táctiles

#### 🃏 **Sistema de Tarjetas (Cards)**

-  Cada foto se muestra en una tarjeta elegante
-  Incluye imagen, título y descripción
-  Diseño Material Design

#### 🔢 **Indicadores de Posición**

-  Muestra la posición actual en la galería
-  Indicadores visuales claros
-  Navegación rápida entre elementos

#### 🧭 **Botones de Navegación**

-  Controles intuitivos para moverse entre fotos
-  Botones anterior/siguiente
-  Acceso rápido a funciones principales

---

## ⚙️ Funcionalidades Principales

### **🔄 Navegación e Interacción:**

#### **1. 👆 Desplazamiento Horizontal**

-  **Funcionalidad**: Navegación táctil fluida
-  **Implementación**: Gestos de deslizamiento izquierda/derecha
-  **UX**: Transiciones animadas entre fotos

#### **2. 📋 Navegación por Menú**

-  **Vista de miniaturas**: Grid con todas las fotos
-  **Selección rápida**: Tap para ver en pantalla completa
-  **Organización**: Ordenamiento por fecha/nombre

#### **3. ✅ Selección Múltiple**

-  **Modo selección**: Activación con long press
-  **Acciones disponibles**:
   -  📤 **Compartir**: Enviar por email/redes sociales
   -  🗑️ **Eliminar**: Borrar fotos seleccionadas
   -  📁 **Organizar**: Mover a álbumes

---

## 🧩 Elementos de Diseño

### **🃏 Tarjetas (Cards)**

```markdown
┌─────────────────────────┐
│ [IMAGEN FOTO] │
│ │
├─────────────────────────┤
│ 📸 Título de la Foto │
│ 📝 Descripción breve │
│ 📅 Fecha: DD/MM/YYYY │
└─────────────────────────┘
```

**Características:**

-  ✨ Sombras y elevación para profundidad
-  🎨 Esquinas redondeadas
-  📱 Responsive design
-  🖼️ Imagen con aspect ratio optimizado

### **🔢 Indicadores de Posición**

```markdown
● ○ ○ ○ ○ [3 de 5]
```

**Características:**

-  🔵 Punto activo destacado
-  ⚪ Puntos inactivos tenues
-  📊 Contador numérico opcional
-  🎯 Navegación directa al tocar

### **🧭 Botones de Navegación**

```markdown
[◀ Anterior] [🏠 Inicio] [Siguiente ▶]
```

**Características:**

-  🎨 Iconos Material Design
-  🔘 Estados visual feedback
-  ♿ Accesibilidad completa
-  📱 Tamaño touch-friendly

---

## 🔧 Especificaciones Técnicas

### **📚 Librerías Recomendadas:**

-  **ViewPager2**: Para navegación horizontal
-  **RecyclerView**: Para grid de miniaturas
-  **Glide/Picasso**: Para carga de imágenes
-  **Material Components**: Para UI moderna

### **🗂️ Estructura de Archivos:**

```
app/src/main/
├── java/com/ejemplo/galeria/
│   ├── MainActivity.java
│   ├── adapters/
│   │   ├── PhotoPagerAdapter.java
│   │   └── ThumbnailAdapter.java
│   ├── models/
│   │   └── Photo.java
│   └── utils/
│       └── ImageLoader.java
├── res/
│   ├── layout/
│   │   ├── activity_main.xml
│   │   ├── item_photo_card.xml
│   │   └── item_thumbnail.xml
│   ├── drawable/
│   └── values/
└── assets/
    └── sample_photos/
```

### **🎯 Objetivos de Aprendizaje:**

-  📱 Implementar ViewPager2 para navegación
-  🖼️ Manejo eficiente de imágenes
-  🎨 Aplicar principios de Material Design
-  ⚡ Optimizar rendimiento con lazy loading
-  🧪 Testing de UI y funcionalidades

---

## 📈 Criterios de Evaluación

| Criterio             | Peso | Descripción                             |
| -------------------- | ---- | --------------------------------------- |
| **🎨 Diseño UI**     | 25%  | Interfaz atractiva y usable             |
| **⚙️ Funcionalidad** | 30%  | Todas las características implementadas |
| **📱 UX**            | 20%  | Experiencia de usuario fluida           |
| **🔧 Código**        | 15%  | Calidad y organización del código       |
| **📝 Documentación** | 10%  | Respuestas teóricas completas           |

---

## 🚀 Entregables

### **📦 Archivos Requeridos:**

1. **📱 Proyecto Android completo**

   -  Código fuente organizado
   -  APK funcional
   -  Screenshots de la aplicación

2. **📄 Documentación**

   -  Respuestas a preguntas teóricas
   -  Manual de usuario
   -  Comentarios en el código

3. **🎥 Demo (Opcional)**
   -  Video mostrando funcionalidades
   -  Explicación de características principales

---

## 💡 Tips de Desarrollo

### **🎯 Mejores Prácticas:**

-  🏗️ **Arquitectura**: Usar patrón MVP o MVVM
-  📸 **Imágenes**: Implementar lazy loading y cache
-  🔄 **Estados**: Manejar rotación de pantalla
-  ⚡ **Performance**: Optimizar memoria y CPU
-  🧪 **Testing**: Incluir pruebas unitarias básicas

### **🔍 Puntos de Atención:**

-  📱 **Compatibilidad**: Probar en diferentes dispositivos
-  🎨 **Responsive**: Adaptar a tablets y phones
-  ♿ **Accesibilidad**: Incluir content descriptions
-  🔒 **Permisos**: Manejar acceso a almacenamiento

---

## 📚 Recursos Adicionales

-  📖 [Documentación ViewPager2](https://developer.android.com/guide/navigation/navigation-swipe-view-2)
-  🎨 [Material Design Guidelines](https://material.io/design)
-  🖼️ [Glide Documentation](https://bumptech.github.io/glide/)
-  📱 [Android UI Best Practices](https://developer.android.com/guide/topics/ui/look-and-feel)

---

> **💡 Nota**: Esta actividad integra conceptos de multimedia, UI/UX design y buenas prácticas de desarrollo Android. ¡Enfócate en crear una experiencia de usuario excepcional!
