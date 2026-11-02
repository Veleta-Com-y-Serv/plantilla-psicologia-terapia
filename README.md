# Plantilla NoExpertise · Psicología y terapia

Web serena para psicólogos, terapeutas, logopedas, coaches y centros de mindfulness: portada a pantalla completa con
foto a sangre, motivos de consulta, terapias con modalidad, duración y precio opcional, cómo trabajas, equipo,
la consulta en mosaico, preguntas frecuentes y primera cita con formulario.

- Sectores: psicologia, terapia, logopedia, coaching, mindfulness. Estilo: sereno. Plan mínimo: gratis. Orden 290.
- Secciones: hero, motivos, terapias, frase, proceso, sobre, espacio, preguntas, cita, contacto (+ `texto` genérico).
- Campos propios: `hero.items[]` (accesos), `motivos.items[].titulo`, `terapias.terapias[]` (titulo, texto,
  modalidad, duracion, precio), `frase.declaracion/autor`, `sobre.declaracion/subtitulo/personas[]`,
  `espacio.galeria[]`, `cita.items[]/enlace_agenda/texto_agenda/nota/boton`, `contacto.boton`.
- Diseño: salvia + arena + carbón, serif de sistema grande, bandas a todo el ancho (salvia plena, arena, salvia
  clara, carbón), fotos a sangre 50/50 y mosaico de borde a borde, tarjetas y retratos en arco, cabecera fija
  transparente sobre la portada y pie salvia hondo con columnas. Detalle en `DISEÑO.md`.
- Ejemplo: «Lur Psicología», centro ficticio de San Sebastián (teléfonos ficticios).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en
  `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`).
Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.terapias.terapias` con `detalle` tiene su página en `/terapias/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
