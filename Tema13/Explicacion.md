# 🗺️ Tema 13. Mapeo

## 📖 Contexto

Hace poco estaba en un evento en el qu🌍 **C🔍 **Controlando el zoom:\*\* Y la cercanía o lejanía del mapa puedes cambiarlo en el zoom a través de moveCamera, prueba poniendo 10, 15 o 20.

🔭 > El zoom es como usar un **telescopio con diferentes lentes**:iando de ciudad:\*\* Puedes modificar la ciudad cambiándola por otra que desees en el código y sustituyendo en donde dice sydney. Las coordenadas de otra ciudad las puedes localizar en la página https://www.coordenadas-gps.com/.

🗺️ > Es como **ca🔧 > Recuerda: ¡La depuración es como ser un **detective digital\*\* - cada error te da pistas para encontrar la solución!

## 🏁 Cierrecanal de TV\*\* - en lugar de ver un programa sobre Sydney, puedes "sintonizar" cualquier otra ciudad del mundo simplemente cambiando las coordenadas.e trata de capacitar a jóvenes en ## ✅ Checkpoint

**Asegúrate de:**

-  ✔️ Conocer los requisitos para hacer uso de Google Maps en el sistema operativo Android.

   🗝️ > Es como obtener las **llaves de un auto** - necesitas los permisos correctos (API Key) para poder "conducir" los mapas en tu aplicación.

-  ✔️ Conocer los requisitos para obtener API KEY.

   🎫 > La API Key es como un **boleto de entrada** a un parque de diversiones. Sin este boleto especial, no puedes acceder a todas las atracciones (funcionalidades) que Google Maps ofrece.imeros respondientes, esto es en un caso de emergencia médica: ser lo más indispensable y eficaz para la víctima mientras llega el auxilio. 🚑 Fue un evento muy gratificante en el que muchos aprendimos, pero lo más importante fue la actividad a desarrollar por los jóvenes además de la capacitación, ellos deberían de hacer una herramienta que previniera e informara a otros en lo importante que es ser primer respondiente.

La mayoría desarrollaron folletos 📄 o videos 🎥, unos pocos hicieron aplicaciones 📱 y lo más maravilloso, usaron google maps 🗺️ para buscar lugares de socorro y ambulancias, es entonces que se vuelve tan importante estar en contacto con el mundo exterior en cuanto a localización a través de una aplicación en el celular.

🌉 > Los mapas en aplicaciones móviles son como **puentes digitales** que conectan el mundo físico con el virtual. Imagínate poder "tocar" cualquier lugar del mundo desde tu teléfono y obtener información instantánea sobre él.

Este tema te ayudará a entender cómo usar en tu celular los mapas de Google para mostrar tu localización y poder hacer uso de sus beneficios. 📍

🎯 **¿Por qué es importante?** Es como tener un **superpoder de orientación** - nunca más te perderás y siempre sabrás qué hay a tu alrededor.

## 📚 Explicación

### 🔧 13.1 Añadiendo el mapeo a una aplicación

Es posible acceder a la herramienta Google Maps por medio de aplicaciones Android utilizando la API de Google Maps para Android (Smyth, 2020).

🧠 **Piensa en esto como:** La API de Google Maps es como un conjunto de herramientas especializadas que Google nos presta para construir aplicaciones con mapas. Es similar a cuando un carpintero usa diferentes herramientas (martillo, sierra, taladro) para construir una casa; cada herramienta tiene un propósito específico.

La API de Google Maps para Android consta de un conjunto básico de clases que se combinan para proporcionar capacidades de mapeo en aplicaciones de Android.

Las principales son las siguientes, de acuerdo con Smyth (2020).

-  **🗺️ GoogleMap**: es la clase principal de la API de Google Maps para Android. Clase responsable de descargar y mostrar mosaicos de mapas y de mostrar y responder a los controles del mapa.

   🏗️ > Es como el **motor de un automóvil** - es la parte principal que hace que todo funcione. Sin el motor, el auto no puede moverse; sin GoogleMap, no puedes mostrar mapas en tu aplicación.

