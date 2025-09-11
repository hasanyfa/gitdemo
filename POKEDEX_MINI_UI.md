# 🧪 Ejercicio Android (Java): “PokeDex Mini UI” con PokeAPI

**Tema:** Elementos de interfaz gráfica (Android Studio – Java)  
**Duración estimada:** 90–120 min  
**Nivel:** Principiantes/intermedio

---

## 🎯 Objetivos de aprendizaje

-  Usar **EditText**, **Hint**, **Button**, **ImageButton**, **ToggleButton**, **Switch**, **CheckBox**, **RadioGroup/RadioButton**, **ImageView** desde el **Palette**.
-  Consumir una API pública (**PokeAPI**) con **Retrofit** + **Gson**.
-  Cargar imágenes remotas con **Glide**.
-  Manejar estados de UI según los controles seleccionados.

---

## ✅ Requisitos previos

-  Android Studio (Giraffe o superior).
-  **SDK mínimo:** 21 (Android 5.0) o superior.
-  Conexión a Internet.

---

## 🧰 Entregables

-  App que permite **buscar un Pokémon** por nombre o ID.
-  UI que:
   -  EditText con **hint** para búsqueda.
   -  **Button** “Buscar”.
   -  **ImageButton** para “**Aleatorio**”.
   -  **CheckBox** “Shiny”.
   -  **RadioButtons**: “Frente” y “Espalda”.
   -  **ToggleButton**: “Sprite / Artwork”.
   -  **Switch**: “Mostrar detalles”.
   -  **Button** “Limpiar”.
   -  **ImageView** que muestra la imagen.
   -  TextViews para nombre/ID y detalles (peso, tipo, habilidades) si procede.

---

## 🧱 Paso 1. Crear el proyecto

1. **New Project → Empty Views Activity**
2. **Name:** `MiniPokedexUI`
3. **Language:** Java
4. **Minimum SDK:** API 21+
5. Finish.

---

## 🌐 Paso 2. Permiso de Internet

**`app/src/main/AndroidManifest.xml`**

```xml
<manifest ... >
    <uses-permission android:name="android.permission.INTERNET" />
    <application ...>
        ...
    </application>
</manifest>
```

---

## 📦 Paso 3. Dependencias (Retrofit, Gson, Glide)

**`app/build.gradle`**

```gradle
dependencies {
    implementation 'com.squareup.retrofit2:retrofit:2.11.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.11.0'
    implementation 'com.github.bumptech.glide:glide:4.16.0'
    annotationProcessor 'com.github.bumptech.glide:compiler:4.16.0'
}
```

**Sync Now**.

---

## 🧩 Paso 4. Diseñar la UI en XML

**`app/src/main/res/layout/activity_main.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <ScrollView
        android:fillViewport="true"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <LinearLayout
            android:orientation="vertical"
            android:padding="16dp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <!-- Título -->
            <TextView
                android:id="@+id/tvTitle"
                android:text="Mini PokeDex UI"
                android:textStyle="bold"
                android:textSize="22sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <!-- EditText con Hint -->
            <EditText
                android:id="@+id/etQuery"
                android:layout_width="match_parent"
                android:layout_height="48dp"
                android:layout_marginTop="12dp"
                android:hint="Nombre o ID (e.g. pikachu o 25)"
                android:inputType="text" />

            <!-- Acciones principales -->
            <LinearLayout
                android:orientation="horizontal"
                android:layout_marginTop="8dp"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <Button
                    android:id="@+id/btnSearch"
                    android:text="Buscar"
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1" />

                <ImageButton
                    android:id="@+id/btnRandom"
                    android:src="@android:drawable/ic_menu_rotate"
                    android:contentDescription="Aleatorio"
                    android:background="?attr/selectableItemBackgroundBorderless"
                    android:layout_marginStart="12dp"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />
            </LinearLayout>

            <!-- Opciones de imagen -->
            <CheckBox
                android:id="@+id/cbShiny"
                android:text="Shiny"
                android:layout_marginTop="8dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <ToggleButton
                android:id="@+id/tgSpriteArtwork"
                android:textOn="Artwork"
                android:textOff="Sprite"
                android:layout_marginTop="4dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <RadioGroup
                android:id="@+id/rgSide"
                android:orientation="horizontal"
                android:layout_marginTop="4dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content">
                <RadioButton
                    android:id="@+id/rbFront"
                    android:checked="true"
                    android:text="Frente"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content" />
                <RadioButton
                    android:id="@+id/rbBack"
                    android:text="Espalda"
                    android:layout_marginStart="12dp"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content" />
            </RadioGroup>

            <Switch
                android:id="@+id/swDetails"
                android:layout_width="wrap_content"
                android:layout_height="48dp"
                android:layout_marginTop="4dp"
                android:text="Mostrar detalles" />

            <!-- Imagen del Pokémon -->
            <ImageView
                android:id="@+id/ivPokemon"
                android:contentDescription="Imagen del Pokémon"
                android:adjustViewBounds="true"
                android:scaleType="fitCenter"
                android:layout_marginTop="12dp"
                android:layout_width="match_parent"
                android:layout_height="200dp" />

            <!-- Info básica -->
            <TextView
                android:id="@+id/tvBasic"
                android:text="Nombre / ID"
                android:textStyle="bold"
                android:layout_marginTop="8dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />

            <!-- Detalles (ocultos con el Switch) -->
            <TextView
                android:id="@+id/tvDetails"
                android:text="Detalles (tipo, peso, habilidades...)"
                android:visibility="gone"
                android:layout_marginTop="4dp"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />

            <!-- Limpiar -->
            <Button
                android:id="@+id/btnClear"
                android:text="Limpiar"
                android:layout_marginTop="12dp"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />

        </LinearLayout>
    </ScrollView>


</androidx.constraintlayout.widget.ConstraintLayout>
```

