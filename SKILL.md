---
name: tailwind-ux-ui
description: |
  A masterclass-level reference and design guidelines skill for implementing the premium, developer-centric UX/UI design system of tailwindcss.com.
  Use this skill when designing web interfaces, dashboards, documentation, and frontend components to ensure high-end aesthetics.
license: Apache-2.0
metadata:
  version: v4
  publisher: user-custom
---

# Tailwind CSS Premium UX/UI Design System Guide (v4)

This skill is a deep-dive, pixel-perfect study of the official **tailwindcss.com** site — including live source code, marketing design, and documentation layout. It provides exact implementation details, code blueprints, and styling parameters for recreating their premium, high-tech, developer-centric aesthetic using **Tailwind CSS v4**.

---

## 1. System Tokens & Color Palette

tailwindcss.com uses a curated palette — never generic colors.

### Neutral Base Colors
| Role | Light Mode | Dark Mode |
|---|---|---|
| Page background | `bg-white` | `dark:bg-gray-950` |
| Surface / Panel | `bg-gray-50` | `dark:bg-gray-900` |
| Subtle border | `border-gray-950/5` | `dark:border-white/10` |
| Divider line | `bg-gray-950/5` | `dark:bg-white/10` |

> **Note**: Tailwind v4 switched from `slate-*` to `gray-*` as the primary neutral. Use `gray-950` not `slate-950`.

### Brand & Accent Colors
| Role | Class | Hex |
|---|---|---|
| Sky (primary accent) | `sky-500` / `sky-400` (dark) | `#0ea5e9` |
| Monospace label, badge | `text-sky-500 dark:text-sky-400` | — |
| Sponsor button dashed | `text-sky-800 dark:text-sky-300` | — |

### Text Contrast Hierarchy
```
Primary heading    → text-gray-950 dark:text-white
Body / Secondary   → text-gray-600 dark:text-gray-400
Muted description  → text-gray-500 dark:text-gray-500
Monospace / Code   → text-sky-500 dark:text-sky-400
```

---

## 2. Tailwind v4 CSS-First Configuration

In Tailwind v4, configuration lives in CSS, not `tailwind.config.js`.

### A. Enabling Class-Based Dark Mode
```css
@import "tailwindcss";

/* Toggle dark mode via .dark class instead of media query */
@custom-variant dark (&:where(.dark, .dark *));
```

### B. Custom Theme Variables & Utilities
```css
@theme {
  --color-brand-primary: #0ea5e9;
  --color-brand-glow: rgba(14, 165, 233, 0.15);
}

@utility animate-blob {
  animation: blob 7s infinite;
}
```

### C. Key v4 New Utilities (Used Live on tailwindcss.com)
| Utility | What it does |
|---|---|
| `text-lg/7` | Font size + line-height shorthand → `font-size: 1.125rem; line-height: 1.75rem` |
| `text-[2.5rem]/10` | Custom size + line-height shorthand |
| `bg-gray-950/5` | Background with opacity → `oklch(... / 5%)` |
| `border-white/10` | Border with inline opacity |
| `inset-ring` | Inner `box-shadow` ring (replaces `ring-inset`) |
| `inset-ring-gray-950/8` | Inset ring with opacity |
| `rounded-4xl` | `border-radius: 2rem` (32px) |
| `min-h-dvh` | `min-height: 100dvh` (dynamic viewport) |
| `bg-size-[10px_10px]` | `background-size` shorthand |
| `bg-fixed` | `background-attachment: fixed` |
| `[--name:value]` | Inline CSS custom property (e.g., `[--gutter-width:2.5rem]`) |
| `data-active:...` | Style when `data-active` attribute is present |

---

## 3. Typography System (Inter Stack)

tailwindcss.com uses **Inter Variable** (UI text) and **IBM Plex Mono** (code). Font weights are variable-based.

### Font Preloading (Head)
```html
<link rel="preload" href="InterVariable.woff2" as="font" crossorigin="" type="font/woff2"/>
<link rel="preload" href="IBMPlexMono_Regular.woff2" as="font" crossorigin="" type="font/woff2"/>
<link rel="preload" href="IBMPlexMono_Medium.woff2" as="font" crossorigin="" type="font/woff2"/>
<link rel="preload" href="IBMPlexMono_SemiBold.woff2" as="font" crossorigin="" type="font/woff2"/>
```

