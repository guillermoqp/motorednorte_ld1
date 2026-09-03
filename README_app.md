# AI Apaec Motos | Red Norte

Aplicación móvil (**Flutter**) para la zona norte del Perú (Trujillo, Virú, Chao) que reúne un **directorio geolocalizado de talleres de motos** y la **gestión de motocicletas** de cada usuario. Backend gestionado con **Supabase** (Auth, PostgreSQL y RLS).

## Stack tecnológico

- **Flutter / Dart** — UI multiplataforma y lógica de negocio.
- **Supabase Auth + GoTrue** — Autenticación por email/contraseña y recuperación de contraseña.
- **Supabase PostgreSQL + RLS** — Base de datos con control de acceso por filas y triggers de sincronización.
- **Deep Links** — Esquema `motored://reset-password` para el flujo de recuperación de contraseña.
- **geolocator / flutter_map** — Geolocalización del dispositivo y mapas.
- **url_launcher** — Apertura de WhatsApp y llamadas telefónicas.
- **provider** — Gestión de estado (ChangeNotifier).
- **image_picker** — Carga de fotos (avatar, moto, talleres).

## Funcionalidades implementadas

### Autenticación con Supabase
Login, registro y resumen de bienvenida post-login con alertas preventivas (SOAT y mantenimiento). El perfil del usuario se mantiene sincronizado con la tabla `profiles` mediante un **trigger de sincronización en PostgreSQL** (se crea/actualiza automáticamente al registrar al usuario).

### Recuperación de contraseña vía Deep Links
Flujo completo:
1. `AuthService.resetPassword(email)` envía el enlace con `redirectTo: 'motored://reset-password'`.
2. Al abrir el enlace, el listener de `AuthProvider` detecta `AuthChangeEvent.passwordRecovery` y navega a `UpdatePasswordScreen`.
3. El usuario define su nueva contraseña, se llama `updateUser(...)`, luego `signOut()` y se regresa al `LoginScreen`.

El enlace se captura en Android con un `<intent-filter>` para el esquema `motored` / host `reset-password`.

### Directorio de talleres / workshops
Listado en tiempo real desde Supabase con filtros por distrito, marca y especialidad. Detalle del taller con enlace a WhatsApp y llamada (exclusivo para usuarios autenticados). También es posible **recomendar un taller** con captura de coordenadas GPS y calificación previa (1 a 5).

### Gestión de motocicletas del usuario (user_motorcycles)
Garage virtual con la moto principal del usuario (marca, modelo, placa, foto), cálculo del próximo mantenimiento (intervalo configurable) y estado de vencimiento del SOAT, con alertas preventivas.

## Instalación

1. **Requisitos**: Flutter (SDK Dart ^3.13.0) y un proyecto Supabase con Auth habilitado.
2. **Configuración de Supabase**:
   - Crear las tablas `profiles`, `workshops` y `user_motorcycles` con RLS.
   - Configurar el trigger de sincronización de perfiles en `profiles` (upsert por `user.id` al registrarse).
   - En Auth → URL settings, permitir el redirect a `motored://reset-password`.
3. **Credenciales**: Instalar dependencias y ejecutar.

### Variables de entorno

> **Importante:** la app **no usa `.env`**. La URL del proyecto y la *publishable key* de Supabase están **hardcodeadas** como constantes en `lib/main.dart` (`_supabaseUrl` y `_supabaseAnonKey`). Si cambias de proyecto, edítalas ahí.

## Comandos

```bash
# Instalar dependencias (después de modificar pubspec.yaml)
flutter pub get

# Ejecutar la app en un dispositivo/emulador
flutter run

# Análisis estático (lint/typecheck)
flutter analyze

# Ejecutar pruebas (no requiere dispositivo ni red)
flutter test

# Limpieza pre-commit
flutter clean
dart format .
```