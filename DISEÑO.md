# Psicología y terapia: brief de diseño

Plantilla `psicologia-terapia` creada el 29/10/2026 a partir de `profesional-autonomo` con `php artisan plantillas:nueva`
y rediseñada entera a ancho completo. Este fichero se queda en el repo: es lo que lee quien (persona o agente) la rediseñe.

## Brief

- **Para quién**: consultas de psicología, centros de terapia, logopedas, coaches y grupos de mindfulness
  (`sectores`: psicologia, terapia, logopedia, coaching, mindfulness). Quien entra suele estar pasándolo mal o
  acompaña a alguien (un hijo, la pareja): busca calma, confianza, saber qué le van a hacer, cuánto cuesta y
  cómo dar el primer paso sin exponerse.
- **Qué tiene que conseguir la web**: pedir la primera cita (formulario, WhatsApp o teléfono) con la menor fricción.
- **Tono y estilo** (`estilo: sereno`): sereno, cálido, respirado. Sí: estudios de bienestar con mucha foto de
  naturaleza y tipografía editorial. No: web clínica de bata blanca ni plantilla de «coach motivacional».
- **Paleta de ejemplo**: primario salvia `#4d6a56`, acento arena dorada `#cfae7d`, fondo arena clara `#f2ede4`,
  texto carbón `#23282a`. Derivados con `color-mix`: `--claro` (salvia 16 % sobre arena), `--hondo` (salvia +
  carbón, cabecera de foto y pie), `--carbon`. El acento solo va como decoración o sobre fondos oscuros.
- **Tipografía**: titulares en serif de sistema («Iowan Old Style», «Palatino Linotype», Palatino, Georgia),
  400, muy grandes (hero hasta 7,25 rem; móvil 2,75 rem), con cursiva para la frase y los motivos alternos;
  texto en `system-ui`; antetítulos en mayúsculas espaciadas con «horizonte» (línea fina y sol pequeño).
- **Motivos propios**: el arco (tarjetas de terapia y retratos con la parte de arriba en arco: refugio, ventana)
  y el horizonte (antetítulos, línea de los pasos, marca sin logo: sol sobre dos líneas).

## Ritmo de bandas (todas de borde a borde)

1. `hero`: foto a sangre de naturaleza (92svh) con velo salvia, titular enorme, dos botones y franja de
   accesos (`items`) en salvia translúcida. Cabecera transparente encima.
2. `motivos`: salvia plena; palabras grandes en serif separadas por soles (`items: [{titulo}]`).
3. `terapias`: arena; titular partido 7/4; rejilla 1/2/3 de tarjetas en arco salvia clara
   (`terapias: [{titulo, texto, modalidad, duracion, precio}]`) y franja de foto a sangre 21:8.
4. `frase`: foto a sangre de bosque con velo; cita enorme en cursiva centrada (`declaracion`, `autor`).
5. `proceso`: salvia clara; pasos sobre una línea de horizonte (horizontal ≥ 900 px, vertical en móvil).
6. `sobre`: fila 50/50 con foto a sangre a la izquierda; credenciales; retratos en arco (`personas`).
7. `espacio`: carbón; mosaico de borde a borde sin márgenes (`galeria`).
8. `preguntas`: arena; titular fijo a la izquierda, acordeón a la derecha.
9. `cita`: 50/50 salvia plena (pasos, WhatsApp, teléfono) + salvia clara con el formulario (terapias,
   modalidad en píldoras, franja horaria).
10. `contacto`: 50/50 datos en serif grande + foto a sangre del portal a la derecha.
11. Pie salvia honda con cuatro columnas.

## Responsive

Móvil primero: 16 px de margen del texto, fotos y fondos de borde a borde, botones de 48 px, menú plegable con
`details`. A 768 cambian la franja de accesos (3 columnas), las tarjetas (2) y el mosaico; desde 1024 las filas
pasan a 50/50 y desde 1100 las terapias a 3 columnas. Sin scroll horizontal (comprobado a 375, 768 y 1440).

## Fotos

`fotos.json` (9): bahía cantábrica al amanecer (hero), mesa con portátil junto a ventana (franja de terapias),
hayedo con niebla (frase), consulta con butacas salvia (sobre), sala de terapia, detalle de mesa, sala de grupo
con cojines, ventana a los tejados y el mar, portal del ensanche (contacto). Sin personas, sin texto, sin logotipos.

## Qué no hacer

- Nada de caja centrada estrecha con tarjetas blancas ni del hero 5/7 con retrato de `profesional-autonomo`.
- No añadir opiniones de pacientes (delicado en sanidad) ni cifras de «casos de éxito».
- No meter fotos de caras ni antes/después; personas con la silueta hasta que el cliente suba la suya.
