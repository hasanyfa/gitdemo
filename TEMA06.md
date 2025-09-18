# 📱 Ejercicio Android (Java): _Agenda con Spinner, Pickers, ImageButtons y ListView_

> Objetivo: construir una mini-app donde el usuario seleccione una
> **categoría** (Spinner), elija **fecha** y **hora** (Pickers), añada
> una **descripción** con un **ImageButton** y vea todo en una
> **ListView** (con opción de borrar).

---

## ✅ Competencias que practicarás

-  **Spinner:** poblarlo con recursos y leer la selección.
-  **Pickers:** usar `DatePickerDialog` y `TimePickerDialog`.
-  **ImageButton:** acciones de "elegir fecha", "elegir hora",
   "agregar" y "limpiar".
-  **ListView:** mostrar elementos, eliminar con long-press y refrescar
   con `ArrayAdapter`.

---

## 🧰 Requisitos

-  Android Studio (última versión estable).
-  SDK Android configurado.
-  Conocimientos básicos de Java y AndroidX.
-  Git instalado y cuenta en GitHub.

---

## 🧪 Resultado esperado

Una pantalla con: - **Spinner** de categorías. - **Fecha** y **Hora**
mostradas en `TextView` y seleccionables con **ImageButtons**. -
**EditText** para descripción + **ImageButton** "Agregar". -
**ImageButton** "Limpiar". - **ListView** listando:
`📌 Categoría — Descripción (YYYY-MM-DD HH:mm)`.\
Borrado de un ítem con **long-press**.

---

## 🧭 Paso a paso (Android Studio)

### 0) Crear el proyecto proyecto

Sigue los pasos 1 al 4 del archivo [GIT_BASICO.md](GIT_BASICO.md) para crear y configurar tu proyecto Android.

Esta vez tienes que seleccionar **"Empty Activity"** y también debes eliminar el texto "Hello World"

1. **New Project → Empty Views Activity** (o _Empty Activity_).
2. Nombre: `Actividad05`
3. Lenguaje: **Java**
4. Minimum SDK: **API 24** o superior.
5. Finish.

> ⚠️ **No olvides** agregar a `hasanyfa` como colaborador del proyecto.

---

### 1) Agregar recursos de texto (strings)

**`app/src/main/res/values/strings.xml`**

```xml
<resources>
    <string name="app_name">AgendaPickers</string>

    <string name="label_categoria">Categoría</string>
    <string name="label_fecha">Fecha</string>
    <string name="label_hora">Hora</string>
    <string name="hint_descripcion">Descripción (ej. Reunión con equipo)</string>
    <string name="cd_pick_fecha">Elegir fecha</string>
    <string name="cd_pick_hora">Elegir hora</string>
    <string name="cd_agregar">Agregar elemento</string>
    <string name="cd_limpiar">Limpiar lista</string>

    <string-array name="categorias">
        <item>Trabajo</item>
        <item>Estudio</item>
        <item>Personal</item>
        <item>Salud</item>
    </string-array>
</resources>
```

---

### 2) Diseñar la interfaz

**`app/src/main/res/layout/activity_main.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <!-- Spinner -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/label_categoria"
        android:textStyle="bold" />

    <Spinner
        android:id="@+id/spinnerCategory"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <!-- Fecha -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/label_fecha"
        android:textStyle="bold"
        android:layout_marginTop="12dp" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical">

        <TextView
            android:id="@+id/tvDate"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="YYYY-MM-DD"
            android:textSize="16sp" />

        <ImageButton
            android:id="@+id/ibPickDate"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:background="@android:color/transparent"
            android:contentDescription="@string/cd_pick_fecha"
            android:src="@drawable/ic_event_24" />
    </LinearLayout>

    <!-- Hora -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/label_hora"
        android:textStyle="bold"
        android:layout_marginTop="12dp" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical">

        <TextView
            android:id="@+id/tvTime"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="HH:mm"
            android:textSize="16sp" />

        <ImageButton
            android:id="@+id/ibPickTime"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:background="@android:color/transparent"
            android:contentDescription="@string/cd_pick_hora"
            android:src="@drawable/ic_access_time_24" />
    </LinearLayout>

    <!-- Descripción + acciones -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginTop="12dp">

        <EditText
            android:id="@+id/etDescription"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="@string/hint_descripcion"
            android:inputType="textCapSentences" />

        <ImageButton
            android:id="@+id/ibAdd"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:background="@android:color/transparent"
            android:contentDescription="@string/cd_agregar"
            android:src="@drawable/ic_add_24" />

        <ImageButton
            android:id="@+id/ibClear"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:background="@android:color/transparent"
            android:contentDescription="@string/cd_limpiar"
            android:src="@drawable/ic_delete_sweep_24" />
    </LinearLayout>

    <!-- ListView -->
    <ListView
        android:id="@+id/lvItems"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginTop="12dp"
        android:layout_weight="1" />

</LinearLayout>
```

---

### 3) Código Java (lógica de UI)

**`app/src/main/java/.../MainActivity.java`**

```java
// Código completo incluido en el ejercicio
public class MainActivity extends AppCompatActivity {
    private Spinner spinnerCategory;
    private TextView tvDate, tvTime;
    private EditText etDescription;
    private ImageButton ibPickDate, ibPickTime, ibAdd, ibClear;
    private ListView lvItems;

    private final ArrayList<String> items = new ArrayList<>();
    private ArrayAdapter<String> listAdapter;
    private Calendar selected; // fecha/hora seleccionadas


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        spinnerCategory = findViewById(R.id.spinnerCategory);
        tvDate = findViewById(R.id.tvDate);
        tvTime = findViewById(R.id.tvTime);
        etDescription = findViewById(R.id.etDescription);
        ibPickDate = findViewById(R.id.ibPickDate);
        ibPickTime = findViewById(R.id.ibPickTime);
        ibAdd = findViewById(R.id.ibAdd);
        ibClear = findViewById(R.id.ibClear);
        lvItems = findViewById(R.id.lvItems);

        ArrayAdapter<CharSequence> spinnerAdapter = ArrayAdapter.createFromResource(
                this, R.array.categorias, android.R.layout.simple_spinner_item);
        spinnerAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        spinnerCategory.setAdapter(spinnerAdapter);

    }
}

```

---

### 4) Ejecutar y probar

-  Corre la app en un **emulador** o **dispositivo físico**.
-  Flujo de prueba:
   1. Selecciona **categoría** en el **Spinner**.
   2. Toca **ImageButton de fecha** → elige una fecha.
   3. Toca **ImageButton de hora** → elige una hora.
   4. Escribe una **descripción** y toca **Agregar**.
   5. Verifica que aparece en la **ListView**.
   6. **Long-press** sobre un ítem para **eliminarlo**.
   7. Toca **Limpiar** para borrar todo.

---

## 🌿 Manejo de Git y GitHub (paso a paso)

Incluye GUI (Android Studio) y CLI (terminal).

---

## ✅ Checklist de verificación

-  [ ] El **Spinner** muestra categorías y puedes leer la selección.
-  [ ] Los **Pickers** actualizan correctamente `tvDate` y `tvTime`.
-  [ ] El **ImageButton Agregar** inserta elementos en la **ListView**.
-  [ ] **Long-press** en ListView elimina un elemento.
-  [ ] El **ImageButton Limpiar** borra toda la lista con confirmación.
-  [ ] Proyecto versionado en **Git** y subido a **GitHub** (rama
       `main` + PRs de features).
