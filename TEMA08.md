# TEMA 08. Uso de aplicaciones externas

## Explicación

En Android puedes utilizar **aplicaciones externas** desde tu app, siempre y cuando estén **instaladas** en el dispositivo del usuario. Esta capacidad aumenta el potencial de tus proyectos: por ejemplo, **hacer una llamada**, **abrir un mapa**, **tomar una fotografía** o **compartir contenido** sin implementar toda la funcionalidad tú mismo.

Una de las funciones clave de Android es permitir que una app **envíe al usuario a otra** según la _acción_ que desea realizar. Si tu app tiene una dirección y quieres mostrarla en un mapa, no necesitas construir una actividad propia para mapas: puedes crear una **solicitud** con un **`Intent`** y Android abrirá la app que pueda manejarla (p. ej., Google Maps).

---

## 8.1 Aplicaciones externas (Intents implícitos)

### ¿Qué es un `Intent`?

Un **`Intent`** es un mensaje que solicita una acción de otro componente de Android (actividad, servicio o receptor). Los **intents implícitos** especifican **qué** acción se desea (p. ej., “ver una ubicación”) sin indicar **qué** app exacta la realizará. Android resuelve la app adecuada si existe al menos una instalada.

### Casos frecuentes (Java)

> Asegúrate de probar en un dispositivo/emulador con apps instaladas que puedan manejar cada acción. Antes de lanzar, valida con `resolveActivity(...)`.

**Abrir el marcador de llamadas con un número**:

```java
Uri number = Uri.parse("tel:5551234567");
Intent intent = new Intent(Intent.ACTION_DIAL, number);
if (intent.resolveActivity(getPackageManager()) != null) {
    startActivity(intent);
}
```

**Abrir Google Maps en una dirección/consulta**:

```java
Uri geo = Uri.parse("geo:0,0?q=Av.+Insurgentes+Sur+3000+CDMX");
Intent mapIntent = new Intent(Intent.ACTION_VIEW, geo);
mapIntent.setPackage("com.google.android.apps.maps"); // opcional: forzar Maps
if (mapIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(mapIntent);
}
```

**Compartir texto (chooser)**:

```java
Intent sendIntent = new Intent(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, "Hola, esto es un mensaje compartido desde mi app.");
sendIntent.setType("text/plain");
Intent shareIntent = Intent.createChooser(sendIntent, "Compartir con...");
startActivity(shareIntent);
```

**Enviar correo (solo apps de email)**:

```java
Intent emailIntent = new Intent(Intent.ACTION_SENDTO);
emailIntent.setData(Uri.parse("mailto:"));
emailIntent.putExtra(Intent.EXTRA_EMAIL, new String[]{"soporte@empresa.com"});
emailIntent.putExtra(Intent.EXTRA_SUBJECT, "Soporte de mi App");
if (emailIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(emailIntent);
}
```

**Tomar fotografía (miniatura) con la cámara**

> Requiere una app de cámara. Usa Activity Result API para recibir el resultado.

```java
ActivityResultLauncher<Intent> takePictureLauncher =
    registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), result -> {
        if (result.getResultCode() == Activity.RESULT_OK && result.getData() != null) {
            Bundle extras = result.getData().getExtras();
            Bitmap imageBitmap = (Bitmap) extras.get("data"); // miniatura
            // TODO: mostrar en un ImageView
        }
    });

void openCamera() {
    Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
    if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
        takePictureLauncher.launch(takePictureIntent);
    }
}
```

> Para guardar una **foto a tamaño completo**, crea un archivo mediante `FileProvider`, pasa la `Uri` con `EXTRA_OUTPUT` y solicita permisos temporales. (Opcional avanzado).

---

## 8.2 Extracción de datos de aplicaciones externas

Los **Intents** (`android.content.Intent`) permiten que una actividad **inicie otra** y opcionalmente **reciba resultados**. El patrón moderno para resultados es la **Activity Result API** (AndroidX), que reemplaza al método clásico `startActivityForResult`.

**Ejemplo: seleccionar una imagen de la galería y obtener su URI**:

