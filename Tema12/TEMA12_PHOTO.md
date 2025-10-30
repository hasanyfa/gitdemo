# 📸 Tema 12: Captura de Fotografías en Android

## 12.2 Tomando Fotografías

### 📋 Introducción Técnica

La captura de fotografías es una de las funcionalidades más populares en las aplicaciones móviles modernas. Android proporciona múltiples formas de integrar la funcionalidad de cámara en las aplicaciones, desde soluciones simples usando intents hasta implementaciones más complejas con control directo de la cámara.

El SDK de Android incluye varias clases que facilitan la implementación de captura de fotos en dispositivos Android. La forma más sencilla es utilizar un `Intent` para delegar la captura a la aplicación de cámara del sistema, mientras que para mayor control se puede usar la clase `Camera2` API.

### 📂 Métodos de Captura de Fotografías

Es posible capturar fotografías de diferentes maneras:

-  **Usando Intent (Camera App)** - Delega la captura a la aplicación de cámara del sistema
-  **Camera2 API** - Control directo de la cámara con configuraciones avanzadas
-  **CameraX** - API moderna y simplificada (recomendada para nuevos proyectos)
-  **Desde galería** - Seleccionar fotos existentes del dispositivo

### 🛠️ Clases Principales para Fotografía

Android cuenta con clases específicas para el manejo de fotografías:

-  **Camera2**: API moderna para control directo de la cámara
-  **CameraManager**: Gestiona el acceso a las cámaras del dispositivo
-  **CaptureRequest**: Define los parámetros de captura
-  **ImageReader**: Captura imágenes en formato específico
-  **SurfaceView**: Muestra la vista previa de la cámara
-  **TextureView**: Vista previa con transformaciones
-  **Intent (MediaStore)**: Integración simple con la app de cámara del sistema
-  **BitmapFactory**: Procesa y manipula las imágenes capturadas

> **💡 Tip**: Para implementaciones simples, usar `Intent` con `MediaStore.ACTION_IMAGE_CAPTURE` es la opción más fácil.

---

## 📷 Explicación con Analogías: Android como un Estudio Fotográfico

### **Intent Camera: Tu Fotógrafo Profesional Externo**

Imagina que tienes un **fotógrafo profesional de confianza** 📸. Cuando necesitas una foto, simplemente le dices "tómame una foto" y él se encarga de todo: configurar la cámara, elegir la iluminación, tomar la foto y entregártela lista. Esto es exactamente lo que hace el `Intent` con `MediaStore.ACTION_IMAGE_CAPTURE` - delega todo el trabajo a la aplicación de cámara del sistema.

### **📱 Métodos de Captura: Diferentes Tipos de Fotógrafos**

#### 1. 🤝 **Intent (Camera App)**

**= Como contratar un fotógrafo profesional externo**

-  Le das el trabajo a un experto (la app de cámara del sistema)
-  Tú solo recibes el resultado final
-  Fácil pero con menos control sobre el proceso

#### 2. 🎯 **Camera2 API**

**= Como ser tu propio fotógrafo profesional**

-  Tienes control total sobre la cámara
-  Configuras manualmente ISO, exposición, enfoque, etc.
-  Más complejo pero máximo control

#### 3. 🆕 **CameraX**

**= Como tener un asistente fotográfico inteligente**

-  Combina facilidad de uso con control avanzado
-  Se adapta automáticamente a diferentes dispositivos
-  Recomendado para proyectos nuevos

#### 4. 🖼️ **Desde Galería**

**= Como elegir una foto de tu álbum familiar**

-  Seleccionas fotos que ya existen
-  No capturas nuevas, solo eliges las que ya tienes

### **🎪 Las Clases de Fotografía: El Equipo de tu Estudio**

Cada clase es como un miembro especializado de tu estudio fotográfico:

#### 📷 **Camera2**: El Fotógrafo Principal

-  Como el fotógrafo experto que maneja la cámara profesional
-  Controla todos los aspectos técnicos de la captura

#### 🎬 **CameraManager**: El Director del Estudio

-  Como el gerente que decide qué cámara usar (frontal o trasera)
-  Gestiona el acceso y disponibilidad de las cámaras

#### ⚙️ **CaptureRequest**: El Asistente de Configuración

-  Como el técnico que ajusta ISO, velocidad, enfoque
-  Define cómo debe tomarse cada foto específica