-  **📱 MapView**: subclase de la clase vista que proporciona el lienzo de vista en el que el objeto Google Maps dibuja el mapa, lo que permite colocar un mapa en el diseño de la interfaz de usuario de una actividad.

   🖼️ > Es como un **marco de cuadro** donde colocas una pintura. El MapView es el marco donde se "cuelga" o muestra el mapa dentro de tu aplicación.

-  **🧩 SupportMapFragment**: una subclase de la clase fragment, esta clase permite colocar un mapa dentro de un fragment en un diseño de Android.

   🧩 > Es como una **pieza de rompecabezas** que encaja perfectamente en un diseño más grande. Te permite dividir tu aplicación en secciones y colocar el mapa en una de esas secciones.

-  **📍 Marker**: el propósito de la clase marcador es permitir que las ubicaciones se marquen en un mapa.

   📌 > Es como las **chinchetas rojas** que usas en un mapa físico de papel para marcar lugares importantes. Solo que estas son digitales y pueden tener diferentes colores y formas.

-  **🎨 Formas**: el dibujo de líneas y formas en un mapa se logra mediante el uso de las clases polilínea, polígono y círculo.

   ✏️ > Es como tener **diferentes plumones de colores** para dibujar sobre un mapa. Puedes trazar rutas (líneas), delimitar zonas (polígonos) o marcar áreas de influencia (círculos).

-  **⚙️ UiSettings**: la clase UiSettings proporciona un nivel de control desde dentro de una aplicación cuyos controles de interfaz de usuario aparecen en un mapa.

   🎛️ > Es como el **panel de control** de una televisión. Te permite decidir qué botones mostrar (zoom, rotación) y cuáles ocultar, personalizando la experiencia del usuario.

-  **📍 My Location Layer**: cuando está habilitada, la capa de mi ubicación muestra un botón en el mapa que cuando el usuario lo selecciona, centra el mapa en la ubicación geográfica actual del usuario.

   🧭 > Es como tener una **brújula personal** que siempre te dice "tú estás aquí". Es el punto azul que ves en Google Maps que te muestra exactamente dónde te encuentras.

### ⚡ 13.2 Ejercicio paso a paso: Implementando funcionalidades interactivas

🎯 **Objetivo:** Crear una aplicación Android completa con Google Maps que incluya funcionalidades interactivas como zoom, marcadores y localización en tiempo real.

🎮 > Piensa en tu mapa como un **videojuego de mundo abierto**. Los gestos son como los controles del juego: zoom para acercarte, rotación para cambiar perspectiva y scroll para navegar.

---

#### 📋 **PASO 1: Configuración inicial del proyecto**

**1.1. Crear nuevo proyecto en Android Studio:**

-  API Level: 28 (Android 9.0)
-  Actividad: Empty Activity
-  Nombre: "MiMapaInteractivo"

**1.2. Agregar dependencias en `build.gradle` (Module: app):**

```gradle
dependencies {
    implementation 'com.google.android.gms:play-services-maps:17.0.1'
    implementation 'com.google.android.gms:play-services-location:18.0.0'
    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    implementation 'androidx.core:core:1.3.2'
}
```

💡 **Nota importante:** Estas versiones son específicamente compatibles con API 28. Si usas versiones más nuevas, podrías tener conflictos de compatibilidad.

**1.3. Configurar en `build.gradle` (Module: app) - Sección android:**

```gradle
android {
    compileSdkVersion 28

    defaultConfig {
        applicationId "com.ejemplo.mimapainteractivo"
        minSdkVersion 21
        targetSdkVersion 28
        versionCode 1
        versionName "1.0"
    }

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```

---

#### 🗝️ **PASO 2: Obtener API Key de Google Maps**

**2.1. Ir a Google Cloud Console:**

