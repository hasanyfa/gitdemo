# 📱 Tema 10. Servicios en Android

## 🎯 ¿Qué vamos a aprender?

Imagínate que quieres que tu app reproduzca música mientras navegas por otras aplicaciones, o que descargue archivos en segundo plano. ¡Para eso necesitas **servicios**!

Los servicios son como trabajadores invisibles que siguen haciendo su trabajo aunque el usuario no esté viendo tu app directamente.

En este tema aprenderás a crear estos "trabajadores invisibles" paso a paso. 🚀

## 🔧 Los 3 tipos de servicios principales

### 1. 🚀 Servicios Started (Los independientes)

Son como robots que una vez que los enciendes, siguen trabajando hasta que les digas que paren.

**¿Cuándo usarlos?** Para descargas, reproducir música, o cualquier tarea que debe continuar aunque cambies de app.

-  Se inician con: `startService()`
-  Se detienen con: `stopSelf()` o `stopService()`

### 2. ⚡ Servicios Intent (Los organizados)

Son perfectos para tareas que necesitan hacerse una sola vez y de forma ordenada.

**¿Cuándo usarlos?** Para procesar datos, enviar emails, o subir fotos a la nube.

-  Son más fáciles de usar que los servicios normales
-  Se manejan automáticamente en hilos separados

### 3. 🔗 Servicios Bound (Los comunicativos)

Estos permiten que tu app "hable" directamente con el servicio mientras está funcionando.

**¿Cuándo usarlos?** Para mostrar el progreso de una descarga o controlar un reproductor de música.

-  Se conectan con: `bindService()`
-  Se desconectan con: `unbindService()`

## 👨‍💻 ¡Hora de practicar!

### 🚶‍♂️ Proyecto 1: Mi primer servicio con IntentService

Vamos a crear una app que muestre un mensaje en el log cuando presiones un botón.

#### Paso 1: Crear el proyecto

1. Abre Android Studio
2. Selecciona "Create New Project"
3. Elige "Empty Activity"
4. Nombra el proyecto como "MiPrimerServicio"
5. Haz clic en "Finish"

#### Paso 2: Diseñar la interfaz

Edita el archivo `activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <Button
        android:id="@+id/btnIniciarServicio"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Iniciar Servicio"
        android:onClick="initAction"/>

</LinearLayout>
```

#### Paso 3: Crear la clase MyIntentService

1. Haz clic derecho en la carpeta de tu paquete Java
2. Selecciona "New" > "Java Class"
3. Nombra la clase "MyIntentService"
4. Agrega este código:

```java
import android.app.IntentService;
import android.content.Intent;
import android.util.Log;

public class MyIntentService extends IntentService {

    public MyIntentService() {
        super("MyIntentService");
    }

    @Override
    protected void onHandleIntent(Intent intent) {
        Log.d("MiServicio", "El servicio está funcionando!");
        // Simular trabajo por 3 segundos
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        Log.d("MiServicio", "El servicio terminó su trabajo");
    }
}
```

#### Paso 4: Registrar el servicio en AndroidManifest.xml

Agrega esta línea dentro del tag `<application>`:

```xml
<service android:name=".MyIntentService" />
```

#### Paso 5: Conectar el botón en MainActivity.java

Agrega este método en `MainActivity.java`:

```java
import android.content.Intent;

public void initAction(View view) {
    Intent intent = new Intent(this, MyIntentService.class);
    startService(intent);
    Log.d("MainActivity", "Servicio iniciado desde MainActivity");
}
```

#### Paso 6: Probar la app

1. Ejecuta la aplicación
2. Abre el Logcat (View > Tool Windows > Logcat)
3. Presiona el botón "Iniciar Servicio"
4. ¡Observa los mensajes en el Logcat!

---

### 🏃‍♂️ Proyecto 2: Servicio con cronómetro

Ahora crearemos un servicio que cuenta tiempo usando la clase `Service`.

#### Paso 1: Crear nuevo proyecto

1. Crea un nuevo proyecto llamado "ServiceExample2"
2. Usa "Empty Activity"

#### Paso 2: Diseñar interfaz

En `activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <Button
        android:id="@+id/btnIniciarCronometro"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Iniciar Cronómetro"
        android:onClick="initAction"/>

</LinearLayout>
```

#### Paso 3: Crear clase MyService

Crea una nueva clase "MyService":

```java
import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.util.Log;

public class MyService extends Service {
    private Thread cronometroThread;
    private boolean isRunning = false;
    private int contador = 0;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.d("MyService", "Servicio iniciado");

        if (!isRunning) {
            isRunning = true;
            cronometroThread = new Thread(new Runnable() {
                @Override
                public void run() {
                    while (isRunning) {
                        try {
                            Thread.sleep(1000); // Esperar 1 segundo
                            contador++;
                            Log.d("MyService", "Cronómetro: " + contador + " segundos");
                        } catch (InterruptedException e) {
                            Thread.currentThread().interrupt();
                            break;
                        }
                    }
                }
            });
            cronometroThread.start();
        }

        return START_STICKY; // El servicio se reinicia si es terminado
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        isRunning = false;
        if (cronometroThread != null) {
            cronometroThread.interrupt();
        }
        Log.d("MyService", "Servicio detenido en: " + contador + " segundos");
    }
}
```

