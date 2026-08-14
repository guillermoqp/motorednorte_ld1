# MotoRed Norte — Landing de Pre-Lanzamiento

Landing page de espera para **MotoRed Norte**, la red de talleres y auxilio para moteros en La Libertad (Trujillo, Virú y Chao). Su objetivo es **generar usuarios e interesados** antes del lanzamiento de la app (Beta APK) el **1 de octubre de 2026**.

## Objetivo de conversión

1. **Unirse al grupo Beta en WhatsApp** — CTA principal (link de invitación al grupo).
2. **Recomendar/Registrar un taller** — CTA secundario vía Google Form (`forms.gle/65Fz75RxHq8QoujA9`).

Ambos clics están trackeados para medir la conversión (ver Analytics).

## Archivos

| Archivo      | Descripción                                   |
| ------------ | --------------------------------------------- |
| `index.html` | Landing completa (HTML, CSS y JS en un solo archivo) |
| `logo1.png`  | Logo del header (círculo 44px)                |
| `logo2.png`  | Logo del hero (200px, usado también como imagen de OG) |
| `README.md`  | Este documento                               |

## Funcionalidades implementadas

- **Contador regresivo** al lanzamiento: 1 oct 2026, 20:00 (hora local del navegador).
- **2 CTAs trackeados** (`click_whatsapp_group`, `click_register_workshop`).
- **Logos integrados** en header y hero.
- **Open Graph / Twitter Cards** para previsualización al compartir en redes (URL e imagen basadas en GitHub Pages).
- **Responsive** (móvil/desktop).

## Analytics integrados

| Plataforma       | ID / Configuración                              | Propósito |
| ---------------- | ----------------------------------------------- | --------- |
| **GTM**          | `GTM-5J9T27ZF`                                  | Capa de tags y eventos |
| **GA4**          | Se configura dentro de GTM                       | Tráfico, audiencia y conversiones |
| **Clarity**      | Proyecto `y2gvsln2sb`                            | Mapas de calor, grabaciones ilimitadas |
| **Datadog RUM**  | `appId e5835661-…`, `service: motorednorte-landing`, `env: prod` | Rendimiento, errores JS y errores de red |

### Eventos enviados a `dataLayer` (GTM)

La función `trackEvent()` en `index.html` empuja el evento `custom_event` con estos parámetros:

| Parámetro           | Ejemplo                               |
| ------------------- | ------------------------------------- |
| `event_name`        | `click_whatsapp_group`                |
| `event_category`    | `conversion` / `lead`                 |
| `event_label`       | `Boton Grupo Whatsapp` / `Boton Registrar Taller` |

### Configuración pendiente en GTM (necesaria)

1. Crear un trigger de **Custom Event** llamado `custom_event`.
2. Crear una etiqueta GA4 que se dispare con ese trigger.
3. Crear variables de dataLayer (`event_name`, `event_category`, `event_label`) y pasarlas como parámetros de la etiqueta GA4.
4. Marcar `click_whatsapp_group` como **conversión** en GA4.

## Despliegue

- Publicado en **GitHub Pages**: `https://guillermoqp.github.io/motorednorte_ld1/`
- Dominio propio pendiente: `motorednorte.com` (actualizar `og:url`/`og:image` y canónico al activarlo).

## Pendientes

- [ ] Configurar GA4 dentro de GTM y marcar conversiones (ver arriba).
- [ ] Optimizar `logo1.png` y `logo2.png` (2.2 MB y 2.4 MB) a WebP/PNG comprimido para mejorar el LCP.
- [ ] Activar dominio propio y actualizar el Open Graph.
- [ ] Confirmar fecha exacta de lanzamiento si cambia (contador en `index.html`).