```java
ActivityResultLauncher<String> pickImageLauncher =
    registerForActivityResult(new ActivityResultContracts.GetContent(), uri -> {
        if (uri != null) {
            // uri apunta al contenido seleccionado (p.ej., imagen de la galería)
            // TODO: cargar la imagen en un ImageView
        }
    });

void pickImageFromGallery() {
    pickImageLauncher.launch("image/*");
}
```

**Ejemplo: iniciar una actividad externa y leer un dato sencillo (texto)**:

```java
ActivityResultLauncher<Intent> launcher =
    registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), result -> {
        if (result.getResultCode() == Activity.RESULT_OK && result.getData() != null) {
            Intent data = result.getData();
            String value = data.getStringExtra("result_key");
            // TODO: usar 'value'
        }
    });

void openExternalAndGetText() {
    Intent intent = new Intent("com.ejemplo.ACTION_PICK_TEXT"); // acción definida por otra app
    if (intent.resolveActivity(getPackageManager()) != null) {
        launcher.launch(intent);
    }
}
```

> **Nota**: Si consumes datos de otras apps a través de `Uri` (p. ej., galería), utiliza **ContentResolver** para leer el flujo de datos, y respeta permisos y políticas de almacenamiento (scoped storage).

---

## Checkpoint

Asegúrate de:

-  **Identificar** los **métodos** para **guardar datos** enviados/recibidos entre apps (p. ej., `EXTRA_*`, `Uri`, `ContentResolver`, `EXTRA_OUTPUT` con `FileProvider`).
-  **Identificar** los **métodos que inician** un intento (`startActivity(...)`, `registerForActivityResult(...).launch(...)`).
-  **Identificar** el **sistema de mensajería**: `Intent` (implícito/explicito) con acciones, datos (`Uri`), categorías y extras.

---

## Actividad guiada (paso a paso)

## 0) Requisitos del proyecto

-  **API mínima**: 21 (Android 5.0)
-  **Lenguaje**: Java
-  **AndroidX habilitado**
-  **Gradle (app)**: usa versiones actuales. Asegúrate de incluir (o tener transitivamente):
   ```gradle
   dependencies {
       implementation 'androidx.appcompat:appcompat:1.6.1'
       implementation 'com.google.android.material:material:1.11.0'
       implementation 'androidx.activity:activity:1.8.0' // Activity Result API (Java-compatible)
   }
   ```
   > Usa las **últimas** versiones disponibles en tu entorno.

---

## 1) Crea la UI base (`activity_main.xml`)

En `res/layout/activity_main.xml` agrega botones y un `ImageView` para las pruebas de resultados (cámara/galería).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:orientation="vertical"
        android:padding="16dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <Button
            android:id="@+id/btnDial"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Abrir Teléfono (DIAL)" />

        <Button
            android:id="@+id/btnMaps"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Abrir Mapa (geo)" />

        <Button
            android:id="@+id/btnShare"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Compartir texto" />

        <Button
            android:id="@+id/btnEmail"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Enviar correo (mailto:)" />

        <View
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="#DDDDDD"
            android:layout_marginTop="12dp"
            android:layout_marginBottom="12dp" />

        <Button
            android:id="@+id/btnCamera"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tomar Foto (miniatura)" />

        <Button
            android:id="@+id/btnGallery"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Abrir Galería (seleccionar imagen)" />

        <ImageView
            android:id="@+id/imgPreview"
            android:layout_width="match_parent"
            android:layout_height="200dp"
            android:layout_marginTop="12dp"
            android:adjustViewBounds="true"
            android:scaleType="centerCrop"
            android:src="@android:drawable/ic_menu_gallery"
            android:contentDescription="Vista previa" />
    </LinearLayout>
</ScrollView>
```

---

## 2) Implementa `MainActivity.java`

Registra _launchers_ de la **Activity Result API** y conecta cada botón.

```java
package com.example.tema08;

import android.app.Activity;
import android.content.Intent;
import android.graphics.Bitmap;
import android.net.Uri;
import android.os.Bundle;
import android.provider.MediaStore;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.Toast;

