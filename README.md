# MotoRed Norte — Landing Oficial

Landing page de **MotoRed Norte**, la red de talleres y auxilio para moteros en La Libertad (Trujillo, Virú y Chao). Su objetivo es **promocionar la app y conseguir descargas del APK v1.0.0**, además de sumar usuarios al grupo Beta y talleres al directorio.

## Objetivo de conversión

1. **Descargar el APK v1.0.0 (23.5 MB)** — CTA principal (release `1.0.0` del repositorio `motorednorte_app`).
2. **Unirse al grupo Beta en WhatsApp** — CTA de invitación al grupo.
3. **Recomendar/Registrar un taller** — CTA vía Google Form (`forms.gle/65Fz75RxHq8QoujA9`).

Los tres clics están trackeados para medir la conversión (ver Analytics).

## Características de la App (basadas en `README_app.md`)

- **Directorio de talleres en tiempo real** — Listado en vivo con filtros por distrito, marca y especialidad.
- **Geolocalización GPS** — Captura de coordenadas para recomendar talleres y ubicar el más cercano.
- **Garage Virtual** — Gestión de la moto con alertas preventivas de SOAT vencido y mantenimiento próximo a 30 días.
- **Consulta rápida por WhatsApp y llamada** — Contacto directo al taller con un solo toque.

## Archivos

| Archivo         | Descripción                                   |
| --------------- | --------------------------------------------- |
| `index.html`    | Landing completa (HTML, CSS y JS en un solo archivo) |
| `logo1.png`     | Logo del header (círculo 44px)                |
| `logo2.png`     | Logo del hero (200px, usado también como imagen de OG) |
| `README_app.md` | Documentación técnica de la app (Flutter/Supabase) |
| `README.md`     | Este documento                               |

## Funcionalidades implementadas

- **CTA principal de descarga** del APK v1.0.0 con enlace directo al release de GitHub.
- **3 CTAs trackeados** (`click_download_apk`, `click_whatsapp_group`, `click_register_workshop`).
- **Sección de características** actualizada según la versión final de la app.
- **Logos integrados** en header y hero.
- **Open Graph / Twitter Cards** para previsualización al compartir en redes (URL e imagen basadas en GitHub Pages).
- **Responsive** (móvil/desktop).
- **Footer** con marca registrada, desarrollador y contacto.

## Analytics integrados

| Plataforma       | ID / Configuración                              | Propósito |
| ---------------- | ----------------------------------------------- | --------- |
| **GTM**          | `GTM-5J9T27ZF`                                  | Capa de tags y eventos |
| **GA4**          | Se configura dentro de GTM                       | Tráfico, audiencia y conversiones |
| **Clarity**      | Proyecto `y2gvsln2sb`                            | Mapas de calor, grabaciones ilimitadas |
| **Datadog RUM**  | `appId e5835661-…`, `service: motorednorte-landing`, `env: prod` | Rendimiento, errores JS y errores de red |

### Medición explícita del dominio de producción

Los tres servicios miden de forma explícita el dominio/URL de producción `https://guillermoqp.github.io/motorednorte_ld1/`:

- **GTM**: push de `dataLayer` con el evento `production_landing_view` y los parámetros `production_url`, `production_hostname`, `page_hostname`, `page_path`, `page_full_url` e `is_production_domain`.
- **Clarity**: custom tags `production_url`, `environment` (`production`) y `page_url` vía `clarity("set", …)`.
- **Datadog RUM**: contexto global `production_url`, `production_hostname`, `page_url` e `is_production_domain` vía `addRumGlobalContext`.

### Eventos enviados a `dataLayer` (GTM)

La función `trackEvent()` en `index.html` empuja el evento `custom_event` con estos parámetros:

| Parámetro           | Ejemplo                                 |
| ------------------- | --------------------------------------- |
| `event_name`        | `click_download_apk` / `click_whatsapp_group` / `click_register_workshop` |
| `event_category`    | `conversion` / `lead`                   |
| `event_label`       | `Descargar APK v1.0.0` / `Boton Grupo Whatsapp` / `Boton Registrar Taller` |

### Configuración pendiente en GTM (necesaria)

1. Crear un trigger de **Custom Event** llamado `custom_event`.
2. Crear una etiqueta GA4 que se dispare con ese trigger.
3. Crear variables de dataLayer (`event_name`, `event_category`, `event_label`) y pasarlas como parámetros de la etiqueta GA4.
4. Marcar `click_download_apk` y `click_whatsapp_group` como **conversiones** en GA4.
5. Crear un trigger **Custom Event** `production_landing_view` para reportar el tráfico del dominio de producción.

## Despliegue

- Publicado en **GitHub Pages**: `https://guillermoqp.github.io/motorednorte_ld1/`
- Dominio propio pendiente: `motorednorte.com` (actualizar `og:url`/`og:image` y canónico al activarlo).

## Pendientes

- [ ] Configurar GA4 dentro de GTM y marcar conversiones (ver arriba).
- [ ] Optimizar `logo1.png` y `logo2.png` (2.2 MB y 2.4 MB) a WebP/PNG comprimido para mejorar el LCP.
- [ ] Activar dominio propio y actualizar el Open Graph.
- [ ] Crear enlace de descarga para arquitectura `arm64-v8a` o `x86_64` según el dispositivo.
