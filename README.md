# Portfolio Artistas

Plantilla de portfolio web para artistas visuales, pensada para mostrar obra, proceso creativo y facilitar la venta o el encargo de piezas — sin depender únicamente de redes sociales.

Construida con [Astro](https://astro.build) + [Tailwind CSS](https://tailwindcss.com). Caso de uso actual: portfolio de [Flor Ortega](https://www.instagram.com/ortega_flor_), artista de realismo en grafito y carboncillo (San Rafael, Mendoza).

## Demo

_Agregar acá el link de producción una vez desplegado en Vercel._

## Características

- **Hero con carrusel de fondo** — crossfade automático entre varias imágenes de obra, con animación de entrada en el texto y respeto por `prefers-reduced-motion`.
- **Navbar responsive** — versión desktop con links directos, versión mobile con menú hamburguesa animado.
- **Sección "La artista"** — narrativa personal, pensada para generar cercanía antes de mostrar el catálogo.
- **Galería de obra** con:
  - Estados de venta por pieza (`disponible`, `vendida`, `a-pedido`).
  - Tipos de pieza (`original`, `impresión`, `encargo`).
  - Modal con mini-galería de fotos y videos de proceso relacionados a cada obra.
  - Zoom táctil/con mouse sobre el detalle de cada imagen.
- **Cuaderno de bocetos** — slider horizontal para contenido más suelto e informal (dibujos rápidos, práctica diaria).
- **Sección de proceso** — fotos y videos de "detrás de escena", conectados a la obra terminada correspondiente cuando aplica.
- **Reseñas de clientes**.
- **Formulario de encargo** — reemplaza el "escribime por DM" por un formulario estructurado (vía Formspree).
- **Botón "volver arriba"** flotante, con aparición animada al hacer scroll.
- Paleta y tipografía propias (tonos papel/tinta/borgoña, Fraunces + Inter) en vez de estilos por defecto.

## Stack

- [Astro](https://astro.build) — sitio estático, componentes `.astro`.
- [Tailwind CSS v4](https://tailwindcss.com) — estilos utilitarios, tema definido en `src/styles/global.css` con `@theme`.
- TypeScript (interfaces livianas para tipar los datos de `src/data/`).
- Sin frameworks de UI adicionales — JavaScript vanilla para interactividad (modal, carrusel, menú, zoom).

## Requisitos

- [Node.js](https://nodejs.org) 18 o superior.
- Cuenta gratuita en [Formspree](https://formspree.io) para que funcione el formulario de encargo.

## Instalación

```bash
git clone https://github.com/FlorenciaOrtega82/Portfolio-artistas.git
cd Portfolio-artistas
npm install
npm run dev
```

El sitio queda disponible en `http://localhost:4321`.

## Estructura del proyecto

```
/
├── public/
│   ├── images/          # fotos de obra, proceso, sketchbook, logo
│   └── videos/          # timelapses y videos de proceso
├── src/
│   ├── components/
│   │   ├── Navbar.astro
│   │   ├── Hero.astro
│   │   ├── AboutSection.astro
│   │   ├── Gallery.astro
│   │   ├── SketchbookSection.astro
│   │   ├── ProcessSection.astro
│   │   ├── TestimonialsSection.astro
│   │   ├── CommissionForm.astro
│   │   ├── Footer.astro
│   │   └── BackToTop.astro
│   ├── data/
│   │   ├── artworks.json     # catálogo de obras
│   │   ├── process.json      # fotos/video de proceso, ligados a artworks por artworkId
│   │   ├── sketchbook.json   # páginas del cuaderno de bocetos
│   │   └── testimonials.json # reseñas de clientes
│   ├── layouts/
│   │   └── Layout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css        # tema de Tailwind (colores, tipografías)
└── package.json
```

## Modelo de datos

### `artworks.json`

Cada obra tiene esta forma:

```json
{
  "id": "identificador-unico",
  "title": "Título de la obra",
  "image": "/images/nombre-archivo.jpg",
  "type": "original | impresion | encargo",
  "status": "disponible | vendida | a-pedido",
  "price": 45000,
  "priceVisible": true,
  "description": "Descripción de la pieza.",
  "technique": "Grafito sobre papel",
  "size": "30x40cm",
  "featured": true,
  "gallery": ["/images/foto-extra-1.jpg"]
}
```

`price` puede ser `null` cuando no aplica o no se muestra (por ejemplo, en encargos con precio variable). `gallery` es opcional: fotos adicionales de esa pieza puntual (aparte de las de `process.json`).

### `process.json`

```json
{
  "id": "identificador-unico",
  "title": "Título del ítem de proceso",
  "media": "/images/proceso-x.jpg",
  "isVideo": false,
  "description": "Descripción breve.",
  "artworkId": "id-de-la-obra-relacionada"
}
```

Si `artworkId` coincide con el `id` de una obra en `artworks.json`, ese contenido aparece también dentro del modal de esa obra en la Galería. Si `artworkId` se deja vacío, el ítem se muestra solo en la sección "Proceso", con su propio visor.

### `sketchbook.json` y `testimonials.json`

Estructuras más simples, ver los archivos de ejemplo en `src/data/` para el formato exacto de cada uno.

## Personalización para un nuevo cliente

Este proyecto nació como plantilla reutilizable, no solo como sitio personal. Para adaptarlo a otro artista:

1. Reemplazar los datos en `src/data/*.json` por el contenido del nuevo cliente.
2. Actualizar props de `Hero.astro`, `AboutSection.astro` y `Footer.astro` (nombre, tagline, redes, mail).
3. Reemplazar `public/images/logo.svg` por el logo del cliente.
4. Ajustar la paleta de colores en `src/styles/global.css` si el cliente lo requiere (por defecto: tonos papel/tinta/borgoña).
5. Configurar un endpoint propio de Formspree para el formulario de encargo.

## Despliegue

El proyecto está pensado para desplegarse en [Vercel](https://vercel.com): conectar el repositorio desde el dashboard de Vercel, que detecta Astro automáticamente sin configuración adicional.

## Roadmap

- [ ] Newsletter / captura de mail (pendiente por disponibilidad de tiempo).
- [ ] Versión self-service para que otros artistas carguen su propio contenido sin intervención manual.
- [ ] Integración de feed de Instagram embebido.

## Autora

Flor Ortega — artista y desarrolladora Front End. [Instagram](https://www.instagram.com/ortega_flor_) · San Rafael, Mendoza.
