# 🚀 ACTIVIDAD 7 - PASO A PASO

## 📋 Checklist de la Actividad

### ✅ Fase 1: Configuración inicial del repositorio

-  [ ] **Paso 1.1:** Crear nuevo repositorio

-  [ ] **Paso 1.2:** Agregar colaborador

   ```bash
   # En GitHub: Settings > Manage access > Invite a collaborator
   # Usuario: hasanyfa
   ```

-  [ ] **Paso 1.3:** Inicializar proyecto Android
   ```
   📱 Abrir Android Studio
   📁 New Project > Empty Views Activity
   📝 Name: Actividad7
   🎯 Language: Java
   📱 Minimum SDK: API 21+
   ```

### ✅ Fase 2: Configuración del proyecto

-  [ ] **Paso 2.1:** Crear paleta de colores

   ```xml
   <!-- Archivo: app/src/main/res/values/colors.xml -->
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <!-- 🎨 Paleta de colores principales (mínimo 5) -->
       <color name="primary_color">#FF6B35</color>        <!-- Naranja vibrante -->
       <color name="secondary_color">#F7931E</color>      <!-- Naranja dorado -->
       <color name="tertiary_color">#FFD23F</color>       <!-- Amarillo brillante -->
       <color name="accent_color">#4ECDC4</color>         <!-- Turquesa -->
       <color name="complementary_color">#45B7D1</color>  <!-- Azul cielo -->

       <!-- 🎨 Colores adicionales de soporte -->
       <color name="background_color">#FFFFFF</color>     <!-- Blanco -->
       <color name="surface_color">#F8F9FA</color>        <!-- Gris muy claro -->
       <color name="text_primary">#2C3E50</color>         <!-- Gris oscuro -->
       <color name="text_secondary">#7F8C8D</color>       <!-- Gris medio -->
       <color name="success_color">#27AE60</color>        <!-- Verde éxito -->
       <color name="warning_color">#F39C12</color>        <!-- Naranja advertencia -->
       <color name="error_color">#E74C3C</color>          <!-- Rojo error -->
   </resources>
   ```

-  [ ] **Paso 2.2:** Agregar fuente personalizada

   ```
   📂 Crear carpeta: app/src/main/res/font/
   📥 Descargar fuente de Google Fonts (ej: roboto_medium.ttf)
   📁 Colocar archivo en carpeta font/
   ```

-  [ ] **Paso 2.3:** Configurar tema

   ```xml
   <!-- Archivo: app/src/main/res/values/themes.xml -->
   <resources>
       <style name="Theme.Actividad7" parent="Theme.Material3.DayNight">
           <!-- 🎨 Colores principales del tema -->
           <item name="colorPrimary">@color/primary_color</item>
           <item name="colorSecondary">@color/secondary_color</item>
           <item name="colorTertiary">@color/tertiary_color</item>
           <item name="colorSurface">@color/surface_color</item>
           <item name="colorBackground">@color/background_color</item>

           <!-- 🎨 Colores de acento y complementarios -->
           <item name="colorAccent">@color/accent_color</item>
           <item name="colorError">@color/error_color</item>

           <!-- 🔤 Tipografía personalizada -->
           <item name="android:fontFamily">@font/roboto_medium</item>
           <item name="fontFamily">@font/roboto_medium</item>

           <!-- 📝 Colores de texto -->
           <item name="android:textColorPrimary">@color/text_primary</item>
           <item name="android:textColorSecondary">@color/text_secondary</item>
       </style>
   </resources>
   ```

### ✅ Fase 3: Pull Request y Merge

-  [ ] **Paso 3.1:** Commit inicial

   ```bash
   git add .
   git commit -m "🎨 Agregar paleta de colores, fuente y tema personalizado"
   git push origin main
   ```

-  [ ] **Paso 3.2:** Crear Pull Request

   ```bash
   # En GitHub:
   # 1. Go to Pull requests
   # 2. Click "New pull request"
   # 3. Add hasanyfa as reviewer
   # 4. Wait for approval
   ```

-  [ ] **Paso 3.3:** Realizar Merge
   ```bash
   # Después de la aprobación:
   # 1. Click "Merge pull request"
   # 2. Confirm merge
   ```

### ✅ Fase 4: Sincronización local

-  [ ] **Paso 4.1:** Cambiar a rama main

   ```bash
   git checkout main
   ```

-  [ ] **Paso 4.2:** Verificar cambios remotos

   ```bash
   git fetch
   ```

-  [ ] **Paso 4.3:** Descargar cambios

   ```bash
   git pull origin main
   ```

-  [ ] **Paso 4.4:** Crear rama desarrollo
   ```bash
   git checkout -b desarrollo
   ```

### ✅ Fase 5: Documentación README

-  [ ] **Paso 5.1:** Crear archivo README.md

   ```bash
   touch README.md
   ```

