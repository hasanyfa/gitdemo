# 📱 Tema 12: Reproducción de Video en Android

## 12.1 Desplegando Video

### 📋 Introducción Técnica

Uno de los usos principales de los teléfonos inteligentes y las tabletas es brindar acceso a contenido en línea, siendo el más utilizado el video (Smyth, 2020).

El SDK de Android incluye dos clases que hacen que la implementación de la reproducción de video en dispositivos Android sea extremadamente fácil de implementar al desarrollar aplicaciones. La forma más sencilla de mostrar video dentro de una aplicación es utilizar la clase `VideoView`; que es un componente visual que cuando se agrega al diseño de una actividad proporciona una superficie en la que se puede reproducir un video (Smyth, 2020).

### 📂 Fuentes de Reproducción de Video

Es posible reproducir audio y video desde orígenes distintos (UNIVERSIDAD POLITÉCNICA DE VALENCIA, s.f.):

-  **Desde un folder almacenado en el dispositivo**
-  **Desde un recurso que está incrustado en el paquete de la aplicación** (archivo .apk)
-  **Desde un stream que es leído desde una conexión de red**. En este punto admite dos posibles protocolos (`http://` y `rstp://`)

### 🛠️ Clases Multimedia de Android

De acuerdo con la UNIVERSIDAD POLITÉCNICA DE VALENCIA (s.f.), Android cuenta con clases que nos permitirán acceder a los servicios Multimedia:

-  **MediaPlayer**: reproducción de audio/video desde ficheros o streams.
-  **MediaController**: visualiza controles estándar para mediaPlayer (pausa, stop, entre otros).
-  **VideoView**: vista que permite la reproducción de video.
-  **MediaRecorder**: permite grabar audio y video.
-  **AsyncPlayer**: reproduce lista de audios desde un thread secundario.
-  **AudioManager**: gestiona varias propiedades del sistema (volumen, tonos).
-  **AudioTrack**: reproduce un búfer de audio PCM directamente por hardware.
-  **SoundPool**: maneja y reproduce una colección de recursos de audio.
-  **JetPlayer**: reproduce audio y video interactivo creado con JetCreator.
-  **Camera**: indica cómo utilizar la cámara para tomar fotos y video.
-  **FaceDetector**: identifica la cara de la gente en un bitmap.

> **💡 Tip**: La forma más fácil de incluir un video en tu aplicación es incluir una vista de tipo `VideoView`.

---

## 🎬 Explicación con Analogías: Android como un Cine Personal

### **VideoView: Tu Pantalla de Cine Portátil**

Imagina que el `VideoView` es como una **pantalla de cine portátil** 📺. Así como en un cine tienes una pantalla donde se proyectan las películas, el VideoView es esa "pantalla" que colocas dentro de tu aplicación donde aparecerán los videos. Es tan fácil como poner un televisor en tu sala - solo lo conectas y ya tienes donde ver contenido.

### **🎭 Fuentes de Video: Diferentes Formas de Obtener Películas**

Las tres fuentes de video son como diferentes maneras de conseguir películas para ver:

#### 1. 💾 **Desde un folder del dispositivo**

**= Como tener un DVD personal en casa**

-  Son videos que ya tienes guardados en tu teléfono, como tus videos familiares o películas descargadas

#### 2. 📦 **Desde recursos incrustados (.apk)**

**= Como una película incluida en una consola de videojuegos**

-  El video viene "empacado" con tu aplicación, como los videos introductorios que vienen incluidos en un juego

#### 3. 🌐 **Desde un stream de red**

**= Como Netflix o YouTube**

-  Los videos se transmiten desde internet en tiempo real usando protocolos como HTTP o RTSP

### **🎪 Las Clases Multimedia: El Equipo de Producción de tu Cine**

Cada clase es como un miembro especializado del equipo de un cine:

#### 🎭 **MediaPlayer**: El Proyeccionista

-  Es quien realmente reproduce el contenido, como el operador que maneja el proyector en un cine
-  Puede trabajar con películas (archivos) o transmisiones en vivo

#### 🎮 **MediaController**: El Control Remoto Universal

-  Como el control remoto de tu TV que tiene botones de play, pausa, stop
-  Te da los controles estándar sin tener que inventarlos tú mismo

#### 📺 **VideoView**: La Pantalla del Cine

-  Es donde se ve todo el contenido visual
-  Como la pantalla principal de un cine donde se proyectan las películas

#### 📹 **MediaRecorder**: El Camarógrafo

-  Como un director de fotografía que graba nuevas películas
-  Te permite crear contenido nuevo (grabar audio y video)

#### 🎵 **AsyncPlayer**: El DJ de la Radio