import androidx.activity.result.ActivityResultLauncher;
import androidx.activity.result.contract.ActivityResultContracts;
import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private ImageView imgPreview;

    // Launcher para cámara (miniatura)
    private ActivityResultLauncher<Intent> takePictureLauncher =
            registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), result -> {
                if (result.getResultCode() == Activity.RESULT_OK && result.getData() != null) {
                    Bundle extras = result.getData().getExtras();
                    if (extras != null) {
                        Bitmap imageBitmap = (Bitmap) extras.get("data");
                        if (imageBitmap != null) imgPreview.setImageBitmap(imageBitmap);
                    }
                } else {
                    Toast.makeText(this, "Fotografía cancelada", Toast.LENGTH_SHORT).show();
                }
            });

    // Launcher para galería (GetContent)
    private ActivityResultLauncher<String> pickImageLauncher =
            registerForActivityResult(new ActivityResultContracts.GetContent(), uri -> {
                if (uri != null) {
                    imgPreview.setImageURI(uri);
                } else {
                    Toast.makeText(this, "Selección cancelada", Toast.LENGTH_SHORT).show();
                }
            });

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imgPreview = findViewById(R.id.imgPreview);

        Button btnDial = findViewById(R.id.btnDial);
        Button btnMaps = findViewById(R.id.btnMaps);
        Button btnShare = findViewById(R.id.btnShare);
        Button btnEmail = findViewById(R.id.btnEmail);
        Button btnCamera = findViewById(R.id.btnCamera);
        Button btnGallery = findViewById(R.id.btnGallery);

        btnDial.setOnClickListener(v -> openDialer("5551234567"));
        btnMaps.setOnClickListener(v -> openMapQuery("Av. Insurgentes Sur 3000, CDMX"));
        btnShare.setOnClickListener(v -> shareText("Hola, compartido desde mi app."));
        btnEmail.setOnClickListener(v -> composeEmail(
                new String[]{"soporte@empresa.com"},
                "Soporte de mi App",
                "Describe tu problema aquí..."
        ));
        btnCamera.setOnClickListener(v -> takePicture());
        btnGallery.setOnClickListener(v -> pickFromGallery());
    }

    /* ----------  Acciones ---------- */

    private void openDialer(String number) {
        Uri uri = Uri.parse("tel:" + number);
        Intent intent = new Intent(Intent.ACTION_DIAL, uri);
        if (intent.resolveActivity(getPackageManager()) != null) {
            startActivity(intent);
        } else {
            showNoAppMsg();
        }
    }

    private void openMapQuery(String q) {
        Uri geo = Uri.parse("geo:0,0?q=" + Uri.encode(q));
        Intent mapIntent = new Intent(Intent.ACTION_VIEW, geo);
        // mapIntent.setPackage("com.google.android.apps.maps"); // opcional
        if (mapIntent.resolveActivity(getPackageManager()) != null) {
            startActivity(mapIntent);
        } else {
            showNoAppMsg();
        }
    }

    private void shareText(String text) {
        Intent sendIntent = new Intent(Intent.ACTION_SEND);
        sendIntent.putExtra(Intent.EXTRA_TEXT, text);
        sendIntent.setType("text/plain");
        Intent shareIntent = Intent.createChooser(sendIntent, "Compartir con...");
        startActivity(shareIntent);
    }

    private void composeEmail(String[] addresses, String subject, String body) {
        Intent emailIntent = new Intent(Intent.ACTION_SENDTO);
        emailIntent.setData(Uri.parse("mailto:"));
        emailIntent.putExtra(Intent.EXTRA_EMAIL, addresses);
        emailIntent.putExtra(Intent.EXTRA_SUBJECT, subject);
        emailIntent.putExtra(Intent.EXTRA_TEXT, body);
        if (emailIntent.resolveActivity(getPackageManager()) != null) {
            startActivity(emailIntent);
        } else {
            showNoAppMsg();
        }
    }

    private void takePicture() {
        Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
        if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
            takePictureLauncher.launch(takePictureIntent);
        } else {
            showNoAppMsg();
        }
    }

    private void pickFromGallery() {
        pickImageLauncher.launch("image/*");
    }

    private void showNoAppMsg() {
        Toast.makeText(this, "No hay una app para manejar esta acción.", Toast.LENGTH_SHORT).show();
    }
}
```

---

## 3) (Opcional avanzado) Foto a tamaño completo con `FileProvider`

1. Crea un archivo `xml` en `res/xml/file_paths.xml`:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <paths xmlns:android="http://schemas.android.com/apk/res/android">
       <cache-path name="images" path="images/"/>
   </paths>
   ```

