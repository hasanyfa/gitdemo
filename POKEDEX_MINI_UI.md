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

Modelo de datos completo

-  Clase principal con id, name, weight, sprites, types, abilities
-  Clases anidadas para manejar la estructura JSON de PokeAPI
-  Soporte para sprites normales, shiny, y official artwork

**`PokemonResponse.java`**

```java
public class PokemonResponse {
    public int id;
    public String name;
    public int weight;
    public Sprites sprites;
    public Type[] types;
    public Ability[] abilities;

    public static class Sprites {
        public String front_default;
        public String back_default;
        public String front_shiny;
        public String back_shiny;
        public Other other;

        public static class Other {
            public OfficialArtwork official_artwork;

            public static class OfficialArtwork {
                public String front_default;
                public String front_shiny;
            }
        }
    }

    public static class Type {
        public TypeInfo type;

        public static class TypeInfo {
            public String name;
        }
    }

    public static class Ability {
        public AbilityInfo ability;

        public static class AbilityInfo {
            public String name;
        }
    }
}
```

---

## 🔧 Paso 6. Interfaz de API y cliente Retrofit

Interfaz de API:

-  Interfaz Retrofit para consumir PokeAPI
-  Cliente Retrofit configurado con la URL base
-  Método para obtener Pokémon por nombre o ID

**`PokeApi.java`** y **`ApiClient.java`**

```java
// PokeApi.java
import retrofit2.Call;
import retrofit2.http.GET;
import retrofit2.http.Path;

public interface PokeApi {
    @GET("pokemon/{nameOrId}")
    Call<PokemonResponse> getPokemon(@Path("nameOrId") String nameOrId);
}

// ApiClient.java
import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class ApiClient {
    private static final String BASE_URL = "https://pokeapi.co/api/v2/";
    private static Retrofit retrofit = null;

    public static Retrofit getClient() {
        if (retrofit == null) {
            retrofit = new Retrofit.Builder()
                    .baseUrl(BASE_URL)
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }
        return retrofit;
    }

    public static PokeApi getPokeApi() {
        return getClient().create(PokeApi.class);
    }
}
```

---

## 🧠 Paso 7. Lógica en `MainActivity.java`

Lógica principal completa:

-  Inicialización de todas las vistas y API
-  Búsqueda de Pokémon por nombre o ID
-  Búsqueda aleatoria con el ImageButton
-  Manejo de estados de UI según controles:
-  CheckBox para versión Shiny
-  ToggleButton para Sprite/Artwork
-  RadioButtons para Frente/Espalda
-  Switch para mostrar/ocultar detalles
-  Carga de imágenes con Glide según opciones seleccionadas
-  Función limpiar para resetear toda la UI
-  Manejo de errores para conexión y Pokémon no encontrado