-  Como un DJ que reproduce una playlist automáticamente en segundo plano
-  Maneja listas de audio sin interrumpir otras tareas

#### 🔊 **AudioManager**: El Técnico de Sonido

-  Como el ingeniero de audio en un concierto que controla volúmenes y efectos
-  Maneja todas las propiedades del sonido del sistema

#### 🎼 **AudioTrack**: El Altavoz Directo

-  Como conectar directamente los auriculares al amplificador
-  Reproduce audio de manera muy directa, sin intermediarios

#### 🎪 **SoundPool**: El Organizador de Efectos Especiales

-  Como el técnico que tiene una mesa llena de botones para efectos de sonido
-  Perfecto para juegos donde necesitas muchos sonidos cortos (explosiones, clicks, etc.)

#### 🎹 **JetPlayer**: El Director de Orquesta Interactiva

-  Como un director que puede cambiar la música según lo que pasa en la obra
-  Para contenido que cambia según las acciones del usuario

#### 📸 **Camera**: El Fotógrafo/Camarógrafo

-  Obviamente, como el fotógrafo profesional del equipo
-  Controla la cámara para tomar fotos y grabar videos

#### 👤 **FaceDetector**: El Especialista en Reconocimiento

-  Como el portero de un club exclusivo que reconoce caras
-  Identifica rostros en las imágenes

---

## 🎯 **Conclusión: Tu Cine Personal en Android**

Implementar video en Android es como **montar tu propio cine personal**:

✅ **Tienes una pantalla** (VideoView)  
✅ **Tienes diferentes fuentes de contenido** (local, empacado, o streaming)  
✅ **Tienes un equipo completo de especialistas** (las clases) que se encargan de cada aspecto

### 🌟 **La Magia de Android**

La belleza está en que Android ya te da todas estas "herramientas profesionales" pre-construidas. Es como si te dieran un cine completo con equipo y personal especializado - **tú solo decides qué película quieres mostrar y dónde colocar la pantalla**.

> **💡 Recuerda**: Con `VideoView` tienes la solución más sencilla para mostrar videos en tu aplicación Android. ¡Es tan fácil como colocar una TV en tu app! 📱✨

---

---

## 💻 **Ejemplo Práctico: Implementando Video en Android (API 28 - Java)**

### 🛠️ **Paso 1: Layout XML (activity_main.xml)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Mi Reproductor de Video"
        android:textSize="20sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="16dp" />

    <!-- VideoView: Nuestra "pantalla de cine" -->
    <VideoView
        android:id="@+id/videoView"
        android:layout_width="match_parent"
        android:layout_height="250dp"
        android:layout_marginBottom="16dp"
        android:background="#000000" />

    <!-- Botones de control -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">

        <Button
            android:id="@+id/btnPlay"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="▶ Play"
            android:layout_margin="8dp" />

        <Button
            android:id="@+id/btnPause"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="⏸ Pause"
            android:layout_margin="8dp" />

        <Button
            android:id="@+id/btnStop"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="⏹ Stop"
            android:layout_margin="8dp" />

    </LinearLayout>

    <!-- Información del video -->
    <TextView
        android:id="@+id/txtStatus"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Estado: Listo para reproducir"
        android:textSize="14sp"
        android:layout_marginTop="16dp"
        android:gravity="center" />

</LinearLayout>
```

### 🎯 **Paso 2: Código Java (MainActivity.java)**

```java
package com.ejemplo.videoplayer;

import android.app.Activity;
import android.media.MediaController;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.VideoView;
import android.widget.Toast;

public class MainActivity extends Activity {

    // Nuestros componentes de la "sala de cine"
    private VideoView videoView;
    private Button btnPlay, btnPause, btnStop;
    private TextView txtStatus;
    private MediaController mediaController;

