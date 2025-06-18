# UnChazApp2

## Descripción General
UnChazApp2 es una aplicación móvil Android que permite a los usuarios registrar, buscar, calificar y recomendar negocios locales. La app utiliza Firebase como backend para la gestión de usuarios, negocios y calificaciones, e integra un sistema de recomendaciones basado en Python y machine learning, que se comunica mediante una API REST.

## Estructura del Proyecto

```
UnChazApp2/
├── app/                  # Módulo principal de la app Android
│   ├── src/main/java/com/example/unchazapp/
│   │   ├── acces/        # Acceso a datos (DAO, callbacks)
│   │   ├── adapter/      # Adaptadores de UI
│   │   ├── model/        # Modelos de datos (Usuario, Negocio, Producto, etc.)
│   │   ├── services/     # Lógica de negocio y conexión con Python
│   │   ├── CategoriasNegocios/ # Clases relacionadas a categorías
│   │   ├── ...           # Actividades principales (pantallas)
│   ├── res/              # Recursos gráficos y layouts
│   ├── AndroidManifest.xml
│   └── build.gradle.kts  # Configuración del módulo Android
├── app2.py               # Backend Python (API Flask para recomendaciones)
├── prueba3.py            # Lógica de recomendación y actualización de datos
├── datos.csv             # Datos de calificaciones y negocios para ML
├── tuto.json             # Credenciales de Firebase para Python
├── build.gradle.kts      # Configuración global de Gradle
└── ...
```

## Principales Funcionalidades
- **Registro e ingreso de usuarios**
- **Gestión de negocios**: registro, listado, perfil, actualización y eliminación
- **Calificación de negocios**
- **Recomendaciones personalizadas**
- **Integración con Firebase (Realtime Database y Auth)**
- **Backend Python para recomendaciones ML**

## Arquitectura
### Android
- **Actividades**: Cada pantalla principal es una Activity (ej: `MainActivity`, `Registro`, `NegocioRegistro`, `INICIO`, etc.)
- **DAO genérico**: `GenericDAO<T>` permite operaciones CRUD sobre cualquier entidad en Firebase.
- **Modelos**: Clases Java que representan entidades como `Usuario`, `Negocio`, `Producto`, `Calificacion`, etc.
- **Adaptadores**: Para mostrar listas de negocios y productos en la UI.
- **Servicios**: Comunicación con el backend Python mediante HTTP (`ObtenerRecomendacionesTask`).

### Backend Python
- **Flask API** (`app2.py`): expone el endpoint `/recomendar` para recibir solicitudes de recomendación desde la app Android.
- **Machine Learning** (`prueba3.py`): utiliza pandas y scikit-learn para procesar datos y generar recomendaciones personalizadas.
- **Actualización de datos**: sincroniza datos de Firebase a un CSV local para alimentar el sistema de recomendaciones.

## Modelos de Datos
- **Usuario**: userName, email, documento, password
- **Negocio**: nombreNegocio, categoriaNegocio, tipoDeNegocio, descripcionNegocio, keyUsuario, catalogo, imagen
- **Producto**: nombreProducto, precioProducto, descripcionProducto
- **Calificacion**: calificacion, keyNegocio, keyUser, categoria
- **Catalogo**: nombre, productos (lista de Producto)
- **Categoria**: ALIMENTACION, PAPELERIA, ACCESORIOS, MAQUILLAJE, ROPA, MANUALIDADES, OBJETOS_ENTRETENIMIENTO
- **TipoDeNegocio**: ESTATICO, MOVIL

## Integración Android ↔ Python
- La app Android envía el ID del usuario al endpoint `/recomendar` del backend Python.
- El backend responde con una lista de IDs de negocios recomendados, que la app muestra al usuario.
- El backend actualiza periódicamente los datos desde Firebase para mantener el sistema de recomendaciones actualizado.

## Configuración y Ejecución
### Requisitos
- Android Studio (API 30+)
- Python 3.8+
- Paquetes Python: flask, pandas, scikit-learn, firebase-admin

### Pasos para correr el backend Python
1. Instala las dependencias:
   ```bash
   pip install flask pandas scikit-learn firebase-admin
   ```
2. Coloca el archivo `tuto.json` (credenciales de Firebase) en la raíz del proyecto.
3. Ejecuta el backend:
   ```bash
   python app2.py
   ```

### Pasos para correr la app Android
1. Abre el proyecto en Android Studio.
2. Configura el archivo `google-services.json` en `app/`.
3. Compila y ejecuta la app en un emulador o dispositivo físico.

## Notas de Seguridad
- **No compartas el archivo `tuto.json` ni `google-services.json` públicamente.**
- Las credenciales de Firebase son sensibles y deben mantenerse privadas.

## Créditos
Desarrollado por estudiantes de la Universidad Nacional de Colombia.

---

¿Tienes dudas o sugerencias? ¡Contribuye o abre un issue! 