### Typographic Scale (Responsive Hero)
```html
<!-- Self-documenting: shows the classes ABOVE the heading it styles -->
<div aria-hidden="true" class="flex h-16 items-end px-2 font-mono text-xs/6
     whitespace-pre text-black/20 dark:text-white/25">
  <span class="hidden max-sm:inline">text-4xl </span>
  <span class="hidden sm:max-md:inline">text-5xl </span>
  <span class="hidden lg:max-xl:inline">text-6xl </span>
  <span class="hidden xl:inline">text-8xl </span>
  tracking-tighter text-balance
</div>

<h1 class="px-2 text-4xl tracking-tighter text-balance
           max-lg:font-medium
           sm:text-5xl lg:text-6xl xl:text-8xl">
  Rapidly build modern websites without ever leaving your HTML.
</h1>
```

### Typography Rules
| Rule | Implementation |
|---|---|
| **Header Tightening** | All `text-3xl`+ MUST use `tracking-tighter` or `tracking-tight` |
| **Text Balance** | Multi-line headings MUST use `text-balance` |
| **Body Line Height** | Use shorthand: `text-lg/7`, `text-base/7`, `text-sm/6` |
| **Heading Line Height** | `leading-none` or `leading-tight` for `text-2xl`+ |
| **Monospace Badge** | `font-mono text-xs/6 font-semibold tracking-widest uppercase text-sky-500` |
| **Section Labels** | `font-mono text-sm font-semibold tracking-widest uppercase text-sky-500` |

### Section Label (Rotated Vertical on Large Screens)
```html
<p class="text-sky-500 dark:text-sky-400
          top-0 -left-(--gutter-width) origin-bottom-right
          font-mono text-sm font-semibold tracking-widest uppercase
          text-left
          2xl:absolute 2xl:-translate-full 2xl:-rotate-90 2xl:text-right">
  Sponsors
</p>
```
→ On `2xl` screens, this label becomes a **vertical rotated sidebar label** positioned outside the content column.

---

## 4. Visual Hierarchy Techniques

### A. Full-Viewport Horizontal Dividers (Pseudo-Element Trick)
Every section uses `::before` and `::after` pseudo-elements to draw hairline dividers that span the **full browser width** regardless of the content's max-width:
```html
<div class="relative
  before:absolute before:top-0    before:h-px before:w-[200vw] before:left-[-100vw]
  before:bg-gray-950/5 dark:before:bg-white/10
  after:absolute  after:bottom-0 after:h-px  after:w-[200vw] after:left-[-100vw]
  after:bg-gray-950/5 dark:after:bg-white/10">
  <!-- Section content -->
</div>
```
> **Pattern**: `w-[200vw]` + `left-[-100vw]` = line bleeds 100vw to the left and right of its parent.

### B. Diagonal Stripe Gutter Pattern
Side gutters (left/right of content) use a diagonal repeating pattern that adapts to dark/light via inline CSS variable:
```html
<div class="col-start-1 row-span-full row-start-1 hidden
            border-x border-x-(--pattern-fg)
            bg-[repeating-linear-gradient(315deg,var(--pattern-fg)_0,var(--pattern-fg)_1px,transparent_0,transparent_50%)]
            bg-size-[10px_10px] bg-fixed
            [--pattern-fg:var(--color-black)]/5
            md:block
            dark:[--pattern-fg:var(--color-white)]/10">
</div>
```
> **Key insight**: `[--pattern-fg:var(--color-black)]/5` sets a CSS custom property + opacity inline. Dark mode overrides it with `dark:[--pattern-fg:var(--color-white)]/10`.

### C. Glowing Mesh Grid Background (Hero)
```html
<!-- Dark mode repeating grid with radial mask -->
<div class="absolute inset-0 -z-10 h-full w-full bg-gray-950
  bg-[linear-gradient(to_right,#1e293b_1px,transparent_1px),
      linear-gradient(to_bottom,#1e293b_1px,transparent_1px)]
  bg-[size:4rem_4rem]
  [mask-image:radial-gradient(ellipse_60%_50%_at_50%_0%,#000_70%,transparent_100%)]
  opacity-80">
</div>
```

