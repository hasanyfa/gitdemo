# 🎵 Tema 12: Sonido y Audio en Android12.3 Sonido y audio

## 12.3 Sonido y AudioDe acuerdo con Programador clic (s.f.), MediaPlayer es usado para reproducir archivos de audio y video y establece la ruta del archivo con el método setDataSource ().

### 📋 Introducción TécnicaMediaPlayer opera con los siguientes estados: inactivo, inicializado, preparado, inicio, pausa, parada, reproducción, completado, finalización, error.

El manejo de audio en Android es fundamental para crear experiencias multimedia completas. Android proporciona múltiples APIs para reproducir, grabar y manipular audio, siendo las principales `MediaPlayer` para reproducción y `MediaRecorder` para grabación.Cuando se crea el mediaplayer con new o se llama al método reset (), el mediaplayer está en estado inactivo, debe llamar prepare() o prepareAsync() para que el reproductor multimedia esté disponible.

Al crear el reproductor multimedia, se llama al método start (), mientras que el estado del reproductor multimedia no cambia (programador clic, s.f.).

De acuerdo con Programador clic (s.f.), MediaPlayer es usado para reproducir archivos de audio y video y establece la ruta del archivo con el método `setDataSource()`.El siguiente diagrama muestra los respectivos métodos que se pueden utilizar para usar audio o video.

### 🎭 Estados del MediaPlayerMediaRecorder state diagram

MediaPlayer opera con los siguientes estados: **inactivo**, **inicializado**, **preparado**, **inicio**, **pausa**, **parada**, **reproducción**, **completado**, **finalización**, **error**.Fuente: programador clic. (s.f.). Registros de aprendizaje de MediaPlayer para el aprendizaje de reproducción de audio y video de Android. Recuperado de https://programmerclick.com/article/76661765217/

Cuando se crea el mediaplayer con `new` o se llama al método `reset()`, el mediaplayer está en estado inactivo, debe llamar `prepare()` o `prepareAsync()` para que el reproductor multimedia esté disponible.Para probar el uso del audio, realizarás una aplicación que grabe audio, para ello, crea un nuevo proyecto con una empty activity, a la que puedes llamar “Grabadora”.

Al crear el reproductor multimedia, se llama al método `start()`, mientras que el estado del reproductor multimedia no cambia (programador clic, s.f.).En la parte de diseño vas a colocar un imageView y dos botones, el primero de ellos tendrá el id btn_rec y el segundo btn_play. El imageView permanece con mismo id.

El siguiente diagrama muestra los respectivos métodos que se pueden utilizar para usar audio o video.Para las imágenes que desees integrar a tu image view, es necesario tenerlas en un folder de tu computadora, de ahí das copy y las pegas directamente en el folder res/drawable, como lo puedes ver en la siguiente imagen.

**MediaRecorder state diagram**Ejemplo basado en La Geekipedia De Ernesto (2018).

*Fuente: programador clic. (s.f.). Registros de aprendizaje de MediaPlayer para el aprendizaje de reproducción de audio y video de Android. Recuperado de https://programmerclick.com/article/76661765217/*El código en activity_main.xml quedaría algo similar a lo siguiente:

### 🛠️ Clases Principales para AudioEsta pantalla se obtuvo directamente del software que se está explicando en la computadora para fines educativos.

Android cuenta con clases específicas para el manejo de audio:En caso de que desees cambiar los colores de fondo del diseño, debe hacerse en el menú values/styles.

-  **MediaPlayer**: Reproducción de audio/video desde archivos o streamsEsta pantalla se obtuvo directamente del software que se está explicando en la computadora para fines educativos.

-  **MediaRecorder**: Grabación de audio y video

-  **AudioManager**: Gestión de propiedades del sistema de audioY en la parte lógica de la actividad principal (MainActivity.java) se va a realizar el enlace de las variables de grabación y de la salida de audio que permita escuchar la grabación realizada. Dentro del método onCreate se verifica que el archivo manifest tenga los permisos necesarios, en caso contrario, no se ejecuta.

