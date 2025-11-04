# 🚀 ACTIVIDAD 11 - Desarrollo con Google Maps

## 📝 Desarrollo

### 🤔 Responde las siguientes preguntas:

1. **¿Cuáles son las principales clases de la API de Google Maps para Android y qué función cumple cada una?**

2. **¿Cómo se puede agregar un mapa a una aplicación Android usando la API de Google Maps?**

3. **¿Qué opciones ofrece la API de Google Maps para mostrar la ubicación del usuario en un mapa?**

### ✍️ Reflexión personal del tema

> **Instrucciones:** Elabora una reflexión personal sobre el tema (mínimo 50 palabras)

---

## 🎯 Proyecto Práctico

### 📋 Objetivo

Desarrollar una aplicación Android que permita al usuario:

-  ✅ **Capturar una dirección**
-  ✅ **Buscar la dirección en un mapa**
-  ✅ **Mostrar un marcador personalizado** en la ubicación de la dirección
-  ✅ **Cambiar el tipo de mapa** entre vista predeterminada, satelital y relieve

---

## 🎨 Interfaz de Usuario

La aplicación tendrá una **interfaz sencilla e intuitiva** con los siguientes componentes:

### 📱 Componentes UI

| Componente      | Función            | Descripción                              |
| --------------- | ------------------ | ---------------------------------------- |
| 📝 **EditText** | Entrada de datos   | Para que el usuario ingrese la dirección |
| 🔍 **Button**   | Acción de búsqueda | Para iniciar la búsqueda de la dirección |
| 🗺️ **MapView**  | Visualización      | Para mostrar el mapa interactivo         |
| 📋 **Spinner**  | Selector           | Para cambiar el tipo de mapa             |

---

## ⚙️ Funcionalidades Requeridas

### 1. 📍 **Captura de dirección**

-  El usuario podrá ingresar la dirección **manualmente**
-  Opción de utilizar el **autocompletado del sistema**

### 2. 🔍 **Búsqueda de dirección**

-  La aplicación utilizará la **API de Google Maps** para buscar la ubicación de la dirección ingresada
-  Manejo de errores si la dirección no se encuentra

### 3. 📌 **Mostrar marcador personalizado**

-  Se mostrará un **marcador personalizado** en la ubicación de la dirección
-  El **color del marcador** dependerá del tipo de mapa seleccionado:
   -  🔵 **Azul** para vista predeterminada
   -  🔴 **Rojo** para vista satelital
   -  🟢 **Verde** para vista de relieve

### 4. 🗺️ **Cambio de tipo de mapa**

-  El usuario podrá cambiar entre:
   -  📄 **Vista predeterminada** (Normal)
   -  🛰️ **Vista satelital**
   -  ⛰️ **Vista de relieve** (Terrain)

---

## 💡 Criterios de Evaluación

### ✅ Funcionalidad (40%)

-  Búsqueda correcta de direcciones
-  Marcadores funcionando adecuadamente
-  Cambio de tipos de mapa

### ✅ Interfaz de Usuario (30%)

-  Diseño intuitivo y atractivo
-  Componentes bien organizados
-  Experiencia de usuario fluida

### ✅ Código (20%)

-  Estructura clara y organizada
-  Manejo de errores
-  Buenas prácticas de programación

### ✅ Creatividad (10%)

-  Elementos adicionales
-  Mejoras en la funcionalidad
-  Personalización creativa

---

## 🛠️ Tecnologías Requeridas

-  **📱 Android Studio**
-  **☕ Java** (API Level 28)
-  **🗺️ Google Maps API**
-  **📍 Google Places API** (para autocompletado)
-  **🔑 API Key** de Google Cloud Console

---

## 📚 Recursos Adicionales

-  📖 [Documentación oficial de Google Maps](https://developers.google.com/maps/documentation/android-sdk)
-  🎥 [Tutorial paso a paso en el tema](./Explicacion.md)
-  🌐 [Coordenadas GPS](https://www.coordenadas-gps.com/)

🎯 > ¡Esta actividad te convertirá en un **explorador digital** capaz de navegar cualquier lugar del mundo desde tu aplicación!
