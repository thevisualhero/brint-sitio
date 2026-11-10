# BRINT — Sitio v1 (prototipo navegable)

Primera versión navegable del sitio comercial de **BRINT / ECOBRINT S.A. de C.V.** (Cancún, Quintana Roo).

- Página única en HTML/CSS/JS, sin dependencias de build.
- Vistas por hash: inicio, `#cotizar`, `#reportar-servicio`, `#aviso-de-privacidad`.
- Formularios con validación y estado de envío **sin backend** (no envían datos a ningún servidor).
- Eventos de analítica en `window.dataLayer` y persistencia de UTM por sesión.

## Estructura

```
index.html                 Sitio completo
assets/brint-logo-red.png  Logo (extraído de la presentación; reemplazar por SVG original)
assets/brint-logo-white.png
```

## FORM_BACKEND_REQUIRED

Los formularios de Cotizar y Reportar servicio validan y muestran un estado de éxito **simulado** (`DEMO_MODE = true` en `index.html`; el payload incluye `demo: true` y la interfaz indica que no se envió). Antes de producción hay que definir destino: email, CRM, Google Sheets, API, Formspree (o similar) o backend propio, y cambiar `DEMO_MODE` a `false`.

## Pendientes antes de producción

El HTML contiene comentarios internos que marcan contenido por confirmar:
`NEEDS_VERIFICATION`, `IMAGE_PLACEHOLDER`, `SLA_NEEDS_VERIFICATION`, `REPORTING_NEEDS_VERIFICATION`,
`KYOCERA_RELATIONSHIP_NEEDS_VERIFICATION`, `CONSUMABLE_MANAGEMENT_NEEDS_VERIFICATION`, `FORM_BACKEND_REQUIRED`, `WHATSAPP_NUMBER_REQUIRED`, `CANONICAL_PLACEHOLDER`.

Las ilustraciones son temporales y se sustituirán por fotografía real de BRINT.

## Imágenes (temporales)

Las fotografías actuales son **stock de Pexels** (licencia Pexels: uso libre, sin atribución obligatoria), enlazadas desde `images.pexels.com` con recorte y tamaño responsivo. Están marcadas en el HTML con `data-asset="IMAGE_PLACEHOLDER:*"` y `data-target` indica la foto de la sesión BRINT que debe sustituirlas.

| Slot | Stock actual (Pexels ID) | Sustituir por |
|---|---|---|
| Hero | 37688149 | BRINT-4 |
| Servicios administrados | 9301887 | BRINT-1 |
| Soporte | 12437643 | BRINT-3 |
| Nosotros | 36946571 | BRINT-12 (+ BRINT-14 / BRINT-13 como detalle) |
| Soluciones · Oficina compacta | 8297569 | stock / generación (sin foto BRINT adecuada) |
| Soluciones · Departamental | 7964539 | stock / generación |
| Soluciones · Alto volumen | 3791246 | stock / generación |
| Soluciones · Color | 11833899 | stock / generación |
| Soluciones · Flotas | diagrama SVG | se mantiene |

Al subir las fotos BRINT a `assets/images/`, reemplazar el `src`/`srcset` de cada `<img>` por las versiones WebP optimizadas.