---

## 🔌 Paso 5. Modelo de datos mínimo para PokeAPI

**`PokemonResponse.java`**

```java
// Código completo mostrado antes
```

---

## 🔧 Paso 6. Interfaz de API y cliente Retrofit

**`PokeApi.java`** y **`ApiClient.java`**

```java
// Código completo mostrado antes
```

---

## 🧠 Paso 7. Lógica en `MainActivity.java`

```java
// Código completo mostrado antes
```

---

## 🧭 Paso 8. Prueba rápida

1. Ejecuta la app.
2. Escribe `pikachu` o `25` y toca **Buscar**.
3. Activa **Shiny** y alterna **Frente/Espalda** con los **RadioButtons**.
4. Cambia **Sprite/Artwork** con el **ToggleButton**.
5. Activa el **Switch** “Mostrar detalles”.
6. Prueba el **ImageButton** “Aleatorio”.
7. Usa **Limpiar** para resetear.

---

## 🧪 Paso 9. Experimentos sugeridos

-  Deshabilitar **RadioButtons** cuando el **ToggleButton** esté en **Artwork**.
-  Validación si no hay conexión.
-  Añadir **ProgressBar** mientras carga.
-  Localización de textos.
-  Manejo de errores 404.

---

## 🧑‍🏫 Rúbrica de evaluación

| Criterio                                                                           |  Puntos |
| ---------------------------------------------------------------------------------- | ------: |
| UI implementa todos los componentes solicitados                                    |      30 |
| Consumo de PokeAPI con Retrofit + manejo básico de errores                         |      25 |
| Carga de imagen con Glide y lógica según opciones (shiny, frente/espalda, artwork) |      25 |
| Código ordenado, comentarios y nomenclatura                                        |      10 |
| Extras (ProgressBar, validaciones, mejoras UX)                                     |      10 |
| **Total**                                                                          | **100** |

---

## 📝 Notas

-  **PokeAPI** es pública; no requiere API key.
-  Si el Pokémon no existe, Retrofit regresará **404** → manejar con `onResponse` no exitoso.

## 💡 ProTip

> 🚀 **¡Nunca dejes de aprender!** El desarrollo de aplicaciones móviles es un campo en constante evolución.
>
> 🔥 **Consejos para seguir creciendo:**
>
> -  📱 Practica creando mini-aplicaciones cada semana (aunque lo seguiremos haciendo con cada tema..😂)
> -  🌟 Experimenta con nuevos componentes de UI
> -  👥 Únete a comunidades de desarrolladores Android
> -  📚 Mantente actualizado con las últimas versiones de Android
> -  🎯 Enfócate en crear experiencias de usuario intuitivas
>
> 💪 **¡Tu próxima app podría cambiar el mundo!** 🌍
