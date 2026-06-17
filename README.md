# Sify Blog

Tema de blog moderno basado en Astro 6 + Tailwind CSS v4, con soporte para modo claro/oscuro, MDX, fórmulas matemáticas, búsqueda global y sistema de comentarios.

![Astro](https://img.shields.io/badge/Astro-6.x-BC52EE?logo=astro)
![Tailwind](https://img.shields.io/badge/Tailwind-v4-06B6D4?logo=tailwindcss)
![License](https://img.shields.io/badge/license-MIT-blue)

## Características

- **Markdown / MDX** — Soporte para Markdown estándar y componentes JSX incrustados
- **Fórmulas matemáticas KaTeX** — Renderizado de fórmulas LaTeX en línea y en bloque
- **Resaltado de código** — Shiki para resaltado de sintaxis + botón de copiar con un clic
- **Modo oscuro** — Sigue las preferencias del sistema + cambio manual, persistente en `localStorage`
- **Búsqueda global** — `Ctrl+K` para abrir, coincidencia en título/contenido, resaltado
- **Comentarios Waline** — Sistema de comentarios listo para usar
- **Página de enlaces** — Enlaces de amigos + actividad del círculo de enlaces
- **Portada de artículos** — Soporte para URL remota e imágenes locales
- **Suscripción RSS** — Generación automática de `/rss.xml`
- **Diseño responsivo** — Escritorio con dos columnas + barra lateral tipo drawer en móvil
- **Optimización SEO** — Open Graph, Twitter Card, Canonical URL
- **Barra lateral** — Información personal, nube de categorías/etiquetas, recomendaciones aleatorias

## Stack tecnológico

| Tecnología | Uso |
|------------|-----|
| [Astro 6](https://astro.build) | Generación de sitios estáticos |
| [Tailwind CSS v4](https://tailwindcss.com) | Framework CSS |
| [Shiki](https://shiki.style) | Resaltado de sintaxis de código |
| [KaTeX](https://katex.org) | Renderizado de fórmulas matemáticas |
| [MDX](https://mdxjs.com) | Markdown + JSX |
| [Waline](https://waline.js.org) | Sistema de comentarios |

## Inicio rápido

### Requisitos del entorno

- [Bun](https://bun.sh) (recomendado) o Node.js 18+

### Instalación

```bash
git clone <your-repo-url> my-blog
cd my-blog
bun install
```

### Desarrollo local

```bash
bun dev
```

Abre <http://localhost:4321>, con recarga en caliente.

### Compilación

```bash
bun run build
```

La salida está en el directorio `dist/`.

### Previsualizar compilación de producción

```bash
bun preview
```

## Configuración

Edita `src/consts.ts`:

```typescript
export const SITE_TITLE = 'Hugo Alvarez';
export const SITE_DESCRIPTION = 'Un tema de blog moderno basado en Astro';
export const SITE_AUTHOR = 'santisify';
export const SITE_URL = 'https://example.com';
export const SITE_AVATAR = '/favicon.svg';
export const SITE_COVER = '/images/cover.jpg';

export const PAGE_SIZE = 10;

export const NAV_ITEMS = [
  { label: 'Inicio', href: '/' },
  { label: 'Boletín', href: '/weekly' },
  { label: 'Artículos', href: '/archives' },
  { label: 'Enlaces', href: '/friends' },
  { label: 'Acerca de', href: '/about' },
];

export const SOCIAL_LINKS = [
  { name: 'GitHub', href: 'https://github.com/yourname', icon: 'github' },
  { name: 'RSS', href: '/rss.xml', icon: 'rss' },
];
```

### Personalizar color del tema

Edita `src/styles/global.css`:

```css
@theme {
  --color-primary: #e9536a;
  --color-bg-light: #f5f5f5;
  --color-bg-dark: #1a1a2e;
  --color-card-light: #ffffff;
  --color-card-dark: #1e2a45;
}
```

### Personalizar fuente

```css
--font-family-sans: 'Inter', 'Noto Sans SC', sans-serif;
--font-family-mono: 'JetBrains Mono', 'Fira Code', monospace;
```

## Escribir artículos

Crea archivos `.md` o `.mdx` en `src/content/blog/`.

### Frontmatter

```yaml
---
title: Título del artículo
description: Descripción del artículo
date: 2024-06-01
updated: 2024-06-15     # Opcional, fecha de actualización
tags: [Etiqueta1, Etiqueta2]
category: Categoría
cover: ./images/cover.webp  # URL remota o ruta relativa local
pinned: false              # Si se fija en la parte superior
draft: false               # Los borradores no entran en RSS
---
```

### Estructura de directorios

Se admiten dos formas:

```
src/content/blog/
├── my-post.md              # Archivo único (slug: my-post)
└── another-post/
    ├── index.md             # Formato de directorio (slug: another-post)
    └── cover.webp           # Imagen local
```

### Boletín semanal

Crea artículos en `src/content/weekly/`, necesita un campo `issue` adicional:

```yaml
---
title: Boletín #1
date: 2024-06-02
tags: [Frontend]
issue: 1
cover: https://example.com/cover.jpg
---
```

## MDX y componentes

En archivos MDX puedes importar y usar componentes Astro personalizados:

```mdx
---
title: Ejemplo MDX
date: 2024-06-01
---

import LinkCard from '../../../components/LinkCard.astro';

<LinkCard
  url="https://astro.build"
  title="Documentación oficial de Astro"
  description="Framework web completo para sitios orientados a contenido"
/>
```

Componentes incluidos:

- `LinkCard` — Tarjeta de enlace externo (`src/components/LinkCard.astro`)

Crear nuevos componentes:

1. Crea un archivo `.astro` en `src/components/`
2. Impórtalo y úsalo en el archivo MDX

## Fórmulas matemáticas

KaTeX está preconfigurado. Usa `$...$` o `$$...$$` directamente en Markdown:

```markdown
Fórmula en línea: $E = mc^2$

Fórmula en bloque:
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$
```

## Sistema de comentarios

Configura el servidor de comentarios Waline:

Edita `src/components/waline/Comment.astro`, modifica `serverURL`:

```typescript
walineInit({
  el: '#waline',
  serverURL: 'https://your-waline-server.com',
  lang: 'es',
  // ...
});
```

## Enlaces de amigos

Edita `public/links.json` para añadir enlaces de amigos:

```json
{
  "friends": [
    {
      "id_name": "cf-links",
      "desc": "Enlaces de amigos",
      "link_list": [
        {
          "name": "Blog del amigo",
          "link": "https://friend.example.com",
          "avatar": "https://friend.example.com/avatar.jpg",
          "intro": "Biografía personal"
        }
      ]
    }
  ]
}
```

## Despliegue

### Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)

Despliegue con un clic, sin configuración adicional.

### Cloudflare Pages

| Configuración | Valor |
|---------------|-------|
| Comando de compilación | `bun run build` |
| Directorio de salida | `dist` |

### Otro alojamiento estático

Después de compilar, sube directamente el contenido del directorio `dist/` a cualquier servidor de archivos estáticos.

### Verificación antes del despliegue

```bash
# Compilar
bun run build

# Previsualizar (opcional)
bun preview
```

Asegúrate de que existan los siguientes archivos:
- `dist/index.html`
- `dist/rss.xml`
- `dist/search-index.json`
- `dist/favicon.svg`

## Estructura del proyecto

```
astro-theme-sify/
├── src/
│   ├── components/       # Componentes Astro
│   │   └── waline/       # Componentes de comentarios Waline
│   ├── content/
│   │   ├── blog/         # Artículos del blog
│   │   └── weekly/       # Artículos del boletín
│   ├── layouts/          # Componentes de layout
│   ├── pages/            # Páginas de rutas
│   └── styles/           # Estilos globales
├── public/               # Recursos estáticos
│   └── links.json        # Datos de enlaces
├── astro.config.ts       # Configuración de Astro
├── src/consts.ts         # Configuración del sitio
├── src/content.config.ts # Schema de colecciones de contenido
└── package.json
```

## License

MIT