#### 📥 **ImageReader**: El Revelador Digital

-  Como el técnico de laboratorio que procesa las fotos
-  Convierte la captura en archivos de imagen utilizables

#### 🖥️ **SurfaceView**: El Visor de la Cámara

-  Como el visor LCD de una cámara profesional
-  Muestra lo que va a capturar en tiempo real

#### 🎨 **TextureView**: El Monitor Profesional con Efectos

-  Como un monitor profesional que puede aplicar filtros en tiempo real
-  Vista previa con capacidad de transformaciones visuales

#### 📞 **Intent (MediaStore)**: El Intermediario

-  Como el asistente que llama al fotógrafo externo
-  Conecta tu app con la aplicación de cámara del sistema

#### 🖼️ **BitmapFactory**: El Editor de Fotos

-  Como el especialista en Photoshop del equipo
-  Procesa, redimensiona y optimiza las imágenes capturadas

---

## 🎯 **Conclusión: Tu Estudio Fotográfico en Android**

Implementar fotografía en Android es como **montar tu propio estudio fotográfico**:

✅ **Tienes diferentes tipos de fotógrafos** (métodos de captura)  
✅ **Tienes equipo profesional completo** (las clases especializadas)  
✅ **Puedes elegir el nivel de control** (desde simple hasta profesional)

### 🌟 **La Magia de Android**

Android te permite elegir entre la **simplicidad de contratar un fotógrafo externo** (Intent) o **montar tu propio estudio profesional** (Camera2/CameraX). ¡Tú decides qué tan profesional quieres que sea tu app!

> **💡 Recuerda**: Para la mayoría de casos, usar `Intent` es perfecto. Solo necesitas Camera2 cuando requieras control muy específico sobre la captura. 📱✨

---

## 💻 **Ejemplo Práctico: Capturando Fotos en Android (API 28 - Java)**

### 🛠️ **Paso 1: Layout XML (activity_camera.xml)**

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
        android:text="📸 Mi Cámara App"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="16dp" />

    <!-- ImageView para mostrar la foto capturada -->
    <ImageView
        android:id="@+id/imageViewPhoto"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:layout_marginBottom="16dp"
        android:background="#f0f0f0"
        android:scaleType="centerCrop"
        android:src="@drawable/ic_photo_placeholder"
        android:contentDescription="Foto capturada" />

    <!-- Botones de acción -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">

        <Button
            android:id="@+id/btnTakePhoto"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="📷 Tomar Foto"
            android:layout_margin="4dp"
            android:backgroundTint="#4CAF50" />

        <Button
            android:id="@+id/btnSelectPhoto"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="🖼️ Galería"
            android:layout_margin="4dp"
            android:backgroundTint="#2196F3" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center"
        android:layout_marginTop="8dp">

        <Button
            android:id="@+id/btnSavePhoto"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="💾 Guardar"
            android:layout_margin="4dp"
            android:backgroundTint="#FF9800"
            android:enabled="false" />

        <Button
            android:id="@+id/btnClearPhoto"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="🗑️ Limpiar"
            android:layout_margin="4dp"
            android:backgroundTint="#F44336"
            android:enabled="false" />

    </LinearLayout>

    <!-- Estado de la aplicación -->
    <TextView
        android:id="@+id/txtStatus"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Estado: Listo para capturar 📸"
        android:textSize="14sp"
        android:layout_marginTop="16dp"
        android:gravity="center"
        android:background="#e8f5e8"
        android:padding="8dp" />

</LinearLayout>
```

### 🎯 **Paso 2: Código Java (CameraActivity.java)**

```java
package com.ejemplo.cameraapp;