2. Declara el `provider` en `AndroidManifest.xml` (dentro de `<application>`):

   ```xml
   <provider
       android:name="androidx.core.content.FileProvider"
       android:authorities="${applicationId}.fileprovider"
       android:exported="false"
       android:grantUriPermissions="true">
       <meta-data
           android:name="android.support.FILE_PROVIDER_PATHS"
           android:resource="@xml/file_paths" />
   </provider>
   ```

3. Antes de lanzar la cámara, crea un archivo temporal y pasa la `Uri` con `EXTRA_OUTPUT`:

   ```java
   File image = new File(getCacheDir(), "images/capture.jpg");
   image.getParentFile().mkdirs();
   Uri photoUri = FileProvider.getUriForFile(this, getPackageName() + ".fileprovider", image);

   Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
   intent.putExtra(MediaStore.EXTRA_OUTPUT, photoUri);
   intent.addFlags(Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
   if (intent.resolveActivity(getPackageManager()) != null) {
       takePictureLauncher.launch(intent);
   }
   ```

   > Luego carga la imagen con la `Uri` creada. Maneja permisos temporales si la transfieres a otra app.

---

## 4) Pruebas y validaciones

-  **Sin app compatible**: al tocar Teléfono/Mapas/Email, se muestra _toast_ “No hay una app para manejar esta acción”.
-  **Chooser** en compartir: se muestra lista de apps.
-  **Cámara (miniatura)**: tras tomar foto, se ve imagen en `imgPreview`.
-  **Galería**: tras elegir imagen, se ve en `imgPreview`.
-  **Rotación**: si pierdes la imagen al rotar, considera guardarla en `onSaveInstanceState` (extra).

---

## 5) Entregables (para evaluación)

-  Código fuente con:
   -  `activity_main.xml` y `MainActivity.java` completos.
   -  Botones conectados y funcionando.
   -  Activity Result API para cámara y galería.
   -  (Opcional) `FileProvider` funcionando para foto a tamaño completo.
-  Un **README** con capturas de pantalla y breve explicación de:
   -  Qué datos se envían/reciben (`Intent`, `extras`, `Uri`).
   -  Casos de prueba realizados.

---

## 6) Criterios de la rúbrica (alineados)

-  (3) 4+ intents implementados (teléfono, mapas, compartir, email).
-  (3) Cámara y galería con Activity Result API mostrando resultado.
-  (2) Validaciones de `resolveActivity`, nulos y errores.
-  (2) Documentación/README breve y clara.

---

### Tips finales

-  **No uses** `startActivityForResult` (obsoleto); usa Activity Result API.
-  Usa `Uri.encode(...)` al formar consultas con espacios.
-  En emuladores, instala **Google Maps** y alguna **app de correo** para pruebas realistas.

---

## Rúbrica de evaluación (10 pts)

-  (3) Implementa correctamente **al menos 4** intents (teléfono, mapas, compartir, email).
-  (3) Integra **Activity Result API** con **cámara** y **galería** mostrando el resultado.
-  (2) Maneja **validaciones** (`resolveActivity`, nulos, errores).
-  (2) Explica en README o comentarios qué **datos** se envían/reciben (extras, `Uri`).

---

## Recursos complementarios

-  **Haz clic aquí para ver el ejemplo**: (coloca el enlace a tu repositorio o a un gist con el código final).

---

## Referencias

-  Smyth, N. (2021). _Android Studio Arctic Fox Essentials - Java Edition: Developing Android Apps Using Android_. Payload Media, Inc. ISBN-13: 978-1-951442-36-1.
-  Google Developers. (s.f.). _Cómo interactuar con otras apps_ — Intents, acciones y resultados. https://developer.android.com/training/basics/intents?hl=es-419
-  La Geekipedia De Ernesto. (2018, 5 de marzo). _Curso Android desde cero #24 | Cómo pasar datos o parámetros de una Activity a otra_ [Video]. https://www.youtube.com/watch?v=5VYe-_rGT1s