```java
package com.example.minipokedexui;

import android.os.Bundle;
import android.view.View;
import android.widget.*;
import androidx.appcompat.app.AppCompatActivity;
import com.bumptech.glide.Glide;
import retrofit2.Call;
import retrofit2.Callback;
import retrofit2.Response;
import java.util.Random;

public class MainActivity extends AppCompatActivity {

    private EditText etQuery;
    private Button btnSearch, btnClear;
    private ImageButton btnRandom;
    private CheckBox cbShiny;
    private ToggleButton tgSpriteArtwork;
    private RadioGroup rgSide;
    private RadioButton rbFront, rbBack;
    private Switch swDetails;
    private ImageView ivPokemon;
    private TextView tvBasic, tvDetails;

    private PokeApi pokeApi;
    private PokemonResponse currentPokemon;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initViews();
        initApi();
        setupListeners();
    }

    private void initViews() {
        etQuery = findViewById(R.id.etQuery);
        btnSearch = findViewById(R.id.btnSearch);
        btnClear = findViewById(R.id.btnClear);
        btnRandom = findViewById(R.id.btnRandom);
        cbShiny = findViewById(R.id.cbShiny);
        tgSpriteArtwork = findViewById(R.id.tgSpriteArtwork);
        rgSide = findViewById(R.id.rgSide);
        rbFront = findViewById(R.id.rbFront);
        rbBack = findViewById(R.id.rbBack);
        swDetails = findViewById(R.id.swDetails);
        ivPokemon = findViewById(R.id.ivPokemon);
        tvBasic = findViewById(R.id.tvBasic);
        tvDetails = findViewById(R.id.tvDetails);
    }

    private void initApi() {
        pokeApi = ApiClient.getPokeApi();
    }

    private void setupListeners() {
        btnSearch.setOnClickListener(v -> {
            String query = etQuery.getText().toString().trim().toLowerCase();
            if (!query.isEmpty()) {
                searchPokemon(query);
            } else {
                Toast.makeText(this, "Ingresa un nombre o ID", Toast.LENGTH_SHORT).show();
            }
        });

        btnRandom.setOnClickListener(v -> {
            int randomId = new Random().nextInt(1010) + 1; // Pokémon del 1 al 1010
            searchPokemon(String.valueOf(randomId));
        });

        btnClear.setOnClickListener(v -> clearAll());

        // Listeners para actualizar imagen cuando cambian las opciones
        cbShiny.setOnCheckedChangeListener((buttonView, isChecked) -> updatePokemonImage());
        tgSpriteArtwork.setOnCheckedChangeListener((buttonView, isChecked) -> {
            updatePokemonImage();
            // Deshabilitar RadioButtons cuando está en Artwork
            rbFront.setEnabled(!isChecked);
            rbBack.setEnabled(!isChecked);
            if (isChecked) {
                rbFront.setChecked(true); // Artwork solo tiene frente
            }
        });
        rgSide.setOnCheckedChangeListener((group, checkedId) -> updatePokemonImage());

        swDetails.setOnCheckedChangeListener((buttonView, isChecked) -> {
            tvDetails.setVisibility(isChecked ? View.VISIBLE : View.GONE);
        });
    }

    private void searchPokemon(String nameOrId) {
        btnSearch.setEnabled(false);
        btnRandom.setEnabled(false);

        Call<PokemonResponse> call = pokeApi.getPokemon(nameOrId);
        call.enqueue(new Callback<PokemonResponse>() {
            @Override
            public void onResponse(Call<PokemonResponse> call, Response<PokemonResponse> response) {
                btnSearch.setEnabled(true);
                btnRandom.setEnabled(true);

                if (response.isSuccessful() && response.body() != null) {
                    currentPokemon = response.body();
                    displayPokemon();
                } else {
                    Toast.makeText(MainActivity.this, "Pokémon no encontrado", Toast.LENGTH_SHORT).show();
                }
            }

            @Override
            public void onFailure(Call<PokemonResponse> call, Throwable t) {
                btnSearch.setEnabled(true);
                btnRandom.setEnabled(true);
                Toast.makeText(MainActivity.this, "Error de conexión: " + t.getMessage(), Toast.LENGTH_SHORT).show();
            }
        });
    }

    private void displayPokemon() {
        if (currentPokemon == null) return;

        // Información básica
        String basicInfo = String.format("%s (#%d)",
            capitalize(currentPokemon.name), currentPokemon.id);
        tvBasic.setText(basicInfo);

        // Detalles
        StringBuilder details = new StringBuilder();
        details.append("Peso: ").append(currentPokemon.weight / 10.0).append(" kg\n");

        if (currentPokemon.types != null && currentPokemon.types.length > 0) {
            details.append("Tipo(s): ");
            for (int i = 0; i < currentPokemon.types.length; i++) {
                details.append(capitalize(currentPokemon.types[i].type.name));
                if (i < currentPokemon.types.length - 1) details.append(", ");
            }
            details.append("\n");
        }

        if (currentPokemon.abilities != null && currentPokemon.abilities.length > 0) {
            details.append("Habilidades: ");
            for (int i = 0; i < currentPokemon.abilities.length; i++) {
                details.append(capitalize(currentPokemon.abilities[i].ability.name));
                if (i < currentPokemon.abilities.length - 1) details.append(", ");
            }
        }

        tvDetails.setText(details.toString());

        // Actualizar imagen
        updatePokemonImage();
    }

    private void updatePokemonImage() {
        if (currentPokemon == null || currentPokemon.sprites == null) return;

        String imageUrl = null;
        boolean isShiny = cbShiny.isChecked();
        boolean isArtwork = tgSpriteArtwork.isChecked();
        boolean isFront = rbFront.isChecked();

        if (isArtwork) {
            // Official Artwork (solo frente)
            if (currentPokemon.sprites.other != null &&
                currentPokemon.sprites.other.official_artwork != null) {
                imageUrl = isShiny ?
                    currentPokemon.sprites.other.official_artwork.front_shiny :
                    currentPokemon.sprites.other.official_artwork.front_default;
            }
        } else {
            // Sprites normales
            if (isFront) {
                imageUrl = isShiny ?
                    currentPokemon.sprites.front_shiny :
                    currentPokemon.sprites.front_default;
            } else {
                imageUrl = isShiny ?
                    currentPokemon.sprites.back_shiny :
                    currentPokemon.sprites.back_default;
            }
        }

        if (imageUrl != null && !imageUrl.isEmpty()) {
            Glide.with(this)
                .load(imageUrl)
                .placeholder(R.drawable.ic_launcher_foreground)
                .error(R.drawable.ic_launcher_foreground)
                .into(ivPokemon);
        } else {
            Toast.makeText(this, "Imagen no disponible", Toast.LENGTH_SHORT).show();
        }
    }

    private void clearAll() {
        etQuery.setText("");
        tvBasic.setText("Nombre / ID");
        tvDetails.setText("Detalles (tipo, peso, habilidades...)");
        tvDetails.setVisibility(View.GONE);
        ivPokemon.setImageResource(R.drawable.ic_launcher_foreground);

        cbShiny.setChecked(false);
        tgSpriteArtwork.setChecked(false);
        rbFront.setChecked(true);
        swDetails.setChecked(false);
        rbFront.setEnabled(true);
        rbBack.setEnabled(true);

        currentPokemon = null;
    }

    private String capitalize(String str) {
        if (str == null || str.isEmpty()) return str;
        return str.substring(0, 1).toUpperCase() + str.substring(1);
    }
}
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
