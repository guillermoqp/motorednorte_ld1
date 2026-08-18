# AI Apaec Motos | Red Norte
Directorio geolocalizado y red de soporte para moteros en la Zona Norte del Perú (Trujillo, Virú, Chao).

## Tech Stack
- **Flutter / Dart** — UI multiplataforma y lógica de negocio.
- **Supabase** — Autenticación (Auth), base de datos (Postgres) y control de acceso por filas (RLS).
- **geolocator** — Captura de coordenadas GPS del dispositivo.
- **url_launcher** — Apertura de WhatsApp y llamadas telefónicas.

## Funcionalidades Estables Construidas

### Directorio de Talleres
Listado en tiempo real desde Supabase con filtros por distrito, marca y especialidad.

### Detalle del Taller
Información del taller, enlace a WhatsApp y llamada telefónica (exclusivo para usuarios autenticados). Los usuarios no autenticados ven un banner invitándolos a iniciar sesión.

### Recomendar Taller
Formulario con captura de coordenadas GPS (botón "Obtener mi ubicación actual") y estrellas de calificación previa (1 a 5).

### Garage Virtual
Gestión de la moto principal, cálculo del próximo mantenimiento (intervalo configurable por el usuario) y estado de vencimiento del SOAT.

### Autenticación
Login, registro y modal de resumen de bienvenida post-login con alertas preventivas (SOAT y mantenimiento).

## Instalación y Comandos Útiles

```bash
# Instalar dependencias
flutter pub get

# Ejecutar la app en un dispositivo/emulador
flutter run

# Limpieza pre-commit
flutter clean
dart format .
```