    // URL del video (puedes cambiarla por tu propia URL)
    private String videoUrl = "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 🎬 Iniciamos nuestro "cine personal"
        initializeComponents();
        setupVideoView();
        setupButtonListeners();
    }

    /**
     * 🎯 Inicializar los componentes de la UI
     */
    private void initializeComponents() {
        videoView = findViewById(R.id.videoView);
        btnPlay = findViewById(R.id.btnPlay);
        btnPause = findViewById(R.id.btnPause);
        btnStop = findViewById(R.id.btnStop);
        txtStatus = findViewById(R.id.txtStatus);

        updateStatus("Componentes inicializados");
    }

    /**
     * 📺 Configurar nuestro VideoView (la pantalla del cine)
     */
    private void setupVideoView() {
        try {
            // Crear el MediaController (nuestro "control remoto")
            mediaController = new MediaController(this);
            mediaController.setAnchorView(videoView);

            // Asignar el MediaController al VideoView
            videoView.setMediaController(mediaController);

            // Configurar la URI del video
            Uri videoUri = Uri.parse(videoUrl);
            videoView.setVideoURI(videoUri);

            // Configurar listeners para eventos del video
            setupVideoListeners();

            updateStatus("VideoView configurado correctamente");

        } catch (Exception e) {
            updateStatus("Error al configurar video: " + e.getMessage());
            Toast.makeText(this, "Error al cargar el video", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * 🎭 Configurar los listeners para eventos del video
     */
    private void setupVideoListeners() {

        // Cuando el video está preparado para reproducir
        videoView.setOnPreparedListener(mediaPlayer -> {
            updateStatus("Video listo para reproducir");
            Toast.makeText(MainActivity.this, "¡Video preparado! 🎬", Toast.LENGTH_SHORT).show();
        });

        // Cuando el video termina de reproducirse
        videoView.setOnCompletionListener(mediaPlayer -> {
            updateStatus("Reproducción completada");
            Toast.makeText(MainActivity.this, "¡Video terminado! 🎉", Toast.LENGTH_SHORT).show();
        });

        // Si hay un error al reproducir
        videoView.setOnErrorListener((mediaPlayer, what, extra) -> {
            updateStatus("Error en la reproducción");
            Toast.makeText(MainActivity.this, "Error al reproducir video 😞", Toast.LENGTH_SHORT).show();
            return true;
        });
    }

    /**
     * 🎮 Configurar los botones de control
     */
    private void setupButtonListeners() {

        // Botón Play ▶
        btnPlay.setOnClickListener(view -> {
            if (!videoView.isPlaying()) {
                videoView.start();
                updateStatus("Reproduciendo...");
                Toast.makeText(this, "▶ Reproduciendo", Toast.LENGTH_SHORT).show();
            }
        });

        // Botón Pause ⏸
        btnPause.setOnClickListener(view -> {
            if (videoView.isPlaying()) {
                videoView.pause();
                updateStatus("Pausado");
                Toast.makeText(this, "⏸ Pausado", Toast.LENGTH_SHORT).show();
            }
        });

        // Botón Stop ⏹
        btnStop.setOnClickListener(view -> {
            if (videoView.isPlaying()) {
                videoView.stopPlayback();
                setupVideoView(); // Reinicializar el video
                updateStatus("Detenido");
                Toast.makeText(this, "⏹ Detenido", Toast.LENGTH_SHORT).show();
            }
        });
    }

    /**
     * 📝 Actualizar el estado mostrado al usuario
     */
    private void updateStatus(String status) {
        txtStatus.setText("Estado: " + status);
    }

    @Override
    protected void onPause() {
        super.onPause();
        // Pausar el video si la actividad se pausa
        if (videoView.isPlaying()) {
            videoView.pause();
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // Liberar recursos del video
        if (videoView != null) {
            videoView.stopPlayback();
        }
    }
}
```

### 📋 **Paso 3: Permisos en AndroidManifest.xml**

```xml
<!-- Permiso para acceso a internet (para videos streaming) -->
<uses-permission android:name="android.permission.INTERNET" />

<!-- Permiso para acceso al estado de la red -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

<!-- Si planeas usar videos del almacenamiento del dispositivo -->
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

### 🎯 **Variantes del Ejemplo:**

#### **📱 Para Video Local (desde la carpeta assets):**

```java
// En lugar de URL, usar un archivo local
Uri videoUri = Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.mi_video);
videoView.setVideoURI(videoUri);
```

#### **💾 Para Video del Almacenamiento del Dispositivo:**

```java
// Usar un archivo del almacenamiento interno/externo
Uri videoUri = Uri.parse("/storage/emulated/0/DCIM/Camera/mi_video.mp4");
videoView.setVideoURI(videoUri);
```

### 🌟 **Características del Ejemplo:**

✅ **Compatible con API 28** (Android 9.0)  
✅ **Código Java puro** sin dependencias externas  
✅ **VideoView simple** para fácil implementación  
✅ **MediaController incluido** para controles básicos  
✅ **Manejo de errores** y estados del video  
✅ **Controles personalizados** adicionales  
✅ **Gestión del ciclo de vida** de la actividad

### 💡 **Tips Importantes:**

🔹 **Para videos grandes**: Considera usar `ExoPlayer` en lugar de `VideoView`  
🔹 **Formatos soportados**: MP4, 3GP, WebM  
🔹 **Red necesaria**: Para videos streaming, asegúrate de tener conexión a internet  
🔹 **Rendimiento**: `VideoView` es ideal para videos simples, no para aplicaciones profesionales de video

---

### 📚 **Referencias**

-  Smyth, N. (2020). _Android Development_
-  Universidad Politécnica de Valencia. (s.f.). _Servicios Multimedia en Android_
