# Instrucciones para Generar APK en Android Studio Narwhal | 2025.1.1 Patch 1

## Requisitos Previos

-  **Android Studio Narwhal | 2025.1.1 Patch 1** instalado
-  Proyecto Android configurado y funcionando
-  SDK de Android instalado
-  Dispositivo Android o emulador para pruebas

## Métodos para Generar APK

### Método 1: Build APK (Recomendado para pruebas)

#### Pasos:

1. **Abrir el proyecto en Android Studio**

   -  Inicia Android Studio
   -  Selecciona "Open an existing Android Studio project"
   -  Navega hasta tu proyecto y ábrelo

2. **Verificar configuración del proyecto**

   -  Asegúrate de que el proyecto compile sin errores
   -  Ejecuta `Build > Clean Project`
   -  Luego ejecuta `Build > Rebuild Project`

3. **Generar APK de depuración**

   -  Ve al menú `Build`
   -  Selecciona `Build Bundle(s) / APK(s)`
   -  Haz clic en `Build APK(s)`

4. **Ubicar el APK generado**
   -  Una vez completado, aparecerá una notificación
   -  Haz clic en "locate" en la notificación
   -  O navega manualmente a: `app/build/outputs/apk/debug/`

### Método 2: Generate Signed Bundle / APK (Para distribución)

#### Pasos:

1. **Acceder al asistente de firma**

   -  Ve al menú `Build`
   -  Selecciona `Generate Signed Bundle / APK...`

2. **Seleccionar tipo de archivo**

   -  Elige `APK` (para instalación directa)
   -  O `Android App Bundle` (para Google Play Store)
   -  Haz clic en `Next`

3. **Crear o seleccionar Key Store**

   **Para nuevo Key Store:**

   -  Haz clic en `Create new...`
   -  Completa los campos:
      -  **Key store path**: Ubicación donde guardar el keystore
      -  **Password**: Contraseña del keystore
      -  **Key alias**: Nombre del alias de la clave
      -  **Key password**: Contraseña de la clave
      -  **Validity (years)**: Años de validez (mínimo 25 años)
      -  **Certificate**: Información del certificado
         -  First and Last Name
         -  Organizational Unit
         -  Organization
         -  City or Locality
         -  State or Province
         -  Country Code

   **Para Key Store existente:**

   -  Selecciona `Choose existing...`
   -  Navega hasta tu archivo `.jks` o `.keystore`
   -  Ingresa las contraseñas correspondientes

4. **Configurar build variants**

   -  Selecciona `release` para versión de producción
   -  O `debug` para versión de prueba
   -  Marca las opciones según necesites:
      -  `V1 (Jar Signature)`: Para compatibilidad con versiones anteriores
      -  `V2 (Full APK Signature)`: Para Android 7.0+
      -  `V3 (APK Signature Scheme v3)`: Para Android 9.0+
      -  `V4 (APK Signature Scheme v4)`: Para Android 11+

5. **Generar APK**
   -  Haz clic en `Create`
   -  Espera a que se complete el proceso

### Método 3: Usar Terminal/Gradle (Avanzado)

#### Para APK de debug:

```bash
./gradlew assembleDebug
```

#### Para APK de release:

```bash
./gradlew assembleRelease
```

## Configuraciones Importantes en build.gradle (Module: app)

### Configuración básica:

```gradle
android {
    compileSdk 34

    defaultConfig {
        applicationId "com.tuempresa.tuapp"
        minSdk 21
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}
```

### Para APK optimizado (release):

```gradle
buildTypes {
    release {
        minifyEnabled true
        shrinkResources true
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        signingConfig signingConfigs.release
    }
}
```

## Ubicaciones de APK Generados

-  **Debug APK**: `app/build/outputs/apk/debug/app-debug.apk`
-  **Release APK**: `app/build/outputs/apk/release/app-release.apk`

## Instalación del APK

### En dispositivo físico:

1. Habilitar "Fuentes desconocidas" en Configuración
2. Transferir APK al dispositivo
3. Abrir archivo APK e instalar

### Usando ADB:

```bash
adb install ruta/al/archivo.apk
```

## Solución de Problemas Comunes

### Error de compilación:

-  Ejecuta `Build > Clean Project`
-  Luego `Build > Rebuild Project`
-  Verifica las dependencias en `build.gradle`

### Error de firma:

-  Verifica que las contraseñas del keystore sean correctas
-  Asegúrate de que el archivo keystore no esté corrupto

### APK muy grande:

-  Habilita `minifyEnabled true` en build.gradle
-  Usa `shrinkResources true` para reducir recursos no utilizados
-  Considera usar App Bundle en lugar de APK

### Problemas de permisos:

-  Verifica permisos en `AndroidManifest.xml`
-  Para Android 6.0+, implementa permisos en tiempo de ejecución

## Mejores Prácticas

1. **Siempre prueba el APK** antes de distribuir
2. **Usa versioning** adecuado (versionCode y versionName)
3. **Guarda tu keystore** en un lugar seguro con backup
4. **Usa ProGuard/R8** para ofuscar código en release
5. **Optimiza imágenes** antes de incluirlas
6. **Prueba en diferentes dispositivos** y versiones de Android

## Versiones de APK

-  **Debug**: Para desarrollo y pruebas internas
-  **Release**: Para distribución final
-  **Signed**: APK firmado para distribución oficial

## Notas Adicionales

-  El APK debug está firmado automáticamente con una clave de debug
-  Para distribución en tiendas, siempre usa APK firmado con tu propia clave
-  Android App Bundle (.aab) es preferido para Google Play Store
-  Mantén actualizadas las versiones del SDK y herramientas

---

**Fecha de creación**: 8 de octubre de 2025  
**Versión de Android Studio**: Narwhal | 2025.1.1 Patch 1