#### Paso 4: Registrar en AndroidManifest.xml

```xml
<service android:name=".MyService" />
```

#### Paso 5: Actualizar MainActivity.java

```java
import android.content.Intent;
import android.view.View;

public void initAction(View view) {
    Intent intent = new Intent(this, MyService.class);
    startService(intent);
    Log.d("MainActivity", "Cronómetro iniciado");
}

@Override
protected void onDestroy() {
    super.onDestroy();
    // Detener el servicio cuando la actividad se destruye
    Intent intent = new Intent(this, MyService.class);
    stopService(intent);
}
```

#### Paso 6: Probar

1. Ejecuta la app
2. Presiona el botón
3. Ve al Logcat y observa el cronómetro funcionando
4. Incluso si sales de la app, ¡el cronómetro sigue!

---

### 🤝 Proyecto 3: Servicio Local con comunicación bidireccional

Este proyecto muestra la hora actual usando un servicio que se comunica con la actividad.

#### Paso 1: Crear proyecto

1. Nuevo proyecto llamado "LocalService"
2. "Empty Activity"

#### Paso 2: Diseñar interfaz

En `activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <TextView
        android:id="@+id/tvTiempo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hora: --:--:--"
        android:textSize="24sp"
        android:layout_marginBottom="20dp"/>

    <Button
        android:id="@+id/btnObtenerHora"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Obtener Hora Actual"
        android:onClick="initAction"/>

</LinearLayout>
```

#### Paso 3: Crear MyService con Binder

```java
import android.app.Service;
import android.content.Intent;
import android.os.Binder;
import android.os.IBinder;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class MyService extends Service {
    private final IBinder myBinder = new MyLocalBinder();

    public class MyLocalBinder extends Binder {
        public MyService getService() {
            return MyService.this;
        }
    }

    @Override
    public IBinder onBind(Intent intent) {
        return myBinder;
    }

    public String getCurrentTime() {
        SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss", Locale.getDefault());
        return sdf.format(new Date());
    }
}
```

#### Paso 4: Actualizar MainActivity.java

```java
import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.IBinder;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private MyService myService;
    private boolean serviceBound = false;
    private TextView tvTiempo;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        tvTiempo = findViewById(R.id.tvTiempo);
    }

    private ServiceConnection connection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            MyService.MyLocalBinder binder = (MyService.MyLocalBinder) service;
            myService = binder.getService();
            serviceBound = true;
        }

        @Override
        public void onServiceDisconnected(ComponentName name) {
            serviceBound = false;
        }
    };

    @Override
    protected void onStart() {
        super.onStart();
        Intent intent = new Intent(this, MyService.class);
        bindService(intent, connection, BIND_AUTO_CREATE);
    }

    @Override
    protected void onStop() {
        super.onStop();
        if (serviceBound) {
            unbindService(connection);
            serviceBound = false;
        }
    }

    public void initAction(View view) {
        if (serviceBound) {
            String horaActual = myService.getCurrentTime();
            tvTiempo.setText("Hora: " + horaActual);
        }
    }
}
```

#### Paso 5: Registrar en AndroidManifest.xml

```xml
<service android:name=".MyService" />
```

#### Paso 6: Probar la aplicación

1. Ejecuta la app
2. Presiona "Obtener Hora Actual"
3. ¡La hora se actualiza en pantalla!
4. El servicio se conecta automáticamente cuando abres la app

¡Ahora tienes tres ejemplos completos de servicios funcionando! 🎉

## 💡 ¿Por qué son importantes los servicios?

Imagínate que haces una app para transferir archivos, pero usas hilos normales en lugar de servicios. ¿Qué pasaría?

❌ **Sin servicios:** Si el usuario cambia de app o la cierra, ¡la transferencia se detiene!
✅ **Con servicios:** La transferencia continúa aunque el usuario haga otras cosas.

**Recuerda:** Una app que funciona mal = usuarios molestos = malas calificaciones. ¡No queremos eso!

## ✅ Checkpoint - ¿Ya entendiste?

Antes de continuar, asegúrate de poder:

-  [ ] 🎯 Explicar qué es un servicio con tus propias palabras
-  [ ] 🔧 Decidir cuándo usar cada tipo de servicio
-  [ ] 👨‍💻 Crear un servicio básico desde cero
-  [ ] 🔗 Conectar un servicio con tu actividad principal

## 📚 Para saber más

-  **Smyth, N.** (2021). _Android Studio Arctic Fox Essentials - Java Edition_
-  **Miranda, M.** (2019). _Android / Servicios_ - [Ver artículo](https://tinchicus.com/2019/02/04/android-servicios/)

---

### 📖 Glosario rápido

**🤖 Service:** Un "trabajador invisible" que sigue funcionando aunque no veas la app

**🔗 IBinder:** El "teléfono" que permite que tu app hable con el servicio

**📱 IntentService:** Un servicio "automático" que se maneja solo y es perfecto para principiantes
