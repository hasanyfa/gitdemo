# 🌌 **Guía para Crear una App Mágica con Android**

## ✨ 1) Configuración inicial

-  **Crear proyecto**: Android Studio → Empty Views Activity → Lenguaje **Java**, Mínimo SDK **API 24+**.
-  **Nombre sugerido**: `Actividad06`
-  **Paquete ejemplo**: `com.nickname.actividad06`

---

## 🎨 2) Colores, tipografía y tema

### 🎨 **Paleta de colores** (archivo: `res/values/colors.xml`)

```xml
<resources>
    <color name="md_bg">#0C0F1A</color>         <!-- Azul noche -->
    <color name="md_primary">#5C7AEA</color>   <!-- Azul luminoso -->
    <color name="md_secondary">#E1BEE7</color> <!-- Violeta tenue -->
    <color name="md_text">#EAEAF2</color>      <!-- Blanco suave -->
    <color name="md_accent">#F7C948</color>    <!-- Dorado (destellos) -->
</resources>
```

### 🖋️ **Fuentes** (opcional, recomendado)

1. Descarga fuentes de [Google Fonts](https://fonts.google.com) como:
   -  **Cinzel** para títulos.
   -  **Montserrat** para el cuerpo.
2. Crea la carpeta `res/font/` y agrega los archivos `.ttf` (por ejemplo, `cinzel_regular.ttf` y `montserrat_regular.ttf`).

Archivo: `res/values/fonts.xml`

```xml
<resources>
    <string name="font_title">@font/cinzel_regular</string>
    <string name="font_body">@font/montserrat_regular</string>
</resources>
```

### 🎭 **Tema** (archivo: `res/values/themes.xml`)

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <style name="Theme.MagicScenes" parent="Theme.Material3.DayNight.NoActionBar">
        <item name="android:statusBarColor">@color/md_bg</item>
        <item name="android:navigationBarColor">@color/md_bg</item>
        <item name="android:windowBackground">@color/md_bg</item>
        <item name="colorPrimary">@color/md_primary</item>
        <item name="colorSecondary">@color/md_secondary</item>
        <item name="android:fontFamily">@font/montserrat_regular</item>
        <item name="textColor">@color/md_text</item>
    </style>
</resources>
```

---

## 🖼️ 3) Recursos gráficos

### 🖼️ **Imágenes**

Coloca dos imágenes en `res/drawable/`:

-  `scene1.jpg` (o `.png`)
-  `scene2.jpg`

### 🌈 **Fondo con gradiente**

Archivo: `res/drawable/bg_gradient.xml`

```xml
<gradient xmlns:android="http://schemas.android.com/apk/res/android"
    android:startColor="#0C0F1A"
    android:endColor="#5C7AEA"
    android:angle="270"/>
```

o

```xml
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <shape android:shape="rectangle">
            <gradient
                android:startColor="@color/md_bg"
                android:endColor="#10152A"
                android:angle="270"/>
        </shape>
    </item>
    <item android:gravity="center">
        <shape android:shape="oval">
            <size android:width="600dp" android:height="600dp"/>
            <gradient
                android:startColor="#22FFFFFF"
                android:centerColor="#11FFFFFF"
                android:endColor="#00FFFFFF"
                android:gradientRadius="300dp"
                android:type="radial"/>
        </shape>
    </item>
</layer-list>
```

---

## 🎥 4) Animaciones de transición

Crea la carpeta `res/anim/` y agrega los siguientes archivos:

### ➡️ **slide_in_right.xml**

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="100%" android:toXDelta="0%" android:duration="500"/>
    <alpha android:fromAlpha="0" android:toAlpha="1" android:duration="500"/>
</set>
```

### ⬅️ **slide_out_left.xml**

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="0%" android:toXDelta="-100%" android:duration="500"/>
    <alpha android:fromAlpha="1" android:toAlpha="0" android:duration="500"/>
</set>
```

### ⬅️ **slide_in_left.xml**

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="-100%" android:toXDelta="0%" android:duration="500"/>
    <alpha android:fromAlpha="0" android:toAlpha="1" android:duration="500"/>
</set>
```

### 🔍 **zoom_fade_in.xml**

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <scale android:fromXScale="0.9" android:toXScale="1.0"
           android:fromYScale="0.9" android:toYScale="1.0"
           android:pivotX="50%" android:pivotY="50%" android:duration="600"/>
    <alpha android:fromAlpha="0" android:toAlpha="1" android:duration="600"/>
</set>
```

---

## 📜 5) Manifest

Archivo: `AndroidManifest.xml`

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:theme="@style/Theme.MagicScenes"
        android:allowBackup="true"
        android:label="MagicScenes">
        <activity android:name=".Scene2Activity"
            android:exported="false"/>
        <activity android:name=".Scene1Activity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>
</manifest>
```

---

## 🖌️ 6) Layouts

Usaremos ViewBinding para mayor comodidad.

### 📄 **activity_scene1.xml**

Archivo: `res/layout/activity_scene1.xml`

```xml
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:background="@drawable/bg_magic_gradient"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:padding="20dp"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/tvTitle"
            android:text="Escena I — La llamada a la aventura"
            android:textSize="24sp"
            android:textStyle="bold"
            android:fontFamily="@font/cinzel_regular"
            android:textColor="@color/md_accent"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

        <ImageView
            android:id="@+id/ivScene"
            android:src="@drawable/scene1"
            android:contentDescription="@string/app_name"
            android:layout_marginTop="16dp"
            android:layout_width="match_parent"
            android:layout_height="220dp"
            android:scaleType="centerCrop"
            android:alpha="0"
            />

        <TextView
            android:id="@+id/tvDescription"
            android:layout_marginTop="16dp"
            android:textColor="@color/md_text"
            android:textSize="16sp"
            android:lineSpacingExtra="4dp"
            android:text="Descripción inmersiva de la escena 1: el protagonista descubre el llamado que cambiará su destino. Los colores azules y dorados destellan como si un hechizo se activara..."
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btnNext"
            android:text="Viajar a la siguiente escena ✨"
            android:textAllCaps="false"
            android:layout_marginTop="24dp"
            android:backgroundTint="@color/md_primary"
            android:textColor="@color/md_text"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>
    </LinearLayout>
</ScrollView>
```

### 📄 **activity_scene2.xml**

Archivo: `res/layout/activity_scene2.xml`

```xml
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:background="@drawable/bg_magic_gradient"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:padding="20dp"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/tvTitle"
            android:text="Escena II — El clímax bajo las estrellas"
            android:textSize="24sp"
            android:textStyle="bold"
            android:fontFamily="@font/cinzel_regular"
            android:textColor="@color/md_accent"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

        <ImageView
            android:id="@+id/ivScene"
            android:src="@drawable/scene2"
            android:contentDescription="@string/app_name"
            android:layout_marginTop="16dp"
            android:layout_width="match_parent"
            android:layout_height="220dp"
            android:scaleType="centerCrop"
            android:alpha="0"
            />

        <TextView
            android:id="@+id/tvDescription"
            android:layout_marginTop="16dp"
            android:textColor="@color/md_text"
            android:textSize="16sp"
            android:lineSpacingExtra="4dp"
            android:text="Descripción inmersiva de la escena 2: la banda sonora se eleva, el cielo se abre y la magia culmina en un destello dorado que envuelve a los héroes..."
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <LinearLayout
            android:orientation="horizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="24dp">

            <Button
                android:id="@+id/btnBack"
                android:text="Regresar ⬅️"
                android:textAllCaps="false"
                android:layout_weight="1"
                android:backgroundTint="@color/md_secondary"
                android:textColor="@color/md_bg"
                android:layout_width="0dp"
                android:layout_height="wrap_content"/>

            <Space
                android:layout_width="12dp"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/btnToScene1"
                android:text="Escena I ✨"
                android:textAllCaps="false"
                android:layout_weight="1"
                android:backgroundTint="@color/md_primary"
                android:textColor="@color/md_text"
                android:layout_width="0dp"
                android:layout_height="wrap_content"/>
        </LinearLayout>
    </LinearLayout>
</ScrollView>
```

---

## 🧙‍♂️ 7) Actividades en Java

### **Scene1Activity.java**

```java
package com.nickname.actividad06;

import android.content.Intent;
import android.os.Bundle;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;

import androidx.activity.OnBackPressedCallback;
import androidx.appcompat.app.AppCompatActivity;

import com.example.magicscenes.databinding.ActivityScene1Binding;

public class Scene1Activity extends AppCompatActivity {

    private ActivityScene1Binding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = ActivityScene1Binding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Anima la imagen al entrar (zoom + fade)
        Animation zoomFade = AnimationUtils.loadAnimation(this, R.anim.zoom_fade_in);
        binding.ivScene.startAnimation(zoomFade);

        // Botón para ir a la escena 2
        binding.btnNext.setOnClickListener(v -> {
            Intent intent = new Intent(Scene1Activity.this, Scene2Activity.class);
            startActivity(intent);
            // Transición "viaje mágico"
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        // Manejo de back (si hiciera falta personalizar)
        getOnBackPressedDispatcher().addCallback(this, new OnBackPressedCallback(true) {
            @Override public void handleOnBackPressed() {
                finish();
            }
        });
    }

    @Override
    protected void onResume() {
        super.onResume();
        // Reaplica un pequeño fade a la imagen si vuelven
        binding.ivScene.clearAnimation();
        binding.ivScene.setAlpha(0f);
        binding.ivScene.animate().alpha(1f).setDuration(500).start();
    }
}
```

### **Scene2Activity.java**

```java
package com.nickname.actividad06

import android.content.Intent;
import android.os.Bundle;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;

import androidx.appcompat.app.AppCompatActivity;

import com.example.magicscenes.databinding.ActivityScene2Binding;

public class Scene2Activity extends AppCompatActivity {

    private ActivityScene2Binding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = ActivityScene2Binding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Anima la imagen al entrar
        Animation zoomFade = AnimationUtils.loadAnimation(this, R.anim.zoom_fade_in);
        binding.ivScene.startAnimation(zoomFade);

        // Regresar (cierra la Activity actual con transición inversa)
        binding.btnBack.setOnClickListener(v -> {
            finish();
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        // Ir a la escena 1 (reinicia Activity1 para ver animación)
        binding.btnToScene1.setOnClickListener(v -> {
            Intent intent = new Intent(Scene2Activity.this, Scene1Activity.class);
            intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP | Intent.FLAG_ACTIVITY_SINGLE_TOP);
            startActivity(intent);
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });
    }

    @Override
    public void onBackPressed() {
        super.onBackPressed();
        overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
    }
}
```

---

## 📖 8) Textos (strings)

Archivo: `res/values/strings.xml`

```xml
<resources>
    <string name="app_name">MagicScenes</string>
    <string name="scene1_title">Escena I — La llamada a la aventura</string>
    <string name="scene2_title">Escena II — El clímax bajo las estrellas</string>
    <string name="scene1_desc">Descripción inmersiva de la escena 1 ...</string>
    <string name="scene2_desc">Descripción inmersiva de la escena 2 ...</string>
    <string name="next">Viajar a la siguiente escena ✨</string>
    <string name="back">Regresar ⬅️</string>
    <string name="to_scene1">Escena I ✨</string>
</resources>
```

---

## 🌟 9) Detalles de UX/UI recomendados

-  **Paleta**: Azules nocturnos + dorado de luz mágica.
-  **Tipografía**: Títulos con **Cinzel**, cuerpo con **Montserrat**.
-  **Accesibilidad**: Contraste alto, botones grandes, touch targets ≥ 48dp.
-  **Animaciones**: Sutiles (500–600 ms).

---

## 🎬 10) Cómo personalizar a tu película

-  **Imágenes**: reemplaza `scene1` y `scene2` por fotogramas o arte original (sin infringir derechos si es para publicación).
-  **Colores**: ajusta `colors.xml` a la atmósfera:
   -  Sci-fi: cian/neón (#00E5FF), gris oscuro (#121212), acentos magenta.
   -  Épica medieval: azul petróleo, dorado, granate tenue.
-  **Fuentes**: cambia `font_title` por una serif decorativa y `font_body` por sans-serif legible.
-  **Textos**: narra en segunda persona (“cruzas el arco...”), añade onomatopeyas y metáforas moderadas.
