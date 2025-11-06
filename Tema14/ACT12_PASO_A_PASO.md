# 📱 ACTIVIDAD 12 - PASO A PASO 🔐 Autenticación Biométrica

## 📋 Tabla de Contenidos

1. [🚀 Configuración inicial del proyecto](#configuración-inicial)
2. [🎨 Configuración de estilos y diseño](#configuración-de-estilos)
3. [🔐 Configuración de permisos](#configuración-de-permisos)
4. [📱 Desarrollo de la interfaz](#desarrollo-de-la-interfaz)
5. [⚙️ Implementación de autenticación biométrica](#implementación-de-autenticación)
6. [🧪 Pruebas y validación](#pruebas-y-validación)
7. [📚 Documentación final](#documentación-final)

---

## 🚀 Configuración inicial del proyecto {#configuración-inicial}

### 1. 📁 Creación del repositorio en GitHub

```bash
# 1. Crear repositorio en GitHub (vía web)
# - Nombre: Actividad12
# - Descripción: App de autenticación biométrica para Android
# - Público/Privado según preferencia
# - Inicializar con README.md

# 2. Clonar el repositorio
git clone https://github.com/tu-usuario/Actividad12.git
cd Actividad12
```

### 2. 👥 Configuración de colaboradores

1. Ve a tu repositorio en GitHub
2. Navega a **Settings** → **Manage access**
3. Haz clic en **Add people**
4. Busca el usuario `hasanyfa`
5. Asigna permisos de **Write**
6. Envía la invitación

### 3. 📱 Crear proyecto Android Studio

1. Abre Android Studio
2. Selecciona **New Project**
3. Elige **Empty Activity**
4. Configura:
   -  **Name**: `BiometricAuth`
   -  **Package name**: `com.tudominio.biometricauth`
   -  **Save location**: Dentro de la carpeta del repositorio clonado
   -  **Language**: Java
   -  **Minimum SDK**: API 23 (Android 6.0) - Requerido para BiometricPrompt

---

## 🎨 Configuración de estilos y diseño {#configuración-de-estilos}

### 4. 🌈 Definir paleta de colores

**Archivo**: `app/src/main/res/values/colors.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Colores primarios -->
    <color name="primary_blue">#2196F3</color>
    <color name="primary_dark_blue">#1976D2</color>
    <color name="primary_light_blue">#BBDEFB</color>

    <!-- Colores secundarios -->
    <color name="secondary_teal">#009688</color>
    <color name="secondary_dark_teal">#00695C</color>
    <color name="secondary_light_teal">#B2DFDB</color>

    <!-- Colores de acento -->
    <color name="accent_orange">#FF9800</color>
    <color name="accent_green">#4CAF50</color>
    <color name="accent_red">#F44336</color>

    <!-- Colores de fondo y texto -->
    <color name="background_white">#FFFFFF</color>
    <color name="background_light_gray">#F5F5F5</color>
    <color name="text_primary">#212121</color>
    <color name="text_secondary">#757575</color>
    <color name="text_hint">#BDBDBD</color>

    <!-- Estados -->
    <color name="success_green">#4CAF50</color>
    <color name="error_red">#F44336</color>
    <color name="warning_amber">#FFC107</color>
</resources>
```

### 5. 🔤 Configurar tipografía personalizada

**Paso 1**: Descargar fuente de [Google Fonts](https://fonts.google.com/)

-  Recomendación: **Roboto** o **Open Sans**

**Paso 2**: Crear carpeta `app/src/main/res/font/`

**Paso 3**: Agregar archivos de fuente (ejemplo con Roboto):

-  `roboto_regular.ttf`
-  `roboto_bold.ttf`
-  `roboto_light.ttf`

### 6. 🎭 Configurar tema principal

**Archivo**: `app/src/main/res/values/themes.xml`

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.BiometricAuth" parent="Theme.MaterialComponents.DayNight.DarkActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/primary_blue</item>
        <item name="colorPrimaryVariant">@color/primary_dark_blue</item>
        <item name="colorOnPrimary">@color/background_white</item>

        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/secondary_teal</item>
        <item name="colorSecondaryVariant">@color/secondary_dark_teal</item>
        <item name="colorOnSecondary">@color/background_white</item>

        <!-- Status bar color. -->
        <item name="android:statusBarColor" tools:targetApi="l">?attr/colorPrimaryVariant</item>

        <!-- Customize your theme here. -->
        <item name="android:fontFamily">@font/roboto_regular</item>
    </style>

    <!-- Estilo personalizado para botones -->
    <style name="CustomButton" parent="Widget.MaterialComponents.Button">
        <item name="android:layout_width">match_parent</item>
        <item name="android:layout_height">56dp</item>
        <item name="android:layout_margin">16dp</item>
        <item name="android:textSize">16sp</item>
        <item name="android:fontFamily">@font/roboto_bold</item>
        <item name="cornerRadius">8dp</item>
        <item name="backgroundTint">@color/primary_blue</item>
    </style>

    <!-- Estilo para títulos -->
    <style name="TitleText">
        <item name="android:layout_width">wrap_content</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:textSize">24sp</item>
        <item name="android:textColor">@color/text_primary</item>
        <item name="android:fontFamily">@font/roboto_bold</item>
        <item name="android:layout_marginBottom">16dp</item>
    </style>

    <!-- Estilo para texto descriptivo -->
    <style name="DescriptionText">
        <item name="android:layout_width">wrap_content</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:textSize">16sp</item>
        <item name="android:textColor">@color/text_secondary</item>
        <item name="android:fontFamily">@font/roboto_regular</item>
        <item name="android:textAlignment">center</item>
        <item name="android:layout_marginBottom">32dp</item>
    </style>
</resources>
```

---

## 🔐 Configuración de permisos {#configuración-de-permisos}

### 7. 📋 Configurar AndroidManifest.xml

**Archivo**: `app/src/main/AndroidManifest.xml`

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <!-- Permisos para autenticación biométrica -->
    <uses-permission android:name="android.permission.USE_FINGERPRINT" />
    <uses-permission android:name="android.permission.USE_BIOMETRIC" />

    <!-- Declarar que la app requiere sensor de huella (opcional) -->
    <uses-feature
        android:name="android.hardware.fingerprint"
        android:required="false" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.BiometricAuth"
        tools:targetApi="31">

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

### 8. 📦 Agregar dependencias necesarias

**Archivo**: `app/build.gradle` (Module: app)

```gradle
dependencies {
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.10.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'

    // Dependencia para autenticación biométrica
    implementation 'androidx.biometric:biometric:1.1.0'

    // Para iconos adicionales
    implementation 'androidx.vectordrawable:vectordrawable:1.1.0'

    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
}
```

---

## 📱 Desarrollo de la interfaz {#desarrollo-de-la-interfaz}

### 9. 🎨 Diseñar layout principal

**Archivo**: `app/src/main/res/layout/activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/background_light_gray"
    tools:context=".MainActivity">

    <!-- Contenedor principal -->
    <androidx.cardview.widget.CardView
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_margin="24dp"
        app:cardCornerRadius="16dp"
        app:cardElevation="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:padding="32dp">

            <!-- Icono de huella digital -->
            <ImageView
                android:id="@+id/fingerprintIcon"
                android:layout_width="120dp"
                android:layout_height="120dp"
                android:layout_gravity="center"
                android:layout_marginBottom="24dp"
                android:src="@drawable/ic_fingerprint"
                android:tint="@color/primary_blue"
                app:tint="@color/primary_blue" />

            <!-- Título -->
            <TextView
                android:id="@+id/titleText"
                style="@style/TitleText"
                android:layout_gravity="center"
                android:text="@string/auth_title" />

            <!-- Descripción -->
            <TextView
                android:id="@+id/descriptionText"
                style="@style/DescriptionText"
                android:layout_gravity="center"
                android:text="@string/auth_description" />

            <!-- Estado de autenticación -->
            <TextView
                android:id="@+id/statusText"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginBottom="24dp"
                android:fontFamily="@font/roboto_regular"
                android:gravity="center"
                android:text="@string/ready_to_authenticate"
                android:textColor="@color/text_secondary"
                android:textSize="14sp" />

            <!-- Botón de autenticación -->
            <com.google.android.material.button.MaterialButton
                android:id="@+id/authenticateButton"
                style="@style/CustomButton"
                android:text="@string/authenticate_button"
                app:icon="@drawable/ic_fingerprint"
                app:iconGravity="textStart" />

        </LinearLayout>

    </androidx.cardview.widget.CardView>

</androidx.constraintlayout.widget.ConstraintLayout>
```

### 10. 🎨 Crear iconos vectoriales

**Archivo**: `app/src/main/res/drawable/ic_fingerprint.xml`

```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp"
    android:height="24dp"
    android:viewportWidth="24"
    android:viewportHeight="24"
    android:tint="?attr/colorOnSurface">
  <path
      android:fillColor="@android:color/white"
      android:pathData="M17.81,4.47c-0.08,0 -0.16,-0.02 -0.23,-0.06C15.66,3.42 14,3 12.01,3c-1.98,0 -3.86,0.47 -5.57,1.41 -0.24,0.13 -0.54,0.04 -0.68,-0.2 -0.13,-0.24 -0.04,-0.55 0.2,-0.68C7.82,2.52 9.86,2 12.01,2c2.13,0 3.99,0.47 6.03,1.52 0.25,0.13 0.34,0.43 0.21,0.67 -0.09,0.18 -0.26,0.28 -0.44,0.28zM3.5,9.72c-0.1,0 -0.2,-0.03 -0.29,-0.09 -0.23,-0.16 -0.28,-0.47 -0.12,-0.7 0.99,-1.4 2.25,-2.5 3.75,-3.27C9.98,4.04 14,4.03 17.15,5.65c1.5,0.77 2.76,1.86 3.75,3.25 0.16,0.22 0.11,0.54 -0.12,0.7 -0.23,0.16 -0.54,0.11 -0.7,-0.12 -0.9,-1.26 -2.04,-2.25 -3.39,-2.94 -2.87,-1.47 -6.54,-1.47 -9.4,0.01 -1.36,0.7 -2.5,1.7 -3.4,2.96 -0.08,0.14 -0.23,0.21 -0.39,0.21zM9.75,21.79c-0.13,0 -0.26,-0.05 -0.35,-0.15 -0.87,-0.87 -1.34,-1.43 -2.01,-2.64 -0.69,-1.23 -1.05,-2.73 -1.05,-4.34 0,-2.97 2.54,-5.39 5.66,-5.39s5.66,2.42 5.66,5.39c0,0.28 -0.22,0.5 -0.5,0.5s-0.5,-0.22 -0.5,-0.5c0,-2.42 -2.09-4.39 -4.66,-4.39 -2.57,0 -4.66,1.97 -4.66,4.39 0,1.44 0.32,2.77 0.93,3.85 0.64,1.15 1.08,1.64 1.85,2.42 0.19,0.2 0.19,0.51 0,0.71 -0.11,0.1 -0.24,0.15 -0.37,0.15zM16.92,19.94c-1.19,0 -2.24,-0.3 -3.1,-0.89 -1.49,-1.01 -2.41,-2.73 -2.41,-4.5 0,-0.28 0.22,-0.5 0.5,-0.5s0.5,0.22 0.5,0.5c0,1.41 0.72,2.74 1.94,3.56 0.71,0.48 1.54,0.71 2.57,0.71 0.24,0 0.64,-0.03 1.04,-0.1 0.27,-0.05 0.53,0.13 0.58,0.41 0.05,0.27 -0.13,0.53 -0.41,0.58 -0.57,0.11 -1.07,0.23 -1.21,0.23zM12.01,16.85c-0.66,0 -1.26,-0.27 -1.69,-0.71 -0.19,-0.19 -0.19,-0.51 0,-0.71 0.19,-0.19 0.51,-0.19 0.71,0 0.23,0.23 0.57,0.42 0.98,0.42 0.45,0 0.78,-0.19 1.01,-0.42 0.19,-0.19 0.51,-0.19 0.71,0 0.19,0.19 0.19,0.51 0,0.71 -0.44,0.44 -1.04,0.71 -1.72,0.71z"/>
</vector>
```

### 11. 📝 Definir strings

**Archivo**: `app/src/main/res/values/strings.xml`

```xml
<resources>
    <string name="app_name">Autenticación Biométrica</string>

    <!-- Textos de la interfaz -->
    <string name="auth_title">Autenticación Biométrica</string>
    <string name="auth_description">Utiliza tu huella digital para acceder de forma segura</string>
    <string name="authenticate_button">Autenticar con huella</string>
    <string name="ready_to_authenticate">Listo para autenticar</string>

    <!-- Estados de autenticación -->
    <string name="auth_success">✅ Autenticación exitosa</string>
    <string name="auth_failed">❌ Autenticación fallida</string>
    <string name="auth_error">⚠️ Error en la autenticación</string>
    <string name="auth_canceled">🚫 Autenticación cancelada</string>

    <!-- Mensajes del BiometricPrompt -->
    <string name="biometric_prompt_title">Verificación biométrica</string>
    <string name="biometric_prompt_subtitle">Usa tu huella digital para continuar</string>
    <string name="biometric_prompt_description">Coloca tu dedo en el sensor de huella digital</string>
    <string name="biometric_prompt_negative_button">Cancelar</string>

    <!-- Mensajes de error -->
    <string name="biometric_not_supported">La autenticación biométrica no está disponible</string>
    <string name="biometric_not_enrolled">No hay huellas registradas en el dispositivo</string>
    <string name="biometric_no_hardware">No se detectó hardware biométrico</string>
</resources>
```
