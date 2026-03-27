# AGENTS.md - Proyecto Boda

## Descripción

Página de invitación de boda hecha en Astro con diseño mobile-first. Incluye cuenta regresiva, ubicación, formulario RSVP, código de vestimenta, playlist de Spotify e información de regalos.

## Comandos

### Desarrollo
```bash
npm run dev          # Inicia servidor de desarrollo en http://localhost:4321
```

### Build
```bash
npm run build        # Genera versión de producción en /dist
npm run preview     # Previsualiza la build de producción
```

### Astro
```bash
npm run astro -- --help  # Ver comandos disponibles de Astro
```

### Testing
Este proyecto no tiene tests configurados. Para agregar tests, usar:
```bash
npx astro add vitest
```

## Estructura del Proyecto

```
/boda
├── public/
│   ├── images/         # Imágenes (novios, etc.)
│   └── favicon.svg
├── src/
│   ├── components/     # Componentes Astro reutilizables
│   │   ├── Hero.astro
│   │   ├── Countdown.astro
│   │   ├── CalendarButton.astro
│   │   ├── Location.astro
│   │   ├── RsvpForm.astro
│   │   ├── DressCode.astro
│   │   ├── SpotifyButton.astro
│   │   ├── GiftInfo.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Layout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Guías de Código

### Estructura de Componentes

Cada componente Astro sigue esta estructura:

```astro
---
// Frontmatter: imports, props, variables
const title = "Mi título";
---

<!-- Template HTML -->
<section class="mi-seccion">
  <h1>{title}</h1>
</section>

<!-- Estilos scoped -->
<style>
  .mi-seccion {
    padding: var(--spacing-lg) 0;
  }
</style>

<!-- Script del cliente (si es necesario) -->
<script>
  // Código JavaScript del cliente
</script>
```

### CSS

- Usar variables CSS definidas en `src/styles/global.css`
- Nombres de clases con kebab-case
- Estilos mobile-first (base styles, luego media queries para desktop)
- Prefijos: `--color-*`, `--font-*`, `--spacing-*`, `--border-radius-*`

### TypeScript

- Modo strict habilitado en `tsconfig.json`
- Usar tipos explícitos en props de componentes
- Non-null assertion (`!`) solo cuando se está seguro

### Convenciones de Nombres

| Tipo | Convención | Ejemplo |
|------|------------|---------|
| Componentes | PascalCase | `Hero.astro`, `Countdown.astro` |
| Variables | camelCase | `targetDate`, `eventTitle` |
| Props | camelCase | `title`, `description` |
| Clases CSS | kebab-case | `.hero-section`, `.countdown-item` |
| Constantes | UPPER_SNAKE_CASE | `BANK_ACCOUNTS` |
| Carpetas | kebab-case | `src/components`, `public/images` |

### Importaciones

```astro
---
// Imports de otros componentes
import Layout from '../layouts/Layout.astro';
import Hero from '../components/Hero.astro';

// Imports de utilidades
import { formatDate } from '../utils/date';
---
```

### Manejo de Errores

- Usar try/catch en código asíncrono del cliente
- Validar datos de props con TypeScript
- Mostrar mensajes amigables al usuario en caso de errores

### Imágenes

- Colocar en `public/images/`
- Usar formatos optimizados (WebP, JPG)
- Incluir atributo `alt` en imágenes

### Scripts Client-side

- Usar `<script>` con tipo módulo cuando sea necesario
- Preferir vanilla JS sobre frameworks innecesarios
- Asegurar que el código se ejecute después del DOM load

## Configuración de Google Forms (RSVP)

Para integrar el formulario con Google Sheets:

1. Crear Google Form en forms.google.com
2. Obtener el ID del formulario de la URL
3. Reemplazar `YOUR_FORM_ID` en `src/components/RsvpForm.astro`
4. Obtener los IDs de cada campo (entry.xxx) del formulario

## Despliegue

El proyecto puede desplegarse en cualquier hosting estático (Vercel, Netlify, GitHub Pages, etc.).

```bash
# Build para producción
npm run build

# La carpeta /dist contiene los archivos estáticos
```

## Notas Adicionales

- No hay linter configurado (puede agregarse con `npx astro add eslint` o `npx astro add biome`)
- No hay tests configurados
- Solo Astro (sin frameworks como React/Vue)
- CSS vanilla con variables CSS (sin Tailwind)
