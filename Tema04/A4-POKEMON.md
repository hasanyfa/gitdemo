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

**Llamadas necesarias:**

-  `GET https://pokeapi.co/api/v2/pokemon?limit=50` → obtener los primeros 50 Pokémon

```bash
curl --location 'https://pokeapi.co/api/v2/pokemon?limit=2'
```

-  `GET https://pokeapi.co/api/v2/pokemon/{id}` → obtener detalles de cada uno

```bash
curl --location 'https://pokeapi.co/api/v2/pokemon/1'
```

> **💡 Tip**: Tú puedes validar las llamdas en Postman

### Modelos de Datos

Agregar los archivos:

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

> **Nota**: No es necesario definir todos los campos que retorna la API, solo los que necesites.

### Interfaz para la API

Crea un paquete llamado resources.

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

---

## Paso 4 – Integrar Todo en la Vista Principal

En la función `onCreate` de `MainActivity` añade:

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

## Paso 5 – Cambiar el menú

El título de la Pantalla de Home tiene que ser Pokedex
El título de cada pantalla debe de tener el nombre del pokemon
Cada menú debe de tener el nombre del pokemon
Cada pantalla debe de mostrar el texto del pokemon
