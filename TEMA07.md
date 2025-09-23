# 📱 Tema 7. Transiciones

Ejercicio: Transiciones en Android (Escenas, Enter/Exit y patrones)

## Objetivos de aprendizaje

-  **Comprender** qué es una transición y cuándo usarla.\
-  **Identificar** el **generador de la estructura principal** de una
   transición (quién "dispara/coordina" la animación).\
-  **Reconocer** las **clases patrón** de transiciones (los "estilos"
   prefabricados).

## Parte A --- Transiciones con **Escenas** dentro de una sola actividad

### 1) Crear el proyecto

Sigue los pasos 1 al 4 del archivo [GIT_BASICO.md](GIT_BASICO.md) para crear y configurar tu proyecto Android.

Esta vez tienes que seleccionar **"Empty Activity"** y también debes eliminar el texto "Hello World"

1. **New Project → Empty Views Activity** (o _Empty Activity_).
2. Nombre: `Tema07`
3. Lenguaje: **Java**
4. Minimum SDK: **API 24** o superior.
5. Finish.

> ⚠️ **No olvides** agregar a `hasanyfa` como colaborador del proyecto.

---

-  **Minimum SDK**: API 21+ (Lollipop).\
-  Lenguaje: **Java**.\
-  Actividad vacía: `MainActivity`.

### 2) Layout base de la actividad (`activity_main.xml`)

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent" android:padding="16dp">

    <Button
        android:id="@+id/btnToggle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Cambiar escena" />

    <FrameLayout
        android:id="@+id/sceneRoot"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:background="#EEEEEE"
        android:layout_marginTop="12dp"/>
</LinearLayout>
```

### 3) **Escena inicial** (`initial_layout.xml`)

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:padding="24dp"
    android:layout_width="match_parent" android:layout_height="match_parent">

    <TextView
        android:id="@+id/tvTitle"
        android:text="Escena Inicial"
        android:textSize="22sp"
        android:layout_width="wrap_content" android:layout_height="wrap_content"/>

    <ImageView
        android:layout_marginTop="16dp"
        android:src="@android:drawable/ic_menu_gallery"
        android:layout_width="wrap_content" android:layout_height="wrap_content"/>
</LinearLayout>
```

### 4) **Escena final** (`final_layout.xml`)

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:padding="24dp"
    android:layout_width="match_parent" android:layout_height="match_parent">

    <TextView
        android:id="@+id/tvTitleFinal"
        android:text="Escena Final"
        android:textStyle="bold" android:textSize="22sp"
        android:layout_width="wrap_content" android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"/>

    <ImageView
        android:id="@+id/imgBig"
        android:src="@android:drawable/ic_menu_camera"
        android:layout_width="120dp" android:layout_height="120dp"
        android:layout_centerInParent="true"/>

    <TextView
        android:id="@+id/tvSubtitle"
        android:text="Nuevo contenido"
        android:layout_below="@id/imgBig"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="12dp"
        android:layout_width="wrap_content" android:layout_height="wrap_content"/>
</RelativeLayout>
```

### 5) Lógica en `MainActivity.java`

```java
public class MainActivity extends AppCompatActivity {
    private Scene sceneInitial;
    private Scene sceneFinal;
    private boolean showingInitial = true;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ViewGroup sceneRoot = findViewById(R.id.sceneRoot);
        sceneInitial = Scene.getSceneForLayout(sceneRoot, R.layout.initial_layout, this);
        sceneFinal   = Scene.getSceneForLayout(sceneRoot, R.layout.final_layout, this);
        sceneInitial.enter();

        Button btn = findViewById(R.id.btnToggle);
        btn.setOnClickListener(v -> toggleScene(sceneRoot));
    }

    private void toggleScene(ViewGroup sceneRoot) {
        Transition explode = new Explode();
        Transition slide   = new Slide(Gravity.BOTTOM);
        Transition fade    = new Fade();

        TransitionSet set = new TransitionSet()
                .addTransition(explode)
                .addTransition(slide)
                .addTransition(fade)
                .setDuration(600);

        if (showingInitial) {
            TransitionManager.go(sceneFinal, set);
        } else {
            TransitionManager.go(sceneInitial, set);
        }
        showingInitial = !showingInitial;
    }
}
```

## Parte B --- Transiciones **Enter/Exit** entre actividades

```java
// ActivityA.java
import android.app.ActivityOptions;
import android.content.Intent;
import android.os.Bundle;
import android.transition.Explode;
import androidx.appcompat.app.AppCompatActivity;

public class ActivityA extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_a);

        // Define la transición de salida de A
        getWindow().setExitTransition(new Explode());

        findViewById(R.id.btnOpenB).setOnClickListener(v -> {
            Intent intent = new Intent(this, ActivityB.class);
            startActivity(intent, ActivityOptions
                    .makeSceneTransitionAnimation(this)
                    .toBundle());
        });
    }
}
```

```java
// ActivityB.java
import android.os.Bundle;
import android.transition.Explode;
import androidx.appcompat.app.AppCompatActivity;

public class ActivityB extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // Define la transición de entrada de B
        getWindow().setEnterTransition(new Explode());
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b);
    }
}
```

## Parte C --- (Opcional) **Elementos compartidos**

```java
ActivityOptions options = ActivityOptions.makeSceneTransitionAnimation(
    this, imageViewA, "hero"
);
startActivity(intent, options.toBundle());
```

## Guía de práctica

1. Ejecuta la Parte A y prueba patrones individuales.
2. Ajusta `setDuration(...)`.
3. Implementa la Parte B y compara Explode vs Fade.
4. Añade shared element en la Parte C.

## Preguntas rápidas

1. ¿Qué diferencia hay entre una **escena** y una **transición**?\
2. Menciona dos **clases patrón**.\
3. ¿Qué clase coordina el cambio entre escenas?\
4. ¿Qué ventajas tiene un **shared element**?

## Rúbrica (10 pts)

-  (3) Cambio de escenas funcionando.\

-  (3) Usa al menos dos patrones.\

-  (2) Identifica que `TransitionManager` coordina.\

-  (2) Explica enter/exit vs escenas.

## Referencias

-  Android Developers. Animate layout changes using a transition.\
-  Android Developers. Start an activity using an animation.\
-  Material Design. Transitions.\
-  Develou. Usar Transiciones En Android Con Material Design.\
-  Valle, L. Material-Animations repo.