-  [ ] **Paso 5.2:** Agregar contenido README

   ```markdown
   # 📱 Actividad 7 - Intents y Comunicación entre Apps

   ## ❓ Preguntas y Respuestas

   ### 🔗 Pregunta 1: Aprovechamiento de funcionalidades

   **¿Cómo se pueden aprovechar las funcionalidades de otras aplicaciones para mejorar la experiencia del usuario en una aplicación propia?**

   **Respuesta:** [Tu respuesta aquí]

   ### 🚀 Pregunta 2: Intents para abrir aplicaciones

   **¿Cómo se pueden utilizar Intents para abrir otras aplicaciones de forma segura y eficiente?**

   **Respuesta:** [Tu respuesta aquí]

   ### 🔄 Pregunta 3: Compartir datos entre aplicaciones

   **¿Cómo se pueden utilizar Intents para compartir datos y acciones entre diferentes aplicaciones?**

   **Respuesta:** [Tu respuesta aquí]

   ### 💭 Reflexión Personal

   **Reflexión del tema (mínimo 50 palabras):**

   [Tu reflexión personal aquí]

   ## 📸 Capturas de Pantalla

   [Agregar capturas de pantalla de la aplicación]
   ```

### ✅ Fase 6: Desarrollo de la aplicación

-  [ ] **Paso 6.1:** Diseñar layout principal

   ```xml
   <!-- activity_main.xml -->
   <LinearLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical"
       android:padding="16dp">

       <TextView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="🌍 Explorador de Productos"
           android:textSize="24sp"
           android:textStyle="bold" />


       <androidx.recyclerview.widget.RecyclerView
           android:id="@+id/recyclerProducts"
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:layout_marginTop="16dp" />

   </LinearLayout>
   ```

-  [ ] **Paso 6.2:** Crear modelo de datos

   ```java
   // Product.java
   public class Product {
       private String name;
       private String description;
       private String imageUrl;
       private String webUrl;

       // Constructor, getters y setters
   }
   ```

-  [ ] **Paso 6.3:** Implementar RecyclerView Adapter

   ```java
   // ProductAdapter.java
   public class ProductAdapter extends RecyclerView.Adapter<ProductAdapter.ViewHolder> {
       // Implementar adapter para mostrar productos
   }
   ```

-  [ ] **Paso 6.4:** Configurar datos de productos

   ```java
   // En MainActivity.java
   private void setupProducts() {
       List<Product> products = Arrays.asList(
           new Product("🎧 Auriculares Premium", "Sonido de alta calidad", "url_imagen", "https://example.com/headphones"),
           new Product("📱 Smartphone", "Última tecnología", "url_imagen", "https://example.com/phone"),
           new Product("💻 Laptop Gaming", "Para gamers profesionales", "url_imagen", "https://example.com/laptop"),
           new Product("⌚ Smartwatch", "Fitness y salud", "url_imagen", "https://example.com/watch"),
           new Product("📷 Cámara Digital", "Fotografía profesional", "url_imagen", "https://example.com/camera")
       );
   }
   ```

-  [ ] **Paso 6.5:** Implementar Intent para abrir navegador
   ```java
   private void openWebUrl(String url) {
       Intent intent = new Intent(Intent.ACTION_VIEW);
       intent.setData(Uri.parse(url));
       startActivity(intent);
   }
   ```

### ✅ Fase 7: Testing y capturas

-  [ ] **Paso 7.1:** Probar la aplicación

   ```
   📱 Run app
   🧪 Test TableView/RecyclerView
   🌐 Test web links
   ⬅️ Test back navigation
   ```

-  [ ] **Paso 7.2:** Tomar capturas de pantalla
   ```
   📸 Captura de pantalla principal
   📸 Captura de producto seleccionado
   📸 Captura de navegador abierto
   📸 Captura de regreso a la app
   ```

### ✅ Fase 8: Entrega final

-  [ ] **Paso 8.1:** Commit final

   ```bash
   git add .
   git commit -m "🛍️ Implementar aplicación de productos con Intents"
   git push origin desarrollo
   ```

-  [ ] **Paso 8.2:** Crear Pull Request final

   ```bash
   # En GitHub:
   # 1. New pull request from desarrollo to main
   # 2. Add screenshots to PR description
   # 3. Add hasanyfa as reviewer
   ```

-  [ ] **Paso 8.3:** Actualizar README con capturas

   ```markdown
   ## 📸 Capturas de Pantalla

   ### Vista Principal

   ![Vista Principal](screenshots/main_view.png)

   ### Navegador Web

   ![Navegador](screenshots/web_view.png)
   ```

## 🎯 Criterios de Evaluación

| Criterio                           | Puntos  | ✅  |
| ---------------------------------- | ------- | --- |
| Configuración de colores y fuentes | 20      | [ ] |
| Implementación de Intents          | 25      | [ ] |
| Diseño de interfaz                 | 20      | [ ] |
| Funcionalidad completa             | 20      | [ ] |
| Documentación y capturas           | 15      | [ ] |
| **Total**                          | **100** | [ ] |

## 📝 Notas importantes

-  ✅ Asegúrate de que todos los enlaces web funcionen
-  📱 Testa la navegación entre apps
-  🔒 Verifica que los permisos estén correctos
-  📸 Las capturas de pantalla son obligatorias
-  👥 No olvides agregar a hasanyfa como colaborador y revisor

---

**🏁 ¡Actividad completada! Revisa que todos los checkboxes estén marcados antes de entregar.**