-  Visita: https://console.cloud.google.com
-  Crea un proyecto nuevo o selecciona uno existente

**2.2. Habilitar APIs:**

-  Maps SDK for Android
-  Places API (opcional)

**2.3. Crear credenciales:**

-  Crear API Key
-  Restringir la key a tu aplicación Android

**2.4. Agregar API Key en `AndroidManifest.xml`:**

```xml
<application>
    <meta-data
        android:name="com.google.android.geo.API_KEY"
        android:value="TU_API_KEY_AQUI" />
    <!-- Resto de la aplicación -->
</application>
```

🔑 > Es como obtener las **llaves de un auto** - sin esta API Key, tu aplicación no puede "conducir" los mapas de Google.

---

#### 📱 **PASO 3: Configurar permisos y layout**

**3.1. Agregar permisos en `AndroidManifest.xml`:**

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
```

**3.2. Crear layout en `activity_main.xml`:**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Mapa principal -->
    <fragment
        android:id="@+id/map"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toTopOf="@id/buttonContainer"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <!-- Contenedor de botones -->
    <LinearLayout
        android:id="@+id/buttonContainer"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="16dp"
        android:background="@color/white"
        app:layout_constraintBottom_toBottomOf="parent">

        <Button
            android:id="@+id/btnNormal"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_margin="4dp"
            android:text="Normal"
            android:textSize="12sp" />

        <Button
            android:id="@+id/btnSatellite"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_margin="4dp"
            android:text="Satélite"
            android:textSize="12sp" />

        <Button
            android:id="@+id/btnMyLocation"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_margin="4dp"
            android:text="Mi Ubicación"
            android:textSize="12sp" />

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```

---

#### 🚀 **PASO 4: Implementar MainActivity.java completo**