-  **SoundPool**: Manejo de efectos de sonido cortos

-  **AudioTrack**: Reproducción directa de audio PCMEl método recorder permite grabar un audio dentro de un directorio del dispositivo, el cual en el ejemplo es identificado como “Grabacion.mp3”.

-  **AudioRecord**: Grabación de audio en tiempo real

-  **AudioAttributes**: Configuración de atributos de audioPosteriormente, dentro del try {} se trabajan los métodos de la clase media recorder, el método prepare(), que se prepara para la grabación y luego se trabaja con el método stop() para parar la grabación y se pasa a un estado de finalizado con release(). Finalmente, a través del método reproducir se puede escuchar el audio que se ha grabado por el usuario. Quedando el código en MainActivity.java de la siguiente manera:

-  **AudioFocusRequest**: Manejo del foco de audio

Esta pantalla se obtuvo directamente del software que se está explicando en la computadora para fines educativos.

---

Recuerda escribir los permisos dentro de manifest.

## 🎧 Explicación con Analogías: Android como un Estudio de Grabación

Finalmente, ejecuta tu aplicación y graba el audio que desees.

### **MediaPlayer: Tu Reproductor Profesional**

Imagina que el `MediaPlayer` es como un **reproductor de música profesional** 🎵. Así como un DJ tiene un reproductor que puede cargar canciones, pausarlas, adelantarlas y controlar el volumen, el MediaPlayer hace exactamente lo mismo pero en tu aplicación.

### **MediaRecorder: Tu Micrófono de Estudio**

El `MediaRecorder` es como tener un **micrófono de estudio profesional** 🎤. Cuando quieres grabar algo, presionas "REC", hablas, y luego presionas "STOP" para terminar la grabación. ¡Exactamente como funciona MediaRecorder!

### **🎪 Estados del MediaPlayer: Como los Modos de un Estéreo**

Cada estado es como los diferentes modos de un equipo de sonido:

#### 🔴 **Inactivo**: El Estéreo Apagado

-  Como cuando tu estéreo está apagado o en standby
-  No está listo para reproducir nada

#### ⚙️ **Inicializado**: Estéreo Encendido pero sin CD

-  Como cuando enciendes el estéreo pero no has puesto música
-  Ya está listo pero necesita contenido

#### 🎯 **Preparado**: CD Cargado y Listo

-  Como cuando ya pusiste el CD y está listo para tocar
-  Todo configurado, solo falta presionar play

#### ▶️ **Reproduciendo**: Música Sonando

-  Como cuando está tocando tu canción favorita
-  El audio se está reproduciendo activamente

#### ⏸️ **Pausado**: Música Detenida Temporalmente

-  Como cuando pausas la canción para contestar el teléfono
-  Puedes reanudar desde donde lo dejaste

#### ⏹️ **Detenido**: Música Parada Completamente

-  Como cuando presionas stop y regresa al inicio
-  Para volver a reproducir, necesitas preparar de nuevo

### **🎪 Las Clases de Audio: El Equipo de tu Estudio**

Cada clase es como un miembro especializado de tu estudio de grabación:

#### 🎵 **MediaPlayer**: El Reproductor Principal

-  Como el equipo de sonido principal del estudio
-  Reproduce música, podcasts, cualquier audio largo

#### 🎤 **MediaRecorder**: El Ingeniero de Grabación

-  Como el técnico que maneja la grabación
-  Configura micrófonos, niveles, y graba todo

#### 🔊 **AudioManager**: El Maestro de Sonido

-  Como el ingeniero de audio que controla todo el sistema
-  Maneja volúmenes, ruteo de audio, y configuraciones globales

#### 🎮 **SoundPool**: El Banco de Efectos

-  Como la mesa de efectos especiales
-  Perfecto para sonidos cortos: clicks, explosiones, notificaciones

#### 🎼 **AudioTrack**: El Canal Directo