### D. Ambient Spotlight Glows
```html
<div class="absolute top-0 left-1/4 -z-10 h-[500px] w-[700px]
     rounded-full bg-sky-500/10 blur-[120px] filter animate-pulse">
</div>
<div class="absolute top-10 right-1/4 -z-10 h-[450px] w-[600px]
     rounded-full bg-violet-500/10 blur-[100px] filter animate-pulse"
     style="animation-delay: 2s;">
</div>
```

### E. Horizontal Glowing Laser Beam
```html
<div class="absolute left-0 right-0 top-32 h-[1px]
     bg-gradient-to-r from-transparent via-sky-500/40 to-transparent">
</div>
```

### F. Gradient Border Glow Cards
```html
<div class="relative group overflow-hidden rounded-2xl
     border border-gray-950/5 bg-white p-6
     transition-all duration-300
     dark:border-white/10 dark:bg-gray-900/60
     hover:-translate-y-0.5">

  <!-- Glowing gradient appears behind card on hover -->
  <div class="absolute -inset-px -z-10 rounded-2xl
       bg-gradient-to-r from-sky-500 to-indigo-500
       opacity-0 blur transition-all duration-300
       group-hover:opacity-20 group-hover:blur-md">
  </div>

  <!-- Subtle top-edge highlight -->
  <div class="absolute inset-[1px] rounded-[15px]
       bg-gradient-to-b from-white/10 to-transparent
       pointer-events-none">
  </div>

  <!-- Content -->
  <h3 class="text-lg font-semibold text-gray-950 dark:text-white mb-2">Card Title</h3>
  <p class="text-sm text-gray-500 dark:text-gray-400">Card description text.</p>
</div>
```

---

## 5. Grid & Layout System

### A. Hero / Page Grid (Tailwind v4 style)
```html
<div class="grid min-h-dvh grid-cols-1
            grid-rows-[1fr_1px_auto_1px_auto]
            justify-center pt-14.25
            [--gutter-width:2.5rem]
            md:-mx-4
            md:grid-cols-[var(--gutter-width)_minmax(0,var(--breakpoint-2xl))_var(--gutter-width)]
            lg:mx-0">
  <!-- Col 1: left stripe gutter (md:block) -->
  <!-- Col 2: main content -->
  <!-- Col 3: right stripe gutter (md:block) -->
</div>
```
> `grid-rows-[1fr_1px_auto_1px_auto]` → automatically inserts 1px divider rows between content rows without extra HTML.

### B. Responsive Multi-Column Sponsor/Card Grid
```html
<ul class="grid grid-cols-2 gap-5
           md:gap-10
           lg:grid-cols-3
           xl:grid-cols-4">
  <!-- Automatic vertical border lines using pointer-events-none overlay -->
  <div class="pointer-events-none absolute inset-0 z-10
              grid grid-cols-2 gap-10 md:gap-5
              lg:grid-cols-3 xl:grid-cols-4">
    <div class="border-r border-gray-950/5 dark:border-white/10"></div>
    <div class="border-l border-gray-950/5 lg:border-x dark:border-white/10"></div>
    <div class="border-l border-gray-950/5 max-lg:hidden xl:border-x dark:border-white/10"></div>
    <div class="border-l border-gray-950/5 max-xl:hidden dark:border-white/10"></div>
  </div>
</ul>
```

