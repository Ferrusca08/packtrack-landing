# PackTrack — Sitio web (landing)

Landing page de marketing para **PackTrack**, el sistema de recepción de paquetes para edificios residenciales.

## Contenido del repo

| Archivo | Qué es |
|---|---|
| `index.html` | Landing page completa — interactiva, animada y responsiva. Sin build, sin dependencias (un solo archivo autocontenido). |
| `PRICING.md` | Propuesta de precios: análisis de costos de infraestructura + modelo de cobro por residente activo + planes y ejemplos. |

## Características de la landing

- **Conversión primero:** hero con propuesta de valor clara, CTAs visibles, planes de precio, FAQ y CTA final.
- **Animaciones:** reveal por scroll (IntersectionObserver), contadores animados, mockup flotante del producto, acordeón de FAQ, navegación con scroll suave.
- **Responsiva:** menú hamburguesa en móvil, grids que se reacomodan, breakpoints en 960px y 680px.
- **Rápida:** HTML/CSS/JS puro, una sola petición (más la fuente Inter de Google Fonts).

## Cómo verla

Abre `index.html` en cualquier navegador, o sírvela:

```bash
python3 -m http.server 8000
# luego abre http://localhost:8000
```

## Despliegue

Es estática — se puede publicar en **GitHub Pages**, Netlify, Vercel o cualquier hosting estático sin configuración.

## Pendientes / personalizar antes de publicar

- Reemplazar el correo de contacto `hola@packtrack.mx` por el real.
- Conectar un formulario real o herramienta de agenda (Calendly, etc.) en los CTA.
- Agregar capturas/imágenes reales del producto (hoy el hero usa un mockup en CSS).
- Aviso de privacidad y términos (links en el footer son placeholders).
- Ajustar precios finales según `PRICING.md`.

---

🤖 Generado con [Claude Code](https://claude.com/claude-code)