-  Como conectar directamente a los altavoces profesionales
-  Para audio que necesita control muy preciso

#### 📻 **AudioRecord**: El Micrófono en Vivo

-  Como el micrófono que capta audio en tiempo real
-  Para aplicaciones que necesitan procesar audio mientras se graba

#### 🎛️ **AudioAttributes**: El Configurador de Canal

-  Como el técnico que configura qué tipo de audio es (música, llamada, alarma)
-  Define cómo el sistema debe tratar tu audio

#### 🎯 **AudioFocusRequest**: El Director de Tráfico de Audio

-  Como el coordinador que decide qué audio tiene prioridad
-  Maneja interrupciones (llamadas, notificaciones, etc.)

---

## 🎯 **Conclusión: Tu Estudio de Grabación en Android**

Implementar audio en Android es como **montar tu propio estudio de grabación profesional**:

✅ **Tienes reproductores profesionales** (MediaPlayer, SoundPool)  
✅ **Tienes equipo de grabación** (MediaRecorder, AudioRecord)  
✅ **Tienes control total del sistema** (AudioManager, AudioAttributes)

### 🌟 **La Magia de Android**

Android te da un **estudio de grabación completo** en tu dispositivo. Desde reproducir una simple canción hasta crear una aplicación de podcast profesional, ¡tienes todas las herramientas!

> **💡 Recuerda**: Para reproducciones simples usa MediaPlayer, para efectos cortos usa SoundPool, y para grabación usa MediaRecorder. ¡Cada herramienta tiene su propósito! 📱✨

---

## 💻 **Ejemplo Práctico: Grabadora de Audio en Android (API 28 - Java)**

### 🛠️ **Paso 1: Layout XML (activity_main.xml)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    android:gravity="center">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="🎤 Mi Grabadora de Audio"
        android:textSize="28sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="32dp"
        android:textColor="#2E7D32" />

    <!-- Imagen del micrófono -->
    <ImageView
        android:id="@+id/imageViewMic"
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:layout_marginBottom="32dp"
        android:src="@drawable/ic_mic_inactive"
        android:background="@drawable/circle_background"
        android:padding="40dp"
        android:contentDescription="Micrófono" />

    <!-- Botones de control -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center"
        android:layout_marginBottom="16dp">

        <Button
            android:id="@+id/btn_rec"
            android:layout_width="0dp"
            android:layout_height="60dp"
            android:layout_weight="1"
            android:text="🔴 GRABAR"
            android:textSize="16sp"
            android:textStyle="bold"
            android:layout_margin="8dp"
            android:backgroundTint="#D32F2F"
            android:textColor="#FFFFFF" />

        <Button
            android:id="@+id/btn_stop"
            android:layout_width="0dp"
            android:layout_height="60dp"
            android:layout_weight="1"
            android:text="⏹️ PARAR"
            android:textSize="16sp"
            android:textStyle="bold"
            android:layout_margin="8dp"
            android:backgroundTint="#757575"
            android:textColor="#FFFFFF"
            android:enabled="false" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center"
        android:layout_marginBottom="24dp">

        <Button
            android:id="@+id/btn_play"
            android:layout_width="0dp"
            android:layout_height="60dp"
            android:layout_weight="1"
            android:text="▶️ REPRODUCIR"
            android:textSize="16sp"
            android:textStyle="bold"
            android:layout_margin="8dp"
            android:backgroundTint="#388E3C"
            android:textColor="#FFFFFF"
            android:enabled="false" />

        <Button
            android:id="@+id/btn_pause"
            android:layout_width="0dp"
            android:layout_height="60dp"
            android:layout_weight="1"
            android:text="⏸️ PAUSAR"
            android:textSize="16sp"
            android:textStyle="bold"
            android:layout_margin="8dp"
            android:backgroundTint="#F57C00"
            android:textColor="#FFFFFF"
            android:enabled="false" />

    </LinearLayout>

    <!-- Información del estado -->
    <TextView
        android:id="@+id/txtStatus"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="🎤 Listo para grabar audio"
        android:textSize="16sp"
        android:gravity="center"
        android:background="#E8F5E8"
        android:padding="16dp"
        android:layout_marginBottom="16dp"
        android:textColor="#2E7D32" />

    <!-- Información de la grabación -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:background="#F5F5F5"
        android:padding="16dp">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="📁 Información de Grabación"
            android:textSize="14sp"
            android:textStyle="bold"
            android:layout_marginBottom="8dp"
            android:textColor="#424242" />

        <TextView
            android:id="@+id/txtFileName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Archivo: No hay grabación"
            android:textSize="12sp"
            android:layout_marginBottom="4dp"
            android:textColor="#666666" />

        <TextView
            android:id="@+id/txtDuration"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Duración: --:--"
            android:textSize="12sp"
            android:layout_marginBottom="4dp"
            android:textColor="#666666" />

        <TextView
            android:id="@+id/txtFileSize"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tamaño: -- KB"
            android:textSize="12sp"
            android:textColor="#666666" />

    </LinearLayout>