import android.Manifest;
import android.app.Activity;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.net.Uri;
import android.os.Bundle;
import android.os.Environment;
import android.provider.MediaStore;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import androidx.core.content.FileProvider;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class CameraActivity extends Activity {

    // 📱 Códigos de request para los diferentes intents
    private static final int REQUEST_CAMERA_PERMISSION = 100;
    private static final int REQUEST_STORAGE_PERMISSION = 101;
    private static final int REQUEST_IMAGE_CAPTURE = 200;
    private static final int REQUEST_GALLERY_PICK = 300;

    // 🎬 Componentes de nuestra "cámara app"
    private ImageView imageViewPhoto;
    private Button btnTakePhoto, btnSelectPhoto, btnSavePhoto, btnClearPhoto;
    private TextView txtStatus;

    // 📸 Variables para manejo de la foto
    private Bitmap currentPhotoBitmap;
    private String currentPhotoPath;
    private File photoFile;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_camera);

        // 🎯 Inicializar nuestro "estudio fotográfico"
        initializeComponents();
        setupButtonListeners();
        checkPermissions();
    }

    /**
     * 🎯 Inicializar los componentes de la UI
     */
    private void initializeComponents() {
        imageViewPhoto = findViewById(R.id.imageViewPhoto);
        btnTakePhoto = findViewById(R.id.btnTakePhoto);
        btnSelectPhoto = findViewById(R.id.btnSelectPhoto);
        btnSavePhoto = findViewById(R.id.btnSavePhoto);
        btnClearPhoto = findViewById(R.id.btnClearPhoto);
        txtStatus = findViewById(R.id.txtStatus);

        updateStatus("Componentes inicializados ✅");
    }

    /**
     * 🎮 Configurar los listeners de los botones
     */
    private void setupButtonListeners() {

        // 📷 Botón para tomar foto
        btnTakePhoto.setOnClickListener(view -> {
            if (checkCameraPermission()) {
                dispatchTakePictureIntent();
            } else {
                requestCameraPermission();
            }
        });

        // 🖼️ Botón para seleccionar de galería
        btnSelectPhoto.setOnClickListener(view -> {
            if (checkStoragePermission()) {
                dispatchGalleryIntent();
            } else {
                requestStoragePermission();
            }
        });

        // 💾 Botón para guardar foto
        btnSavePhoto.setOnClickListener(view -> savePhotoToGallery());

        // 🗑️ Botón para limpiar
        btnClearPhoto.setOnClickListener(view -> clearPhoto());
    }

    /**
     * 🔒 Verificar y solicitar permisos necesarios
     */
    private void checkPermissions() {
        if (!checkCameraPermission() || !checkStoragePermission()) {
            updateStatus("⚠️ Permisos requeridos para funcionar correctamente");
        } else {
            updateStatus("✅ Listo para capturar fotos");
        }
    }

    /**
     * 📷 Verificar permiso de cámara
     */
    private boolean checkCameraPermission() {
        return ContextCompat.checkSelfPermission(this, Manifest.permission.CAMERA)
                == PackageManager.PERMISSION_GRANTED;
    }

    /**
     * 💾 Verificar permiso de almacenamiento
     */
    private boolean checkStoragePermission() {
        return ContextCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)
                == PackageManager.PERMISSION_GRANTED;
    }

    /**
     * 📷 Solicitar permiso de cámara
     */
    private void requestCameraPermission() {
        ActivityCompat.requestPermissions(this,
            new String[]{Manifest.permission.CAMERA},
            REQUEST_CAMERA_PERMISSION);
    }

    /**
     * 💾 Solicitar permiso de almacenamiento
     */
    private void requestStoragePermission() {
        ActivityCompat.requestPermissions(this,
            new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
            REQUEST_STORAGE_PERMISSION);
    }

    /**
     * 📸 Lanzar la cámara para capturar foto
     */
    private void dispatchTakePictureIntent() {
        Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);

        // Verificar que hay una app de cámara disponible
        if (takePictureIntent.resolveActivity(getPackageManager()) != null) {

            // Crear archivo para guardar la foto
            photoFile = null;
            try {
                photoFile = createImageFile();
            } catch (IOException ex) {
                updateStatus("❌ Error al crear archivo de imagen");
                return;
            }

            // Si el archivo se creó correctamente
            if (photoFile != null) {
                Uri photoURI = FileProvider.getUriForFile(this,
                    "com.ejemplo.cameraapp.fileprovider",
                    photoFile);
                takePictureIntent.putExtra(MediaStore.EXTRA_OUTPUT, photoURI);
                startActivityForResult(takePictureIntent, REQUEST_IMAGE_CAPTURE);
                updateStatus("📷 Abriendo cámara...");
            }
        } else {
            Toast.makeText(this, "No hay aplicación de cámara disponible", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * 🖼️ Abrir galería para seleccionar foto
     */
    private void dispatchGalleryIntent() {
        Intent intent = new Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
        intent.setType("image/*");

        if (intent.resolveActivity(getPackageManager()) != null) {
            startActivityForResult(intent, REQUEST_GALLERY_PICK);
            updateStatus("🖼️ Abriendo galería...");
        } else {
            Toast.makeText(this, "No hay aplicación de galería disponible", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * 📁 Crear archivo para guardar la imagen
     */
    private File createImageFile() throws IOException {
        // Crear nombre único para la imagen
        String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss", Locale.getDefault()).format(new Date());
        String imageFileName = "JPEG_" + timeStamp + "_";

        File storageDir = getExternalFilesDir(Environment.DIRECTORY_PICTURES);
        File image = File.createTempFile(imageFileName, ".jpg", storageDir);

        // Guardar la ruta para uso posterior
        currentPhotoPath = image.getAbsolutePath();
        return image;
    }

    /**
     * 📱 Manejar resultados de los intents
     */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (resultCode == RESULT_OK) {
            switch (requestCode) {
                case REQUEST_IMAGE_CAPTURE:
                    handleCameraResult();
                    break;

                case REQUEST_GALLERY_PICK:
                    handleGalleryResult(data);
                    break;
            }
        } else {
            updateStatus("⚠️ Operación cancelada");
        }
    }

    /**
     * 📷 Procesar resultado de la cámara
     */
    private void handleCameraResult() {
        try {
            // Cargar la imagen desde el archivo
            currentPhotoBitmap = BitmapFactory.decodeFile(currentPhotoPath);

            if (currentPhotoBitmap != null) {
                // Mostrar la imagen en el ImageView
                imageViewPhoto.setImageBitmap(currentPhotoBitmap);

                // Habilitar botones de acción
                enableActionButtons(true);

                updateStatus("📸 ¡Foto capturada exitosamente!");
                Toast.makeText(this, "📸 ¡Excelente foto!", Toast.LENGTH_SHORT).show();
            } else {
                updateStatus("❌ Error al cargar la imagen");
            }

        } catch (Exception e) {
            updateStatus("❌ Error al procesar la foto: " + e.getMessage());
        }
    }

    /**
     * 🖼️ Procesar resultado de la galería
     */
    private void handleGalleryResult(Intent data) {
        try {
            Uri selectedImageUri = data.getData();

            if (selectedImageUri != null) {
                // Cargar imagen desde la URI
                currentPhotoBitmap = MediaStore.Images.Media.getBitmap(
                    getContentResolver(), selectedImageUri);

                // Mostrar la imagen
                imageViewPhoto.setImageBitmap(currentPhotoBitmap);

                // Habilitar botones de acción
                enableActionButtons(true);

                updateStatus("🖼️ ¡Imagen seleccionada de la galería!");
                Toast.makeText(this, "🖼️ ¡Imagen cargada!", Toast.LENGTH_SHORT).show();
            }

        } catch (Exception e) {
            updateStatus("❌ Error al cargar imagen de galería: " + e.getMessage());
        }
    }

    /**
     * 💾 Guardar foto en la galería
     */
    private void savePhotoToGallery() {
        if (currentPhotoBitmap == null) {
            Toast.makeText(this, "No hay foto para guardar", Toast.LENGTH_SHORT).show();
            return;
        }

        try {
            // Crear nombre único para el archivo
            String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss", Locale.getDefault()).format(new Date());
            String fileName = "IMG_" + timeStamp + ".jpg";

            // Crear archivo en la galería
            File galleryDir = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES);
            File imageFile = new File(galleryDir, fileName);

            // Guardar el bitmap como archivo
            FileOutputStream out = new FileOutputStream(imageFile);
            currentPhotoBitmap.compress(Bitmap.CompressFormat.JPEG, 90, out);
            out.flush();
            out.close();

            // Notificar al sistema que se agregó una nueva imagen
            Intent mediaScanIntent = new Intent(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE);
            Uri contentUri = Uri.fromFile(imageFile);
            mediaScanIntent.setData(contentUri);
            sendBroadcast(mediaScanIntent);

            updateStatus("💾 ¡Foto guardada en la galería!");
            Toast.makeText(this, "💾 Foto guardada exitosamente", Toast.LENGTH_LONG).show();

        } catch (Exception e) {
            updateStatus("❌ Error al guardar: " + e.getMessage());
            Toast.makeText(this, "Error al guardar la foto", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * 🗑️ Limpiar la foto actual
     */
    private void clearPhoto() {
        currentPhotoBitmap = null;
        currentPhotoPath = null;
        imageViewPhoto.setImageResource(R.drawable.ic_photo_placeholder);
        enableActionButtons(false);
        updateStatus("🗑️ Foto eliminada - Listo para nueva captura");
        Toast.makeText(this, "🗑️ Limpiado", Toast.LENGTH_SHORT).show();
    }

    /**
     * 🎛️ Habilitar/deshabilitar botones de acción
     */
    private void enableActionButtons(boolean enabled) {
        btnSavePhoto.setEnabled(enabled);
        btnClearPhoto.setEnabled(enabled);
    }

    /**
     * 📝 Actualizar estado mostrado al usuario
     */
    private void updateStatus(String status) {
        txtStatus.setText("Estado: " + status);
    }

    /**
     * 🔒 Manejar respuestas de permisos
     */
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                         @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
            case REQUEST_CAMERA_PERMISSION:
                if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    updateStatus("📷 Permiso de cámara concedido");
                    Toast.makeText(this, "✅ Permiso de cámara concedido", Toast.LENGTH_SHORT).show();
                } else {
                    updateStatus("❌ Permiso de cámara denegado");
                    Toast.makeText(this, "❌ Se necesita permiso de cámara", Toast.LENGTH_LONG).show();
                }
                break;

            case REQUEST_STORAGE_PERMISSION:
                if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    updateStatus("💾 Permiso de almacenamiento concedido");
                    Toast.makeText(this, "✅ Permiso de almacenamiento concedido", Toast.LENGTH_SHORT).show();
                } else {
                    updateStatus("❌ Permiso de almacenamiento denegado");
                    Toast.makeText(this, "❌ Se necesita permiso de almacenamiento", Toast.LENGTH_LONG).show();
                }
                break;
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // Liberar memoria del bitmap
        if (currentPhotoBitmap != null && !currentPhotoBitmap.isRecycled()) {
            currentPhotoBitmap.recycle();
        }
    }
}
```

### 📋 **Paso 3: Permisos en AndroidManifest.xml**

```xml
<!-- Permisos necesarios -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

<!-- Declarar que la app usa cámara (opcional pero recomendado) -->
<uses-feature
    android:name="android.hardware.camera"
    android:required="true" />

<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/AppTheme">

    <activity android:name=".CameraActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

    <!-- FileProvider para Android 7.0+ -->
    <provider
        android:name="androidx.core.content.FileProvider"
        android:authorities="com.ejemplo.cameraapp.fileprovider"
        android:exported="false"
        android:grantUriPermissions="true">
        <meta-data
            android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/file_paths" />
    </provider>

</application>
```

### 📁 **Paso 4: Configuración FileProvider (res/xml/file_paths.xml)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <external-files-path
        name="my_images"
        path="Pictures" />
    <external-path
        name="external_files"
        path="." />
</paths>
```

### 🌟 **Características del Ejemplo:**

✅ **Compatible con API 28** (Android 9.0+)  
✅ **Manejo completo de permisos** en tiempo de ejecución  
✅ **Captura desde cámara** usando Intent  
✅ **Selección desde galería** con URI handling  
✅ **Guardado en galería** con nombres únicos  
✅ **FileProvider** para Android 7.0+ (Nougat)  
✅ **Gestión de memoria** para evitar OutOfMemoryError  
✅ **UI intuitiva** con estados claros  
✅ **Manejo de errores** robusto

### 💡 **Tips Importantes:**

🔹 **Permisos**: Solicitar permisos en tiempo de ejecución para API 23+  
🔹 **FileProvider**: Necesario para compartir archivos en Android 7.0+  
🔹 **Memoria**: Reciclar bitmaps para evitar memory leaks  
🔹 **Formatos**: JPG es el más compatible, PNG para transparencias  
🔹 **Resolución**: Considerar redimensionar fotos grandes para mejor rendimiento

### 🚀 **Posibles Mejoras:**

🔸 **Compresión automática** de imágenes grandes  
🔸 **Filtros y efectos** básicos  
🔸 **Metadatos EXIF** para información de la foto  
🔸 **Camera2 API** para control avanzado  
🔸 **CameraX** para implementación moderna

---

### 📚 **Referencias**

-  Android Developers. (2021). _Camera and Camera2 APIs_
-  Google. (2021). _CameraX Documentation_
-  Android Developers. (2021). _MediaStore and FileProvider_
-  Códigos de Programación – MR (2020). _Ejemplo original básico_
