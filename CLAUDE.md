# Plantilla «Psicología y terapia» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **sereno**
(salvia + arena + carbón, serif de sistema grande y mucho aire, bandas a todo el ancho de color pleno, fotos a
sangre de naturaleza y consulta, tarjetas y retratos en arco, antetítulos con un «horizonte»: línea fina y sol).
Todo en castellano de España, frases cortas, tono cálido y sin jerga clínica. Nunca hables de cómo está hecha la web.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = salvia de bandas y botones, acento = arena dorada de soles, comillas y detalles, fondo = arena clara, texto = carbón). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`… Los derivados (`--claro`, `--hondo`, `--carbon`, `--linea`, `--suave`) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-texto`, `--fuente-titulos`, `--ancho` 90 rem, bandas `.banda-salvia/.banda-clara/.banda-honda/.banda-carbon`, botones `.btn`/`.btn-sec`, cabecera `.cabecera--sereno`, pie `.pie--sereno`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (se generan aparte a partir de `fotos.json`); las de respaldo en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las personas usan `/placeholders/persona.svg` hasta que el cliente suba su foto: **no se generan caras**.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = sol sobre el horizonte + nombre en serif.
- **Cabecera**: fija a todo el ancho; transparente sobre la portada a sangre hasta que se hace scroll (script pequeño en `Header.astro`; sin JavaScript se queda sólida). Botón = `site.yaml → boton_cabecera`.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones (en este orden en el ejemplo)
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. Un apartado nuevo puede reutilizar un diseño con `tipo: <id>`.
- `hero` → `hero.astro`: pantalla casi completa con `imagen` a sangre y velo salvia (sin foto, salvia honda), `antetitulo`, `titulo` enorme, `texto`, `cta`, `cta_secundario` y franja de accesos `items: [{titulo, texto, icono}]`.
- `motivos` → `motivos.astro`: banda salvia plena; `items: [{titulo}]` como palabras grandes en serif separadas por soles.
- `terapias` → `terapias.astro`: tarjetas en arco con `terapias: [{titulo, texto, modalidad, duracion, precio}]`, `cta` e `imagen` como franja a sangre debajo.
- `frase` → `frase.astro`: `declaracion` enorme en cursiva, `autor`, `imagen` a sangre de fondo (sin foto, salvia honda).
- `proceso` → `proceso.astro`: banda salvia clara; `items: [{titulo, texto, icono}]` sobre una línea de horizonte.
- `sobre` → `sobre.astro`: fila 50/50 con `imagen` a sangre a la izquierda; `declaracion`, `texto` (párrafos con línea en blanco), `items` (credenciales con icono); debajo `subtitulo` y `personas: [{nombre, cargo, foto, texto}]` con retratos en arco.
- `espacio` → `espacio.astro`: banda carbón y `galeria` en mosaico de borde a borde (la primera, grande).
- `preguntas` → `preguntas.astro`: `preguntas: [{pregunta, respuesta}]` en acordeón. Sin preguntas no se pinta.
- `cita` → `cita.astro`: 50/50 salvia plena + formulario; `items` (pasos), `cta`, `enlace_agenda` + `texto_agenda`, `nota`, `boton`. El formulario saca las terapias y las modalidades de la sección `terapias`.
- `contacto` → `contacto.astro`: 50/50 con los datos de `contacto` en grande e `imagen` a sangre a la derecha; si `cita` no está activa, el formulario va aquí. `boton`: texto del botón.
- `texto` → `texto.astro`: apartado genérico (`tipo: texto`) con `declaracion`, `items`, `imagen` (50/50 a sangre) y `cta`.

## Campos propios de esta plantilla (además del esquema común)
- `terapias.terapias[]`: `titulo`, `texto`, `modalidad` («Presencial», «Online» o «Ambas»; «Ambas» se muestra «Presencial y online»), `duracion` («50 min»), `precio` (cadena: «65 €», «Consultar»; vacío = no se muestra). Máximo 24.
- `frase.declaracion`, `frase.autor`. `sobre.declaracion`, `sobre.subtitulo`.
- `cita.enlace_agenda` (url de agenda online, opcional), `cita.texto_agenda`, `cita.nota`, `cita.boton`. `contacto.boton`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para varios valores, una cadena separada por «;».
5. **No inventes** precios, opiniones, colegiaciones, años ni datos clínicos: si el cliente no los da, deja el campo vacío o la lista vacía; el componente lo oculta. Esta plantilla no lleva opiniones de pacientes a propósito.
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Sección nueva**: mejor un id nuevo con `tipo:` (`texto`, `terapias`, `proceso`, `frase`…). Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y bandas a todo el ancho. `src/pages/index.astro` la recoge sola.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt). `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor`, `--gutter`), bandas y fotos de borde a borde, sin scroll horizontal en móvil, ids `hero` y `contacto`. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altGaleria`, `altSeccion`, `altFicha` de `src/lib/seo.ts`, o el nombre de la persona); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.terapias.terapias` → `/terapias/<slug>/` (terapia).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/terapias/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
