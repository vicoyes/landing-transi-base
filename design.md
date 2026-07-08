name: Alquimia de Alma
colors:
  surface: '#fbf9f4'
  surface-dim: '#dbdad5'
  surface-bright: '#fbf9f4'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f5f3ee'
  surface-container: '#f0ede8'
  surface-container-high: '#e9e7e2'
  surface-container-highest: '#e4e2dd'
  on-surface: '#1c1c1a'
  on-surface-variant: '#484742'
  outline: '#797771'
  outline-variant: '#c9c6bf'
  primary: '#d4af37'
  on-primary: '#ffffff'
  primary-container: '#f3e5b3'
  on-primary-container: '#231b00'
  secondary: '#705d00'
  on-secondary: '#ffffff'
  secondary-container: '#ffe16e'
  on-secondary-container: '#221b00'
  tertiary: '#4b6546'
  on-tertiary: '#ffffff'
  tertiary-container: '#cdebc4'
  on-tertiary-container: '#092008'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#410002'
  hero-surface: '#33362a'
  hero-surface-variant: '#4b4f3c'
  on-hero-surface: '#f5f1e6'
  on-hero-surface-variant: '#d8d4c4'
typography:
  font-family: EB Garamond, serif
  ui-family: Manrope, sans-serif
  headings:
    weight: 400-600
    style: normal
  body:
    weight: 400
    style: normal
stack:
  css: Tailwind CDN (cdn.tailwindcss.com) con tailwind.config inline mapeando los tokens de `colors` de este archivo, sin build step
  icons: Lucide (unpkg.com/lucide) via data-lucide + lucide.createIcons()
  fonts: Google Fonts — EB Garamond (font-serif, titulares) y Manrope (font-sans, cuerpo/UI)
  deploy: estático, sin bundler (ver .github/workflows/pages.yml)
shadows:
  soft: 0 4px 20px rgba(212, 175, 55, 0.08)
  glass: 0 8px 32px 0 rgba(31, 38, 135, 0.07)