### C. 3-Column Documentation Layout
```
+-------------------------------------------------------------+
|              Sticky Header (z-10, backdrop-blur)            |
+-------------------------------------------------------------+
|  Left Sidebar  |     Center Content      |  Right TOC       |
|  w-64 fixed    |  max-w-3xl prose        |  w-64 hidden sm  |
+-------------------------------------------------------------+
```
```html
<!-- Sticky Header -->
<div class="sticky top-0 z-10 border-b border-gray-950/5 dark:border-white/10">
  <div class="bg-white dark:bg-gray-950">
    <div class="flex h-14 items-center justify-between gap-8 px-4 sm:px-6">
      <!-- nav content -->
    </div>
  </div>
</div>

<!-- Layout -->
<div class="mx-auto max-w-8xl px-4 sm:px-6 lg:px-8">
  <div class="lg:flex lg:gap-8">
    <!-- Left Sidebar -->
    <aside class="hidden lg:block lg:w-64 lg:shrink-0 py-8
                  sticky top-16 h-[calc(100vh-4rem)] overflow-y-auto">
    </aside>
    <!-- Main Content -->
    <main class="flex-grow min-w-0 max-w-3xl py-8">
    </main>
    <!-- Right TOC -->
    <nav class="hidden xl:block xl:w-64 xl:shrink-0">
    </nav>
  </div>
</div>
```

---

## 6. Responsive Design Patterns

### A. Dual-Element Mobile/Desktop Pattern
Show different elements per breakpoint — no JS needed:
```html
<!-- Desktop version (hidden on mobile) -->
<a class="max-sm:hidden inline-block rounded-4xl bg-black px-4 py-2
          text-sm/6 font-semibold text-white hover:bg-gray-800
          dark:bg-gray-700 dark:hover:bg-gray-600"
   href="/docs/installation">
  Get started
</a>

<!-- Mobile version (hidden on desktop) -->
<div class="mt-10 px-4 sm:hidden">
  <a class="w-full text-center inline-block rounded-4xl bg-black px-4 py-2
            text-sm/6 font-semibold text-white"
     href="/docs/installation">
    Get started
  </a>
</div>
```

### B. Responsive Navigation
```html
<!-- Desktop nav links -->
<div class="flex items-center gap-6 max-md:hidden">
  <a href="/docs">Docs</a>
  <a href="/blog">Blog</a>
</div>

<!-- Mobile icon-only menu -->
<div class="flex items-center gap-2.5 md:hidden">
  <button aria-label="Search">...</button>
  <button aria-label="Navigation">...</button>
</div>
```

### C. Responsive Typography Ranges (v4 range syntax)
```html
<!-- Only visible on specific breakpoint ranges -->
<span class="hidden max-sm:inline">text-4xl </span>
<span class="hidden sm:max-md:inline">text-5xl </span>
<span class="hidden lg:max-xl:inline">text-6xl </span>
<span class="hidden xl:inline">text-8xl </span>
```

### D. Container with Gutters
```html
<div class="mx-auto max-w-screen-2xl px-4 sm:px-6 lg:px-8">
```

---

## 7. Accessibility (A11y)

### A. Focus Rings (Keyboard Navigation)
```html
<button class="focus:outline-none
               focus-visible:ring-2
               focus-visible:ring-sky-500
               focus-visible:ring-offset-2
               dark:focus-visible:ring-offset-gray-950">
  Click me
</button>
```
> **NEVER** use `outline-none` without replacing with `focus-visible:ring-*`.

### B. `aria-hidden` on Decorative / Instructional Elements
```html
<!-- The class-label rows above headings are hidden from screen readers -->
<div aria-hidden="true" class="flex h-16 items-end px-2 font-mono text-xs/6
     whitespace-pre text-black/20 dark:text-white/25">
  text-8xl text-gray-950 tracking-tighter text-balance
</div>
```

### C. `aria-label` on Icon-Only Interactive Elements
```html
<a aria-label="GitHub repository" href="https://github.com/tailwindlabs/tailwindcss">
  <svg viewBox="0 0 20 20" class="size-5 fill-black/40 dark:fill-gray-400">...</svg>
</a>

<button aria-label="Search" type="button" class="inline-grid size-7 place-items-center rounded-md">
  <svg>...</svg>
</button>
```

### D. ARIA State on Interactive Menus (HeadlessUI pattern)
```html
<button
  aria-label="Select version of library"
  aria-haspopup="menu"
  aria-expanded="false"
  data-headlessui-state=""
  type="button">
  v4.3
</button>
```

### E. Custom Text Selection Colors (Theme Harmony)
```html
<div class="selection:bg-blue-100 selection:text-blue-900
            dark:selection:bg-sky-500/30 dark:selection:text-sky-200">
  Selectable content...
</div>
```