</LinearLayout>
```

### 🎯 **Paso 2: Código Java (MainActivity.java)**

```java
package com.ejemplo.grabadora;

import android.Manifest;
import android.app.Activity;
import android.content.pm.PackageManager;
import android.media.MediaPlayer;
import android.media.MediaRecorder;
import android.os.Bundle;
import android.os.Environment;
import android.os.Handler;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class MainActivity extends Activity {

    // 🎤 Códigos de permisos
    private static final int REQUEST_AUDIO_PERMISSION = 200;

    // 🎬 Componentes de la UI
    private Button btnRecord, btnStop, btnPlay, btnPause;
    private ImageView imageViewMic;
    private TextView txtStatus, txtFileName, txtDuration, txtFileSize;

    // 🎵 Variables para manejo de audio
    private MediaRecorder mediaRecorder;
    private MediaPlayer mediaPlayer;
    private String audioFilePath;
    private boolean isRecording = false;
    private boolean isPlaying = false;
    private boolean isPaused = false;

    // ⏱️ Variables para cronómetro
    private Handler handler = new Handler();
    private long recordStartTime = 0;
    private Runnable recordingTimeRunnable;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 🎯 Inicializar nuestro "estudio de grabación"
        initializeComponents();
        setupButtonListeners();
        checkPermissions();
    }

    /**
     * 🎯 Inicializar los componentes de la UI
     */
    private void initializeComponents() {
        btnRecord = findViewById(R.id.btn_rec);
        btnStop = findViewById(R.id.btn_stop);
        btnPlay = findViewById(R.id.btn_play);
        btnPause = findViewById(R.id.btn_pause);
        imageViewMic = findViewById(R.id.imageViewMic);
        txtStatus = findViewById(R.id.txtStatus);
        txtFileName = findViewById(R.id.txtFileName);
        txtDuration = findViewById(R.id.txtDuration);
        txtFileSize = findViewById(R.id.txtFileSize);

        updateStatus("🎤 Estudio de grabación inicializado");
    }

    /**
     * 🎮 Configurar los listeners de los botones
     */
    private void setupButtonListeners() {

        // 🔴 Botón para grabar
        btnRecord.setOnClickListener(view -> {
            if (checkAudioPermission()) {
                startRecording();
            } else {
                requestPermissions();
            }
        });

        // ⏹️ Botón para parar
        btnStop.setOnClickListener(view -> {
            if (isRecording) {
                stopRecording();
            } else if (isPlaying) {
                stopPlayback();
            }
        });

        // ▶️ Botón para reproducir
        btnPlay.setOnClickListener(view -> {
            if (isPaused) {
                resumePlayback();
            } else {
                startPlayback();
            }
        });

        // ⏸️ Botón para pausar
        btnPause.setOnClickListener(view -> pausePlayback());
    }

    /**
     * 🔒 Verificar permisos de audio
     */
    private boolean checkAudioPermission() {
        return ContextCompat.checkSelfPermission(this, Manifest.permission.RECORD_AUDIO)
                == PackageManager.PERMISSION_GRANTED;
    }

    /**
     * 🔒 Verificar y solicitar permisos
     */
    private void checkPermissions() {
        if (!checkAudioPermission()) {
            updateStatus("⚠️ Se necesitan permisos para grabar audio");
        } else {
            updateStatus("✅ Listo para grabar audio");
        }
    }

    /**
     * 📝 Solicitar permisos necesarios
     */
    private void requestPermissions() {
        ActivityCompat.requestPermissions(this,
            new String[]{Manifest.permission.RECORD_AUDIO},
            REQUEST_AUDIO_PERMISSION);
    }

    /**
     * 🔴 Iniciar grabación
     */
    private void startRecording() {
        try {
            // Crear nombre único para el archivo
            String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss", Locale.getDefault()).format(new Date());
            String fileName = "Grabacion_" + timeStamp + ".mp3";

            // Crear ruta del archivo
            File audioDir = new File(getExternalFilesDir(Environment.DIRECTORY_MUSIC), "MisGrabaciones");
            if (!audioDir.exists()) {
                audioDir.mkdirs();
            }
            audioFilePath = new File(audioDir, fileName).getAbsolutePath();

            // Configurar MediaRecorder
            mediaRecorder = new MediaRecorder();
            mediaRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);
            mediaRecorder.setOutputFormat(MediaRecorder.OutputFormat.MPEG_4);
            mediaRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AAC);
            mediaRecorder.setOutputFile(audioFilePath);

            // Preparar y iniciar grabación
            mediaRecorder.prepare();
            mediaRecorder.start();

            // Actualizar estado
            isRecording = true;
            recordStartTime = System.currentTimeMillis();
            updateUIForRecording();
            startRecordingTimer();

            updateStatus("🔴 Grabando audio...");
            updateFileName(fileName);
            Toast.makeText(this, "🔴 Grabación iniciada", Toast.LENGTH_SHORT).show();

        } catch (IOException e) {
            updateStatus("❌ Error al iniciar grabación: " + e.getMessage());
            Toast.makeText(this, "Error al iniciar grabación", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * ⏹️ Parar grabación
     */
    private void stopRecording() {
        try {
            if (mediaRecorder != null && isRecording) {
                mediaRecorder.stop();
                mediaRecorder.release();
                mediaRecorder = null;

                isRecording = false;
                stopRecordingTimer();
                updateUIForStopped();

                // Calcular información del archivo
                File audioFile = new File(audioFilePath);
                long fileSizeKB = audioFile.length() / 1024;
                long durationMs = System.currentTimeMillis() - recordStartTime;

                updateFileInfo(fileSizeKB, durationMs);
                updateStatus("✅ Grabación completada");
                Toast.makeText(this, "✅ Grabación guardada", Toast.LENGTH_SHORT).show();
            }
        } catch (RuntimeException e) {
            updateStatus("❌ Error al parar grabación: " + e.getMessage());
        }
    }

    /**
     * ▶️ Iniciar reproducción
     */
    private void startPlayback() {
        if (audioFilePath == null || !new File(audioFilePath).exists()) {
            Toast.makeText(this, "No hay grabación para reproducir", Toast.LENGTH_SHORT).show();
            return;
        }

        try {
            mediaPlayer = new MediaPlayer();
            mediaPlayer.setDataSource(audioFilePath);
            mediaPlayer.prepare();
            mediaPlayer.start();

            isPlaying = true;
            isPaused = false;
            updateUIForPlaying();

            // Listener para cuando termine la reproducción
            mediaPlayer.setOnCompletionListener(mp -> {
                stopPlayback();
                Toast.makeText(MainActivity.this, "🎵 Reproducción completada", Toast.LENGTH_SHORT).show();
            });

            updateStatus("▶️ Reproduciendo grabación...");
            Toast.makeText(this, "▶️ Reproduciendo", Toast.LENGTH_SHORT).show();

        } catch (IOException e) {
            updateStatus("❌ Error al reproducir: " + e.getMessage());
            Toast.makeText(this, "Error al reproducir audio", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * ⏸️ Pausar reproducción
     */
    private void pausePlayback() {
        if (mediaPlayer != null && isPlaying) {
            mediaPlayer.pause();
            isPaused = true;
            updateUIForPaused();
            updateStatus("⏸️ Reproducción pausada");
            Toast.makeText(this, "⏸️ Pausado", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * ▶️ Reanudar reproducción
     */
    private void resumePlayback() {
        if (mediaPlayer != null && isPaused) {
            mediaPlayer.start();
            isPaused = false;
            updateUIForPlaying();
            updateStatus("▶️ Reproducción reanudada");
            Toast.makeText(this, "▶️ Reanudando", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * ⏹️ Parar reproducción
     */
    private void stopPlayback() {
        if (mediaPlayer != null) {
            if (isPlaying) {
                mediaPlayer.stop();
            }
            mediaPlayer.release();
            mediaPlayer = null;

            isPlaying = false;
            isPaused = false;
            updateUIForStopped();
            updateStatus("⏹️ Reproducción detenida");
        }
    }

    /**
     * ⏱️ Iniciar cronómetro de grabación
     */
    private void startRecordingTimer() {
        recordingTimeRunnable = new Runnable() {
            @Override
            public void run() {
                if (isRecording) {
                    long elapsed = System.currentTimeMillis() - recordStartTime;
                    updateDuration(elapsed);
                    handler.postDelayed(this, 1000);
                }
            }
        };
        handler.post(recordingTimeRunnable);
    }

    /**
     * ⏱️ Parar cronómetro de grabación
     */
    private void stopRecordingTimer() {
        if (recordingTimeRunnable != null) {
            handler.removeCallbacks(recordingTimeRunnable);
        }
    }

    /**
     * 🎨 Actualizar UI para grabación
     */
    private void updateUIForRecording() {
        btnRecord.setEnabled(false);
        btnStop.setEnabled(true);
        btnPlay.setEnabled(false);
        btnPause.setEnabled(false);
    }

    /**
     * 🎨 Actualizar UI para reproducción
     */
    private void updateUIForPlaying() {
        btnRecord.setEnabled(false);
        btnStop.setEnabled(true);
        btnPlay.setEnabled(false);
        btnPause.setEnabled(true);
    }

    /**
     * 🎨 Actualizar UI para pausado
     */
    private void updateUIForPaused() {
        btnRecord.setEnabled(false);
        btnStop.setEnabled(true);
        btnPlay.setEnabled(true);
        btnPause.setEnabled(false);
    }

    /**
     * 🎨 Actualizar UI para detenido
     */
    private void updateUIForStopped() {
        btnRecord.setEnabled(true);
        btnStop.setEnabled(false);
        btnPlay.setEnabled(audioFilePath != null && new File(audioFilePath).exists());
        btnPause.setEnabled(false);
    }

    /**
     * 📝 Actualizar estado
     */
    private void updateStatus(String status) {
        txtStatus.setText(status);
    }

    /**
     * 📁 Actualizar nombre del archivo
     */
    private void updateFileName(String fileName) {
        txtFileName.setText("Archivo: " + fileName);
    }

    /**
     * ⏱️ Actualizar duración
     */
    private void updateDuration(long durationMs) {
        long seconds = (durationMs / 1000) % 60;
        long minutes = (durationMs / (1000 * 60)) % 60;
        String timeString = String.format(Locale.getDefault(), "%02d:%02d", minutes, seconds);
        txtDuration.setText("Duración: " + timeString);
    }

    /**
     * 📊 Actualizar información del archivo
     */
    private void updateFileInfo(long fileSizeKB, long durationMs) {
        updateDuration(durationMs);
        txtFileSize.setText("Tamaño: " + fileSizeKB + " KB");
    }

    /**
     * 🔒 Manejar respuesta de permisos
     */
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                         @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == REQUEST_AUDIO_PERMISSION) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                updateStatus("✅ Permisos concedidos - Listo para grabar");
                Toast.makeText(this, "✅ Permisos concedidos", Toast.LENGTH_SHORT).show();
            } else {
                updateStatus("❌ Se necesitan permisos para funcionar");
                Toast.makeText(this, "❌ Se necesitan permisos de audio", Toast.LENGTH_LONG).show();
            }
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();

        // Liberar recursos
        if (mediaRecorder != null) {
            try {
                mediaRecorder.release();
            } catch (Exception e) {
                // Ignorar errores al liberar recursos
            }
        }

        if (mediaPlayer != null) {
            try {
                mediaPlayer.release();
            } catch (Exception e) {
                // Ignorar errores al liberar recursos
            }
        }

        stopRecordingTimer();
    }
}
```

### 📋 **Paso 3: Permisos en AndroidManifest.xml**

```xml
<!-- Permisos necesarios para audio -->
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

<!-- Declarar que la app usa micrófono (opcional pero recomendado) -->
<uses-feature
    android:name="android.hardware.microphone"
    android:required="true" />

<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/AppTheme">

    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

</application>
```

### 🎨 **Paso 4: Recursos Adicionales**

#### **res/drawable/circle_background.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#E8F5E8" />
    <stroke android:width="2dp" android:color="#4CAF50" />
</shape>
```

#### **res/drawable/ic_mic_inactive.xml**

```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp"
    android:height="24dp"
    android:viewportWidth="24"
    android:viewportHeight="24">
    <path
        android:fillColor="#666666"
        android:pathData="M12,2A3,3 0 0,1 15,5V11A3,3 0 0,1 12,14A3,3 0 0,1 9,11V5A3,3 0 0,1 12,2M19,11C19,14.53 16.39,17.44 13,17.93V21H11V17.93C7.61,17.44 5,14.53 5,11H7A5,5 0 0,0 12,16A5,5 0 0,0 17,11H19Z"/>
</vector>
```

### 🌟 **Características del Ejemplo:**

✅ **Compatible con API 28** (Android 9.0+)  
✅ **Grabación de audio** con MediaRecorder  
✅ **Reproducción de audio** con MediaPlayer  
✅ **Controles completos** (grabar, parar, reproducir, pausar)  
✅ **Manejo de permisos** en tiempo de ejecución  
✅ **Cronómetro de grabación** en tiempo real  
✅ **Información del archivo** (tamaño, duración)  
✅ **UI intuitiva** con estados visuales claros  
✅ **Gestión de recursos** para evitar memory leaks

### 💡 **Tips Importantes:**

🔹 **Permisos**: Solicitar permisos de audio para grabación  
🔹 **Formatos**: AAC es recomendado para audio de calidad  
🔹 **Gestión de recursos**: Liberar MediaRecorder y MediaPlayer  
🔹 **Estados**: Manejar correctamente los estados de grabación/reproducción  
🔹 **Archivos**: Guardar en directorios apropiados del dispositivo

### 🚀 **Posibles Mejoras:**

🔸 **Visualizador de ondas** durante la grabación  
🔸 **Edición básica** de audio (cortar, unir)  
🔸 **Efectos de audio** (eco, reverb)  
🔸 **Compartir grabaciones** por email/redes sociales  
🔸 **Lista de grabaciones** anteriores

---

### 📚 **Referencias**

-  Programador clic. (s.f.). _Registros de aprendizaje de MediaPlayer para el aprendizaje de reproducción de audio y video de Android_
-  La Geekipedia De Ernesto (2018). _Ejemplo original de grabadora_
-  Android Developers. (2021). _MediaPlayer and MediaRecorder Documentation_