effects:
  glassmorphism:
    blur: 12px
    border: 1px solid rgba(255, 255, 255, 0.3)
    background: rgba(255, 255, 255, 0.4)
  iridescence:
    gradient: linear-gradient(135deg, #fceabb 0%, #f8b500 25%, #fceabb 50%, #f8b500 75%, #fceabb 100%)
    animation: shine 8s ease infinite
  chromatic-prism:
    description: Reemplazado por una foto real (assets/hero-rainbow.jpg/.webp) sobre el hero — ver seccion "Hero / Portada" mas abajo. Este token queda solo como referencia historica del gradiente sintetico original.
  rainbow-muted:
    description: Paleta arcoiris muestreada de assets/hero-rainbow.jpg (colores reales del haz de luz de la foto, no valores arbitrarios). Es la paleta "oficial" para cualquier acento arcoiris del sitio — mas apagada/pastel que un arcoiris saturado tipico, a tono con la foto del hero.
    terracota: '#cf9683'
    ambar: '#dfb07c'
    caqui: '#c9c095'
    salvia: '#a1b59a'
    pizarra: '#8f9ea1'
    violeta-azulado: '#8f8d9a'
    uso: .rainbow-edge (borde, alpha ~0.55) y .rainbow-glow (conic-gradient, opacidad de capa ~0.2)
---

# Alquimia de Alma - Guía de Estilo

Esta guía define la dirección visual para la experiencia de transformación consciente de Transi Aracil.

## Conceptos Clave
- **Sabiduría Ancestral:** Uso de tipografías Serif (EB Garamond) que evocan manuscritos y tradición.
- **Transmutación:** Efectos de vidrio y destellos iridiscentes que simbolizan el cambio del plomo al oro.
- **Serenidad:** Una paleta de colores crema y arena que proporciona un fondo tranquilo para el trabajo espiritual.

## Componentes Compartidos
- **Navegación:** Glassmorphism con desenfoque de fondo y logo en cursiva dorada.
- **Tarjetas de Pilares:** Contenedores de cristal con bordes animados que reaccionan al interactuar.
- **Botones (CTA):** Fondo dorado sólido (`primary`) con tipografía en mayúsculas para máxima claridad y peso.

## Hero / Portada — Efecto Cristal Cromático
- **Fondo:** foto real de dispersión de luz (`assets/hero-rainbow.jpg` / `.webp`, ~10-20KB optimizada de un original de 1.3MB) en vez del degradado sintético original. Clase utilitaria: `.hero-prism`.
- **Capas de `.hero-prism`:** `::before` pinta la foto (`image-set` webp+jpg, Ken Burns autónomo de 30s animando `background-size`/`background-position`); `::after` superpone un velo oscuro (`linear-gradient`, alpha ~0.44–0.58) para mantener el texto legible sin apagar el color de la imagen. Rango validado por contraste real (WCAG, muestreado sobre capturas): por debajo de ~0.4 el cuerpo de texto (`on-hero-surface-variant`) cae bajo 3:1; por encima de ~0.65 se empieza a perder el arcoíris de la foto. Si se reemplaza la imagen o se vuelve a pedir "aclarar/oscurecer", volver a validar contraste en ese rango antes de mover la opacidad — no ajustar a ojo.
- **`.pending` sobre el hero:** el estilo base (`color: #705d00`, marrón) es ilegible sobre `.hero-prism` (fondo oscuro). Regla `.hero-prism .pending` lo fuerza a blanco con subrayado punteado dorado (`#ffe16e`). Cualquier placeholder `[CORCHETE]` nuevo dentro del hero/cierre hereda esto automáticamente, no hace falta tocarlo.
- **Parallax:** un listener de scroll (rAF-throttled, en el `<script>` final) escribe `--hero-parallax` en cada `.hero-prism` según su posición en el viewport (±36px), y `::before` lo lee en su `transform: translateY(...)`. Se desactiva por completo si `prefers-reduced-motion: reduce`. El Ken Burns queda en `background-size`/`background-position` (no en `transform`) justamente para no pisarse con este parallax.
- **Titular:** `font-serif` (EB Garamond) en `on-hero-surface` (crema), tamaño grande, sin mayúsculas forzadas.
- **Subtítulo/cuerpo:** `font-sans` (Manrope), color `on-hero-surface-variant`, peso normal/ligero.
- **Badge de autora:** avatar circular + nombre en negrita + rol, en la esquina inferior del bloque de texto, sobre el propio fondo oscuro (sin tarjeta adicional).
- El hero abre y cierra la página (bookend): la sección de cierre reutiliza el mismo `.hero-prism` para dar simetría visual.

## Liquid Glass (tarjetas y navegación) — estilo Apple
Técnica de **capas reales**, no pseudo-elementos combinados con el contenido: el filtro SVG de distorsión (`filter: url(#liquid-glass-distortion)`, `feTurbulence` + `feDisplacementMap`) vive en una capa vacía dedicada, separada del contenido — así solo se deforma el "vidrio", nunca el texto. Es la técnica robusta detrás de las demos "liquid glass" que circulan (evita los problemas de compatibilidad de referenciar un filtro SVG directamente dentro de `backdrop-filter`).
- **Marcado:** cualquier elemento con clase `.prism-glass`, `.prism-glass-dark` o `.liquid-nav` ya se ve bien solo (fallback: `background` + `backdrop-filter: blur() saturate()` + `box-shadow`). El `<script>` final (`initLiquidGlass()`) antepone 3 capas reales como hermanos del contenido original — **nunca lo envuelve**, porque mover un `<summary>` dentro de un `<div>` rompe el `<details>` nativo del FAQ:
  - `.liquid-glass__effect` (z-index 0): `backdrop-filter: blur(5px)` + `filter: url(#liquid-glass-distortion)` — la distorsión real.
  - `.liquid-glass__tint` (z-index 1): color plano semitransparente (blanco en claro, oscuro en `-dark`/nav).
  - `.liquid-glass__shine` (z-index 2): `box-shadow` inset en dos esquinas opuestas — el brillo especular/bisel.
  - El contenido original queda como hermano de estas capas y se eleva por CSS (`.liquid-glass--ready > :not(...)`  → `position: relative; z-index: 3`), sin tocar su estructura.
- **`.rainbow-edge`:** borde de 1.5px con el mismo degradado arcoíris del hero, animado y muy sutil (mask-composite para que solo se vea el borde), como la aberración cromática de una lente real. Se combina con `.prism-glass` en tarjetas destacadas (portales, imagen del hero, tarjeta de inversión).
- **`.liquid-nav`:** mismo sistema en la navegación sticky — al estar montada sobre el hero, el vidrio distorsiona en vivo la foto del arcoíris que pasa detrás.
- **Glow (`.rainbow-glow`):** halo arcoíris difuminado que rota detrás de cada `.rainbow-edge`, técnica "animated border glow" (conic-gradient gigante rotando, `filter: blur()`, sangrando fuera del borde). Tiene que ser un elemento real separado del propio wrapper (`initRainbowGlow()` en el `<script>` final lo antepone como hermano dentro de un `.glow-wrapper` inyectado) porque el `overflow: hidden` del vidrio recortaría el desenfoque si fuera un pseudo-elemento de la misma caja. Opacidad deliberadamente baja (`0.2`): como las tarjetas de liquid glass son translúcidas, el glow se filtra hacia el interior — subirla mucho lava el texto de color. Si se ajusta, verificar que el interior de las tarjetas siga leyéndose limpio, no solo el halo exterior.
- **Placeholders de copy pendiente:** clase `.pending` (subrayado dorado punteado + `title` con tooltip) para marcar visualmente los `[CORCHETES]` del copy que Transi debe confirmar.