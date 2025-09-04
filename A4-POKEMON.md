# 📱 Pokedex - App Android

> Este proyecto es una adaptación de https://coderslink.com/talento/blog/como-consumir-una-api-desde-una-aplicacion-android/

Estamos ocupando la POKEAPI https://pokeapi.co/

## Paso 1 - Crear un Proyecto

Sigue los pasos 1 al 4 del archivo `GIT_BASICO.md` para crear y configurar tu proyecto Android.
Y agrega el menú de dos items.

## Paso 2 – Configuración inicial

Abre el archivo build.gradle de tu aplicación y añade las siguientes dependencias:

```json
dependencies {
    implementation("com.squareup.retrofit2:retrofit:3.0.0")
    implementation("com.squareup.retrofit2:converter-gson:3.0.0")
    implementation("com.google.code.gson:gson:2.13.1")
}
```

> **💡 Tip**: Podrías tener ya la primera línea y la última por lo que sólo tendrás que agregar las 3 líneas de implementation al json

Después de copiar las dependencias, hacer click en el botón "Synk now" para instalar las dependencias.

Retrofit es un cliente REST extremadamente simple de configurar. Nos permitirá tratar las llamadas a la API como funciones Java, así definiremos solamente las URLs que queremos llamar y los tipos de petición y respuesta que esperamos.

Gson es una librería de Google muy popular para serializar y de-serializar data entre objetos JSON y objetos Java. Así, sin mucho boilerplate, podremos tratar a los datos JSON como clases de Java, pasando de esto:

```json
{
   "count": 1118,
   "results": [
      {
         "name": "bulbasaur",
         "url": "https://pokeapi.co/api/v2/pokemon/1/"
      }
   ]
}
```

A esto:

```java
public class PokemonFetchResults {
    @SerializedName("count")
    @Expose
    private int count;

    @SerializedName("results")
    @Expose
    private ArrayList results;
}
```

También hay que conceder permiso a la app para que se pueda conectar a Internet. Agrega la siguiente línea a tu AndroidManifest.xml:

```xml
<uses-permission android:name="android.permission.INTERNET"
        tools:ignore="ManifestOrder" />
```

> **💡 Tip**: El archivo AndroidManifest.xml lo encuentran en la carpeta app/manifests y debe de pegarse después de la etiqueta </application> y antes de la etiqueta </manifest>

---

## Paso 3 – Definir Endpoints y Modelos

### Interfaz para la API

Crea una nueva interfaz llamada `PokemonAPIService`:

```java
import com.example.pokedex.resources.PokemonFetchResults;
import retrofit2.Call;
import retrofit2.http.GET;

public interface PokemonAPIService {
    @GET("pokemon/?limit=50")
    Call<PokemonFetchResults> getPokemons();
}
```

**Llamadas necesarias:**

-  `GET https://pokeapi.co/api/v2/pokemon?limit=50` → obtener los primeros 50 Pokémon
-  `GET https://pokeapi.co/api/v2/pokemon/{id}` → obtener detalles de cada uno

### Modelos de Datos

### Modelos de Datos

**PokemonFetchResults.java**

```java
public class PokemonFetchResults {
    @SerializedName("results")
    @Expose
    private ArrayList<Pokemon> results;

    public ArrayList<Pokemon> getResults() {
        return results;
    }
}
```

**Pokemon.java**

```java
public class Pokemon {
    @SerializedName("name")
    @Expose
    private String name;

    @SerializedName("url")
    @Expose
    private String url;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getDescription() { return "It's " + getName() + "!"; }
}
```

> **Nota**: No es necesario definir todos los campos que retorna la API, solo los que necesites.

---

## Paso 4 – Integrar Todo en la Vista Principal

## Paso 4 – Integrar Todo en la Vista Principal

En la función `onCreate` de `ItemListActivity` añade:

```java
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://pokeapi.co/api/v2/")
    .addConverterFactory(GsonConverterFactory.create(
        new GsonBuilder().serializeNulls().create()
    ))
    .build();
PokemonAPIService pokemonApiService = retrofit.create(PokemonAPIService.class);
Call<PokemonFetchResults> call = pokemonApiService.getPokemons();
```

### Obtener los Datos

```java
call.enqueue(new Callback<PokemonFetchResults>() {
    @Override
    public void onResponse(Call<PokemonFetchResults> call, Response<PokemonFetchResults> response) {
        if (response.isSuccessful()) {
            ArrayList<Pokemon> pokemonList = response.body().getResults();
            View recyclerView = findViewById(R.id.item_list);
            assert recyclerView != null;
            setupRecyclerView((RecyclerView) recyclerView, pokemonList);
        } else {
            Log.d("Error", "Something happened");
        }
    }

    @Override
    public void onFailure(Call<PokemonFetchResults> call, Throwable t) {
        Log.d("Error", t.toString());
    }
});
```

});

````

### Cambios en el Adapter

En `onBindViewHolder`:

```java
@Override
public void onBindViewHolder(final ViewHolder holder, int position) {
    holder.mIdView.setText(Integer.toString(position));
    holder.mContentView.setText(mValues.get(position).getName());
    holder.itemView.setTag(position);
    holder.itemView.setOnClickListener(mOnClickListener);
}
````

En el `OnClickListener`:

```java
private final View.OnClickListener mOnClickListener = new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        int index = (int) view.getTag();
        Pokemon item = mValues.get(index);

        Context context = view.getContext();
        Intent intent = new Intent(context, ItemDetailActivity.class);
        intent.putExtra(ItemDetailFragment.ARG_ITEM_ID, index + 1);
        intent.putExtra(ItemDetailFragment.ARG_ITEM_NAME, item.getName());
        intent.putExtra(ItemDetailFragment.ARG_DESCRIPTION, item.getDescription());

        context.startActivity(intent);
    }
};
```

> **💡 Tip**: Los Pokémon están numerados desde el 1 y las URLs de la API respetan ese orden.

---

## Paso 5 – Diseñar la UI

Hasta ahora no habíamos tocado la UI porque casi todo lo que necesitamos ya está listo; pero es necesario hacer un cambio en el layout para poder mostrar la foto del Pokémon que el usuario seleccione.

Para ello agregaremos otra dependencia a build.gradle llamada Glide, que nos permite reemplazar “en caliente” una imagen mostrada en un componente ImageView.

```
dependencies {
implementation 'com.github.bumptech.glide:glide:4.11.0'

}
```

Ahora, en activity_item_detail, añadimos el ImageView, lo llamamos item_image y lo agregamos como nodo hijo de toolbar_layout.

```
activity_item_detail.xml

```