```java
package com.ejemplo.mimapainteractivo;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.Manifest;
import android.content.pm.PackageManager;
import android.location.Location;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import com.google.android.gms.location.FusedLocationProviderClient;
import com.google.android.gms.location.LocationServices;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;
import com.google.android.gms.tasks.OnSuccessListener;

public class MainActivity extends AppCompatActivity implements OnMapReadyCallback {

    private GoogleMap mMap;
    private FusedLocationProviderClient fusedLocationClient;
    private Button btnNormal, btnSatellite, btnMyLocation;
    private static final int LOCATION_PERMISSION_REQUEST_CODE = 1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Inicializar el cliente de ubicación
        fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);

        // Inicializar botones
        initializeButtons();

        // Obtener el fragmento del mapa
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }

    private void initializeButtons() {
        btnNormal = findViewById(R.id.btnNormal);
        btnSatellite = findViewById(R.id.btnSatellite);
        btnMyLocation = findViewById(R.id.btnMyLocation);

        // Configurar listeners de botones
        btnNormal.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (mMap != null) {
                    mMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);
                    Toast.makeText(MainActivity.this, "Modo Normal activado", Toast.LENGTH_SHORT).show();
                }
            }
        });

        btnSatellite.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (mMap != null) {
                    mMap.setMapType(GoogleMap.MAP_TYPE_SATELLITE);
                    Toast.makeText(MainActivity.this, "Modo Satélite activado", Toast.LENGTH_SHORT).show();
                }
            }
        });

        btnMyLocation.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                getCurrentLocation();
            }
        });
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;

        // Configurar ubicación inicial (Ciudad de México)
        LatLng ciudadMexico = new LatLng(19.4326, -99.1332);

        // Agregar marcador
        mMap.addMarker(new MarkerOptions()
                .position(ciudadMexico)
                .title("Ciudad de México")
                .snippet("¡Bienvenido a la capital!"));

        // Mover cámara con zoom
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(ciudadMexico, 12));

        // Habilitar controles de zoom
        mMap.getUiSettings().setZoomControlsEnabled(true);
        mMap.getUiSettings().setZoomGesturesEnabled(true);
        mMap.getUiSettings().setScrollGesturesEnabled(true);
        mMap.getUiSettings().setRotateGesturesEnabled(true);
        mMap.getUiSettings().setTiltGesturesEnabled(true);

        // Configurar listener de clicks en el mapa
        mMap.setOnMapClickListener(new GoogleMap.OnMapClickListener() {
            @Override
            public void onMapClick(LatLng latLng) {
                // Agregar marcador donde el usuario toque
                mMap.addMarker(new MarkerOptions()
                        .position(latLng)
                        .title("Nuevo marcador")
                        .snippet("Lat: " + String.format("%.4f", latLng.latitude) +
                                ", Lng: " + String.format("%.4f", latLng.longitude)));

                Toast.makeText(MainActivity.this, "Marcador agregado", Toast.LENGTH_SHORT).show();
            }
        });

        // Solicitar permisos de ubicación
        checkLocationPermission();
    }

    private void checkLocationPermission() {
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                != PackageManager.PERMISSION_GRANTED) {

            ActivityCompat.requestPermissions(this,
                    new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
                    LOCATION_PERMISSION_REQUEST_CODE);
        } else {
            enableMyLocation();
        }
    }

    private void enableMyLocation() {
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                == PackageManager.PERMISSION_GRANTED) {
            mMap.setMyLocationEnabled(true);
            mMap.getUiSettings().setMyLocationButtonEnabled(true);
        }
    }

    private void getCurrentLocation() {
        if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                == PackageManager.PERMISSION_GRANTED) {

            fusedLocationClient.getLastKnownLocation()
                    .addOnSuccessListener(this, new OnSuccessListener<Location>() {
                        @Override
                        public void onSuccess(Location location) {
                            if (location != null) {
                                LatLng currentLocation = new LatLng(location.getLatitude(), location.getLongitude());

                                mMap.addMarker(new MarkerOptions()
                                        .position(currentLocation)
                                        .title("Mi ubicación actual")
                                        .snippet("¡Aquí estoy!"));

                                mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(currentLocation, 15));

                                Toast.makeText(MainActivity.this, "Ubicación encontrada", Toast.LENGTH_SHORT).show();
                            } else {
                                Toast.makeText(MainActivity.this, "No se pudo obtener la ubicación", Toast.LENGTH_SHORT).show();
                            }
                        }
                    });
        } else {
            Toast.makeText(this, "Permisos de ubicación requeridos", Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == LOCATION_PERMISSION_REQUEST_CODE) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                enableMyLocation();
                Toast.makeText(this, "Permisos concedidos", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(this, "Permisos denegados", Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```

---

#### 🎮 **PASO 5: Funcionalidades implementadas**

**✅ Gestos interactivos:**

-  **Zoom** 🔍: Pellizcar para acercar/alejar
-  **Rotación** 🔄: Rotar con dos dedos
-  **Scroll** 📜: Deslizar para navegar
-  **Inclinación** ⛰️: Deslizar hacia arriba/abajo con dos dedos

**✅ Botones funcionales:**

-  **Normal:** Vista de mapa estándar
-  **Satélite:** Vista satelital
-  **Mi Ubicación:** Centrar en ubicación actual

**✅ Marcadores dinámicos:**

-  Toca cualquier parte del mapa para agregar marcadores
-  Muestra coordenadas exactas

**✅ Permisos de ubicación:**

-  Solicitud automática de permisos
-  Manejo de respuestas del usuario

---

#### 🔭 **PASO 6: Personalizar niveles de zoom**

🔭 > El zoom es como usar un **telescopio con diferentes lentes**:

**Niveles de zoom explicados:**

-  **Zoom 1-5**: Vista mundial/continental
-  **Zoom 6-10**: Vista de país/estado
-  **Zoom 11-15**: Vista de ciudad/área metropolitana
-  **Zoom 16-18**: Vista de barrio/zona específica
-  **Zoom 19-21**: Vista de calle/edificios individuales

---

#### 🧪 **PASO 7: Probar la aplicación**

