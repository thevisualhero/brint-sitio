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

## Pendientes antes de producción

El HTML contiene comentarios internos que marcan contenido por confirmar:
`NEEDS_VERIFICATION`, `IMAGE_PLACEHOLDER`, `SLA_NEEDS_VERIFICATION`, `REPORTING_NEEDS_VERIFICATION`,
`KYOCERA_RELATIONSHIP_NEEDS_VERIFICATION`, `WHATSAPP_NUMBER_REQUIRED`, `CANONICAL_PLACEHOLDER`.

Las ilustraciones son temporales y se sustituirán por fotografía real de BRINT.