### F. Subtle Scrollbars (Prevent Layout Shifts)
```html
<div class="overflow-y-auto scrollbar-thin
            scrollbar-thumb-gray-200 dark:scrollbar-thumb-gray-800
            scrollbar-track-transparent">
  Scrollable content...
</div>
```

### G. Skip Navigation (Visually Hidden)
```html
<span hidden style="position:fixed;top:1px;left:1px;width:1px;height:0;
      padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);
      white-space:nowrap;border-width:0;display:none">
</span>
```

---

## 8. Interactive Code Editors & Tab Components

```html
<div class="overflow-hidden rounded-2xl bg-gray-950
     border border-white/10 shadow-2xl
     inset-ring inset-ring-white/10 dark:inset-ring-white/5">

  <!-- Window chrome / Tab Header -->
  <div class="flex items-center justify-between px-4 py-3
       bg-gray-950 border-b border-white/5">
    <div class="flex items-center gap-2">
      <!-- macOS-style dots -->
      <span class="size-3 rounded-full bg-white/20"></span>
      <span class="size-3 rounded-full bg-white/20"></span>
      <span class="size-3 rounded-full bg-white/20"></span>
      <!-- File name -->
      <span class="ml-4 font-mono text-xs text-gray-400">CardPreview.jsx</span>
    </div>
    <!-- Copy button -->
    <button class="text-xs text-gray-500 hover:text-gray-300 flex items-center gap-1">
      Copy
    </button>
  </div>

  <!-- Code content -->
  <div class="p-5 overflow-x-auto">
    <pre class="font-mono text-[13px]/6 *:flex *:*:max-w-none *:*:shrink-0 *:*:grow
         *:overflow-auto *:rounded-lg *:bg-white/10! *:p-5">
      <code>
        <span class="line">
          <span style="color:var(--color-pink-400)">div</span>
          <span style="color:var(--color-slate-300)"> class</span>
          <span style="color:var(--color-sky-300)">"flex p-6"</span>
        </span>
      </code>
    </pre>
  </div>
</div>
```

**Syntax Highlight Colors (from tailwindcss.com live source):**
| Token | Color variable |
|---|---|
| HTML tags | `var(--color-pink-400)` |
| Attributes | `var(--color-slate-300)` |
| Class values | `var(--color-sky-300)` |
| Text content | `var(--color-slate-50)` |
| Comments | `var(--color-slate-500)` |
| Punctuation | `var(--color-slate-400)` |

---

## 9. Button & Interactive Element Patterns

### Primary CTA Button
```html
<a class="inline-block rounded-4xl bg-black px-4 py-2
          text-sm/6 font-semibold text-white
          hover:bg-gray-800
          dark:bg-gray-700 dark:hover:bg-gray-600"
   href="/docs/installation">
  Get started
</a>
```

### CTA with Arrow Icon
```html
<a class="inline-flex items-center justify-center gap-2
          rounded-4xl bg-black px-4 py-2
          text-sm/6 font-semibold text-white
          hover:bg-gray-800 dark:bg-gray-700 dark:hover:bg-gray-600"
   href="/partners">
  Become a sponsor
  <svg fill="currentColor" viewBox="0 0 10 10" class="-mr-0.5 w-2.5">
    <path d="M4.85355 0.146423L9.70711 4.99998L4.85355 9.85353..."/>
  </svg>
</a>
```

### Version Badge Button
```html
<button class="flex items-center gap-0.5 rounded-2xl
               bg-gray-950/5 py-0.5 pr-1.5 pl-2.5
               text-xs/5 font-medium text-gray-950 tabular-nums
               hover:bg-gray-950/7.5 data-active:bg-gray-950/7.5
               dark:bg-white/10 dark:text-white
               dark:hover:bg-white/12.5 dark:data-active:bg-white/12.5"
        aria-label="Select version">
  v4.3
  <svg class="size-4 fill-gray-400"><!-- chevron --></svg>
</button>
```