**7.1. Ejecutar en dispositivo o emulador**  
**7.2. Verificar que se muestren los controles**  
**7.3. Probar cada funcionalidad:**

-  ✅ Zoom con pellizco
-  ✅ Rotación del mapa
-  ✅ Cambio entre vista normal y satélite
-  ✅ Agregar marcadores tocando el mapa
-  ✅ Localización actual

🚪 > Pedir permisos es como cuando alguien **toca la puerta de tu casa** y pregunta "¿puedo pasar?". La aplicación respeta tu privacidad.

---

#### 🎯 **Resultado esperado:**

Al completar este ejercicio tendrás una aplicación completamente funcional con:

-  ✅ Mapa interactivo con todos los gestos habilitados
-  ✅ Cambio entre tipos de mapa
-  ✅ Localización en tiempo real
-  ✅ Marcadores dinámicos
-  ✅ Interfaz intuitiva con botones

🛰️ > Tu aplicación funcionará como el **GPS de tu automóvil**, constantemente conectada y lista para mostrar ubicaciones en tiempo real.

---

#### 💡 **Consejos adicionales:**

1. **Para obtener coordenadas:** Visita https://www.coordenadas-gps.com/
2. **Para personalizar marcadores:** Usa `BitmapDescriptorFactory` para iconos personalizados
3. **Para mejorar rendimiento:** Limita la cantidad de marcadores simultáneos
4. **Para producción:** Restringe tu API Key a tu aplicación específica

🎮 > ¡Felicidades! Ahora tienes tu propio **videojuego de exploración mundial** en Android.

---

#### 🛠️ **SOLUCIÓN DE PROBLEMAS COMUNES:**

**❌ Error de dependencias:**
Si tienes errores con las dependencias, verifica que uses las versiones correctas para API 28:

```gradle
// ✅ VERSIONES CORRECTAS PARA API 28
dependencies {
    implementation 'com.google.android.gms:play-services-maps:17.0.1'
    implementation 'com.google.android.gms:play-services-location:18.0.0'
    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    implementation 'androidx.core:core:1.3.2'
}
```

**❌ Error "API key not found":**

-  Verifica que agregaste la API key en `AndroidManifest.xml`
-  Asegúrate de que la API key no tenga espacios extras
-  Confirma que habilitaste "Maps SDK for Android" en Google Cloud Console

**❌ Permisos de ubicación no funcionan:**

-  Verifica que agregaste los permisos en `AndroidManifest.xml`
-  Prueba en un dispositivo físico (el emulador puede tener limitaciones)
-  Ve a Configuración > Apps > Tu App > Permisos y habilita la ubicación manualmente

**❌ Mapa aparece en gris:**

-  Revisa que tu API key sea válida
-  Verifica tu conexión a internet
-  Confirma que la API key tenga restricciones correctas

**❌ App se cierra al abrir:**

-  Revisa el Logcat para ver errores específicos
-  Verifica que todas las dependencias estén sincronizadas
-  Confirma que el `compileSdkVersion` sea 28

🔧 > Recuerda: ¡La depuración es como ser un **detective digital** - cada error te da pistas para encontrar la solución!

-  **Zoom** 🔍: Es como acercarte o alejarte de la acción con el joystick
-  **Rotación** 🔄: Es como girar la cámara para ver desde diferentes ángulos
-  **Scroll** �: Es como mover tu personaje por el mundo del juego

�💡 **Ejemplo basado en YoAndroide (2021).**

🌍 **Cambiando de ciudad:** Puedes modificar la ciudad cambiándola por otra que desees en el código y sustituyendo en donde dice sydney. Las coordenadas de otra ciudad las puedes localizar en la página https://www.coordenadas-gps.com/.

�️ **Analogía:** Es como **cambiar el canal de TV** - en lugar de ver un programa sobre Sydney, puedes "sintonizar" cualquier otra ciudad del mundo simplemente cambiando las coordenadas.

