# Cenere — Artisan Neapolitan Pizza · Landing Page

A luxury single-page website for **Cenere**, an artisan Neapolitan pizzeria. Built as a self-contained `index.html` with zero external dependencies beyond two Google Fonts families.

Designed and built by **Vesa Studios** (Pune, India).

---

## Features

### Hero — Scroll-Driven Pizza Animation
The centrepiece of the page. A sequence of pizza images is preloaded and rendered on an HTML `<canvas>`. As the user scrolls through a 500 vh tall sticky zone, the frames play in reverse — the pizza "assembles" from raw ingredients as the user scrolls down. Overlays (headline, tagline, ingredient call-outs, CTA) fade in and out at specific scroll progress thresholds.

### Loading Screen
A branded splash screen with a wordmark, subtitle, animated progress bar, and percentage counter that tracks actual image preload progress before revealing the page.

### Visual Effects
- **Film grain** — fixed SVG `feTurbulence` filter overlay at very low opacity
- **Vignette** — fixed radial-gradient overlay darkening the edges
- **Mix-blend-mode navbar** — the nav bar uses `mix-blend-mode: difference` so it stays readable over any background

### Menu Section (Tabbed)
Three tab panels — Classici, Bianche, Stagione — each containing pizza rows with:
- Thumbnail image (zoom-on-hover)
- Name, description, and drink pairing tag
- Price with size label
- Staggered fade-in animation when a tab is opened

### Pizza Showcase Carousel (Conveyor Belt)
An auto-rotating card carousel featuring signature pizzas. Supports:
- Continuous auto-scroll (RAF-based, 0.4 px/ms)
- Drag / touch scrubbing with snap-to-card on release
- Prev / Next buttons and dot indicators
- Keyboard navigation (← →)
- Smooth lerp (8% per frame) between auto and manual positions

### Heritage / Story Section
A two-column editorial grid with a heading, body copy, and a set of three numbered craft credentials (72-hour dough, wood-fired oven, Italian imports).

### Scroll-Triggered Section Reveals
All `.section` elements start invisible (`opacity: 0`, `translateY(32px)`) and are observed by an `IntersectionObserver`; they animate in once 15% of the element is visible.

---

## Structure

```
index.html
├── <head>           Google Fonts (Cormorant Garamond, Jost), all CSS inline
├── #grain           Fixed film-grain SVG filter
├── #vignette        Fixed vignette overlay
├── <nav>            Fixed top navbar with logo, links, Vesa Studios badge
├── #loader          Full-screen loading splash
├── #scroll-zone     500 vh sticky scroll container
│   └── #sticky-canvas-wrap
│       ├── #canvas              Pizza frame animation
│       └── .overlay ×6          Headline, tagline, spec labels (L/R), CTA, scroll hint
├── #content
│   ├── .section (heritage)      Story / brand copy
│   ├── .section-divider
│   ├── .section (menu)          Tabbed menu with pizza rows
│   ├── .section-divider
│   └── .section (conveyor)      Auto-rotating pizza card carousel
├── #vesa-footer-credit          Studio attribution footer
└── <script>                     All JS inline (no build step)
```

---

## Image Assets Required

The animation expects a sequence of numbered pizza frames. By default the script is configured for **90 frames** loaded from a `frames/` directory (or equivalent path):

```
frames/
  frame_001.jpg
  frame_002.jpg
  …
  frame_090.jpg
```

The menu rows and carousel cards also reference food photography images (pizza thumbnails). Replace the `src` attributes with your own hosted images or a CDN path.

---

## Fonts

| Family | Weights used | Role |
|---|---|---|
| Cormorant Garamond | 300, 400 (+ italic) | Headings, wordmarks |
| Jost | 200, 300, 400 | Body, labels, UI |

Loaded from Google Fonts via `<link>` in `<head>`.

---

## CSS Variables (Theme)

```css
--bg:           #0a0a0a   /* near-black background */
--fg:           #f0ece4   /* warm off-white foreground */
--accent:       #c0392b   /* deep red */
--accent-light: #e05c3a   /* burnt orange-red */
--muted:        rgba(240,236,228,0.45)
--serif:        'Cormorant Garamond', Georgia, serif
--sans:         'Jost', sans-serif
```

Change these four colour values in `:root` to re-theme the entire page.

---

## Browser Support

Requires a modern browser with support for:
- `<canvas>` 2D API
- CSS `position: sticky`
- `IntersectionObserver`
- `requestAnimationFrame`
- `backdrop-filter` (navbar blur; degrades gracefully)

No JavaScript frameworks, no build tools. Open `index.html` directly in a browser or serve from any static host.

---

## Deployment

Drop the file and the `frames/` image directory onto any static host (Netlify, Vercel, GitHub Pages, AWS S3, etc.). No server-side processing required.

```
/
├── index.html
└── frames/
    ├── frame_001.jpg
    └── …
```