### Plus/Premium Badge (Dashed Border with Corner Pins)
```html
<a href="/plus" class="group relative px-1.5 text-sm/6
                        text-sky-800 dark:text-sky-300">
  <span class="absolute inset-0 border border-dashed border-sky-300/60
               bg-sky-400/10 group-hover:bg-sky-400/15
               dark:border-sky-300/30">
  </span>
  Plus
  <!-- Corner pin SVGs (top-left, top-right, bottom-left, bottom-right) -->
  <svg width="5" height="5" viewBox="0 0 5 5"
       class="absolute top-[-2px] left-[-2px] fill-sky-300 dark:fill-sky-300/50">
    <path d="M2 0h1v2h2v1h-2v2h-1v-2h-2v-1h2z"/>
  </svg>
  <!-- repeat for other 3 corners -->
</a>
```

### Search Bar / Command Palette Trigger
```html
<button type="button"
        class="grid w-full grid-cols-[auto_1fr_auto] items-center gap-1
               rounded-full px-4 py-2 text-left
               text-sm/6 text-gray-950/50
               inset-ring inset-ring-gray-950/8
               sm:w-80
               dark:bg-white/5 dark:text-white/50 dark:inset-ring-white/15">
  <svg class="-ml-0.5 size-4 fill-gray-600 dark:fill-gray-500"><!-- search icon --></svg>
  Quick search
  <kbd class="font-sans text-xs/4 text-gray-500 dark:text-gray-400">
    <span class="opacity-60">Ctrl</span> K
  </kbd>
</button>
```

---

## 10. Dark Mode Implementation

### Theme Color Meta Tags (JavaScript-driven)
tailwindcss.com changes `<meta name="theme-color">` dynamically:
```js
// Dark mode  → oklch(.13 .028 261.692)
// Light mode → white
// System     → both with media queries
function updateTheme(theme) {
  document.documentElement.classList.remove("light", "dark", "system");
  if (theme === 'dark') {
    document.documentElement.classList.add('dark');
    // append meta theme-color: 'oklch(.13 .028 261.692)'
  }
}
try { _updateTheme(localStorage.currentTheme) } catch (_) {}
```

### Dark Mode Image Swap Pattern
```html
<!-- Light mode image -->
<img class="dark:hidden" src="dark-mode-light.png" alt="Light mode preview"/>
<!-- Dark mode image -->
<img class="hidden dark:block" src="dark-mode-dark.png" alt="Dark mode preview"/>
```

### Dark Mode Class Priority Strategy
```html
<!-- Use dark: prefix consistently -->
<div class="bg-white dark:bg-gray-950
            text-gray-950 dark:text-white
            border-gray-950/5 dark:border-white/10">
```

---

## 11. Common Pitfalls & Anti-Patterns

1. **Using `slate-*` instead of `gray-*`**: Tailwind v4 uses `gray-950` as the darkest neutral, not `slate-950`.

2. **Harsh Grid Borders**: Using `border-gray-500` for layout lines. → Use soft opacity: `border-gray-950/5` or `border-white/10`.

3. **Missing Focus Outlines**: Removing `outline` without replacing. → Always add `focus-visible:ring-2 focus-visible:ring-sky-500 focus-visible:ring-offset-2 dark:focus-visible:ring-offset-gray-950`.

4. **Wrong rounded corners**: Using `rounded` (4px) on large cards. → Use `rounded-2xl` (16px) or `rounded-3xl` (24px). Buttons use `rounded-4xl` (32px = pill-like).

5. **Ignoring `text-balance`**: Large headings wrap awkwardly without it. → Always add `text-balance` to multi-line headings.

6. **Skipping line-height shorthand**: Writing `text-lg leading-7` separately. → Use `text-lg/7` in Tailwind v4.

7. **No `aria-hidden` on decorative text**: Screen readers read class-label decorations as content. → Always `aria-hidden="true"` on visual-only instructional elements.

8. **Missing `aria-label` on icon buttons/links**: Icon-only elements must have `aria-label`. → Every `<button>` or `<a>` with only an SVG child needs `aria-label`.

9. **Arbitrary spacing values**: Using `p-[17px]` or `m-7`. → Stick to the Tailwind spacing scale (`p-4`, `p-5`, `p-6`) for visual harmony.

10. **Ignoring Selection & Scrollbar states**: Default blue browser highlights break dark mode palette. → Always add `selection:bg-*` and custom scrollbar classes.