�🔍 **Controlando el zoom:** Y la cercanía o lejanía del mapa puedes cambiarlo en el zoom a través de moveCamera, prueba poniendo 10, 15 o 20.

🔭 **Analogía del telescopio:** El zoom es como usar un **telescopio con diferentes lentes**:

-  **Zoom 10**: Es como ver con binoculares - puedes ver una vista amplia de la ciudad
-  **Zoom 15**: Es como usar un telescopio - enfocas en una zona específica
-  **Zoom 20**: Es como usar un microscopio - puedes ver detalles muy específicos como edificios individuales

El mapa se verá algo similar a lo siguiente:
Ahora modifica el código de la misma actividad principal para agregar un localizador de tiempo real a través de un marcador, quedando de la siguiente manera.

📍 **Localizador en tiempo real:**

🛰️ > Tu teléfono funciona como el **GPS de tu automóvil**. Constantemente está "preguntando" a los satélites "¿dónde estoy?" y actualizando tu posición en tiempo real, como el punto que se mueve en la pantalla cuando conduces.

🔐 Se pide permiso a la aplicación a través de checkSelfPermission, si el usuario otorga el permiso entonces se obtiene la longitud y latitud de la ubicación del usuario, el cual se recibe a través del método LocationListener.

🚪 > Pedir permisos es como cuando alguien **toca la puerta de tu casa** y pregunta "¿puedo pasar?". La aplicación debe pedirte permiso antes de acceder a tu ubicación, respetando tu privacidad.

Al ejecutarlo, la aplicación detecta la ubicación actual del usuario 📍, para lo cual se anexa un ejemplo.

## 🏁 Cierre

🌟 **Reflexión con analogías:**

❓ ¿Cómo se te ocurre que sería interesante añadir esta facilidad a una aplicación?

🏥 > Imagina que tu aplicación es como un **hospital inteligente**. Los mapas pueden ayudar a:

-  Los pacientes a encontrar la sala de emergencias más cercana
-  Los doctores a llegar rápidamente a emergencias
-  Las ambulancias a optimizar sus rutas

💭 ¿Qué tipo de aplicaciones podrían utilizarla?

🎯 **Ejemplos con analogías:**

-  **📱 Apps de delivery:** Como un "repartidor virtual" que siempre sabe dónde estás y dónde está tu comida
-  **� Apps de transporte:** Como un "taxi inteligente" que te encuentra sin necesidad de explicar tu ubicación
-  **🏃‍♂️ Apps de ejercicio:** Como un "entrenador personal" que mapea tus rutas de running
-  **👥 Apps sociales:** Como un "radar de amigos" que te ayuda a encontrar personas cercanas
-  **🏪 Apps comerciales:** Como un "asistente de compras" que te guía a las tiendas más cercanas

�🚀 Cada vez hay más novedades y más aplicaciones que se desarrollan a partir de Google Maps. No dejes de hacer la actividad que te permita reconocer la manera de desarrollar esta facilidad en una aplicación móvil.

💡 > Desarrollar con Google Maps es como ser un **arquitecto digital** - tienes todas las herramientas para construir experiencias que conecten el mundo físico con el digital, creando puentes entre dónde estás y dónde quieres estar.

## ✅ Checkpoint

**Asegúrate de:**

-  ✔️ Conocer los requisitos para hacer uso de Google Maps en el sistema operativo Android.
-  ✔️ Conocer los requisitos para obtener API KEY.

## 📖 Referencias

📚 Smyth, N. (2021). Android Studio Arctic Fox Essentials - Java Edition: Developing Android Apps Using Android. EE. UU.: Payload Media, Inc.

**ISBN-13:** 978-1-951442-36-1

📺 Yo Androide. (2021, 15 de enero). CURSO COMPLETO ANDROID STUDIO 2021 27: Google Maps, marcadores y tipos de mapas [Archivo de video]. Recuperado de https://www.youtube.com/watch?v=egDHSyDaOGg
