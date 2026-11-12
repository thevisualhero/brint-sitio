# BRINT — sitio público (brint.com.mx)

Sitio comercial de **BRINT / ECOBRINT S.A. de C.V.** (Cancún, Quintana Roo). Objetivo: **web operativa capaz de generar y recibir leads.**

- **Staging:** https://thevisualhero.github.io/brint-sitio/ (GitHub Pages, con `noindex`). No es el hosting definitivo.
- **Producción:** `brint.com.mx` (dominio en GoDaddy; hosting por definir).
- Sitio estático: HTML/CSS/JS sin build ni dependencias de servidor. Se puede publicar en cualquier hosting estático.

## Arquitectura

```
brint.com.mx        Sitio público (este repo): presencia, captación de leads y entrada de soporte.
app.brint.com.mx    FUTURO, separado: lecturas de contadores, facturación, inventario,
                    tickets, portal de clientes. No se construye dentro del sitio público.
```

El sitio público **no** incluye login, dashboard, facturación, lecturas, inventario ni portal de cliente.

Dos flujos que no se mezclan:

| Usuario | CTA | Destino | Conversión |
|---|---|---|---|
| Prospecto | Cotizar una solución | `#cotizar` (formulario comercial) | `quote_submit` |
| Cliente actual | Necesito soporte / Reportar servicio | `#reportar-servicio` (formulario de soporte) | `support_request` (se mide aparte) |

## Configuración (antes de producción)

Todo se edita en un solo bloque al inicio del `<script>` de `index.html`: `BRINT_CONFIG`.

| Campo | Estado | Efecto si está vacío |
|---|---|---|
| `phone` | `PHONE_NUMBER_REQUIRED` | No se muestra ningún teléfono |
| `whatsapp` | `WHATSAPP_NUMBER_REQUIRED` | Los botones de WhatsApp muestran un aviso y remiten al correo |
| `emailSales` | `ventas@brint.com.mx` provisional: `PUBLIC_EMAIL_NEEDS_VERIFICATION` (hoy es alias/redirección; confirmar destinatario real) | — |
| `emailSupport` | Futuro alias `soporte@` | No se publica |
| `endpoints.quote` / `endpoints.support` | `FORM_BACKEND_REQUIRED` | Envío simulado (`demo: true`) y la interfaz lo indica |
| `endpointFormat` | `'json'` o `'text'` | — |
| `gtmId` | `GTM_CONTAINER_ID_REQUIRED` | Eventos sólo en `window.dataLayer`, sin scripts externos |

### Formularios

Con endpoint configurado, el sitio hace `POST` con el lead en JSON y **sólo muestra éxito si el servidor responde 2xx**; si falla, muestra error con el correo de respaldo. Incluye campo trampa anti-spam (`_gotcha`).

Opciones de destino (independientes del hosting): Formspree o similar (`json`), webhook de Make/Zapier hacia correo/CRM/Sheets (`json`), Google Apps Script → Google Sheets (`text`), o API propia. Recomendado: que ventas y soporte lleguen a destinos distintos (`ventas@` / `soporte@`).

Cada lead incluye: datos del formulario, `requested_service`, `equipos`, `lead_category`, `utm_*`, `gclid`/`fbclid`, `landing_page`, `referrer`, `page_url`.

## Medición

Eventos en `window.dataLayer` (listos para GTM / GA4):

| Evento | Uso |
|---|---|
| `quote_cta_click`, `support_cta_click` | Clics en Cotizar / Soporte (con `location`) |
| `phone_click` | **Conversión** `call` |
| `whatsapp_click` | **Conversión** `whatsapp` (con `status: number_pending` mientras no haya número) |
| `form_start` | Inicio de formulario (`form_type`) |
| `form_submit` (`form_type: quote`) | **Conversión** `quote_submit`, con `requested_service`, `equipment_count`, `source`, `medium`, `campaign`, `landing_page` |
| `form_submit` (`form_type: support`) | **Conversión** `support_request`, separada de las comerciales |
| `form_error`, `form_submit_error` | Diagnóstico |
| `rental_interest`, `managed_print_interest`, `service_interest`, `email_click` | Interés |

Conversiones comerciales: `quote_submit`, `call`, `whatsapp`. Soporte: `support_request`. Las UTM persisten durante la sesión y viajan con cada lead.

## Imágenes (temporales)

Stock de Pexels enlazado desde `images.pexels.com`, marcado `data-asset="IMAGE_PLACEHOLDER:*"`; `data-target` indica la foto BRINT que lo sustituye. Las fotos de la sesión BRINT van en `assets/images/` (ver su README). Para producción, servir las imágenes desde el propio hosting en WebP.

| Slot | Stock actual (Pexels ID) | Sustituir por |
|---|---|---|
| Hero | 37688149 | BRINT-4 |
| Servicios administrados | 9301887 | BRINT-1 |
| Soporte | 12437643 | BRINT-3 |
| Nosotros | 36946571 | BRINT-12 (+ BRINT-14 / BRINT-13) |
| Soluciones (4 categorías) | 8297569 · 7964539 · 3791246 · 11833899 | stock / generación |
| Soluciones · Flotas | diagrama SVG | se mantiene |

## Pendientes antes de publicar en brint.com.mx

1. Fotografías BRINT en `assets/images/` (WebP).
2. Datos que confirme Hugo: teléfono, WhatsApp, correo público, información comercial (sin inventar precios).
3. Destino real de formularios (`endpoints`).
4. Hosting y DNS en GoDaddy.
5. GTM / GA4 (`gtmId`) y marcar conversiones.
6. Quitar `<meta name="robots" content="noindex, nofollow">` (`REMOVE_NOINDEX_AT_LAUNCH`); confirmar canonical, `og:image`, `robots.txt` y `sitemap.xml`.
7. Aviso de privacidad (texto legal).
8. Revisión móvil final.

Marcadores internos en el HTML: `NEEDS_VERIFICATION`, `IMAGE_PLACEHOLDER`, `SLA_NEEDS_VERIFICATION`, `REPORTING_NEEDS_VERIFICATION`, `KYOCERA_RELATIONSHIP_NEEDS_VERIFICATION`, `CONSUMABLE_MANAGEMENT_NEEDS_VERIFICATION`, `PUBLIC_EMAIL_NEEDS_VERIFICATION`, `WHATSAPP_NUMBER_REQUIRED`, `PHONE_NUMBER_REQUIRED`, `FORM_BACKEND_REQUIRED`, `GTM_CONTAINER_ID_REQUIRED`, `CANONICAL_PLACEHOLDER`, `REMOVE_NOINDEX_AT_LAUNCH`.
