---
name: tailwind-ux-ui
description: |
  A comprehensive reference and design guidelines skill for implementing the premium, developer-centric UX/UI design system of tailwindcss.com.
  Use this skill when designing web interfaces, dashboards, documentation, and frontend components to ensure high-end aesthetics.
license: Apache-2.0
metadata:
  version: v1
  publisher: user-custom
---

# Tailwind CSS Premium UX/UI Design System Guide

This skill provides a deep, comprehensive guidelines and implementation ruleset for crafting web applications that match the premium visual design, layout architectures, and UX details of the official **tailwindcss.com** site.

---

## 1. Core Principles (Refactoring UI Philosophy)

The Tailwind aesthetic is founded on **systematic constraints**. Avoid arbitrary choices; rely on a strict set of design tokens to establish visual hierarchy, readability, and high-end polish.

1. **Design in Grayscale First**: Establish layout, spacing, sizes, and font-weights before adding color. If a layout doesn't look clear in grayscale, color will not fix it.
2. **De-emphasize, Don't Just Amplify**: To make something stand out, make the surrounding elements less prominent (e.g., reduce their font size, change text from `text-slate-900` to `text-slate-500`) instead of making the target element larger or brighter.
3. **Treat CSS Classes as Implementation Details**: Define component-level clean boundaries (React/Vue/HTML components) using strict Tailwind configurations rather than inline chaotic styles (e.g., expose `<Button variant="primary">` instead of writing raw button utility blocks everywhere).

---

## 2. Spacing & Rhythm (The 4px Grid System)

Tailwind uses a logical `0.25rem = 4px` spacing scale. All components should align to this vertical and horizontal rhythm.

### Recommended Spacing Scale
- **Micro-spacing (2px–8px)**: `0.5` (2px), `1` (4px), `2` (8px). Use for compact list items, button-to-icon gaps, checkbox alignments, and small badges.
- **Normal Padding & Gaps (12px–24px)**: `3` (12px), `4` (16px), `5` (20px), `6` (24px). Use for standard button paddings, card interior spacing, and input spacing.
- **Layout Spacing (32px–64px+)**: `8` (32px), `10` (40px), `12` (48px), `16` (64px). Use for margins between large sections, container page paddings, and hero layouts.

### Spacing Rules
* **Consistent Padding Ratio**: Use wider horizontal padding than vertical padding for interactive components (e.g., Buttons: `px-4 py-2` or `px-5 py-2.5`; Inputs: `px-3.5 py-2`).
* **Layout Flex & Grid**: Default to `gap-*` (e.g., `gap-4`, `gap-6`, `gap-8`) for flex/grid containers instead of applying margins to child components. This guarantees consistent rhythm.

---

## 3. The Typography System (Scale & Letter Spacing)

Typography must look sharp and intentional. Adjust letter-spacing (tracking) and line-height (leading) dynamically based on the font size.

### Typography Scale & Details
| Size Class | Pixel Equivalent | Recommended Tracking | Recommended Leading | Primary Use Case |
| :--- | :--- | :--- | :--- | :--- |
| `text-xs` | 12px | `tracking-wide` | `leading-4` (16px) | Badges, Helper Text, Captions |
| `text-sm` | 14px | `tracking-normal` | `leading-5` (20px) | Body Text, Button Labels, Inputs |
| `text-base` | 16px | `tracking-normal` | `leading-6` (24px) | Article Body, Large Lists |
| `text-lg` | 18px | `tracking-tight` | `leading-7` (28px) | Subheadings, Intro Paragraphs |
| `text-xl` | 20px | `tracking-tight` | `leading-7` (28px) | Card Titles, Small Section Titles |
| `text-2xl` | 24px | `tracking-tight` | `leading-8` (32px) | Section Headings |
| `text-3xl` | 30px | `tracking-tight` | `leading-9` (36px) | Page Titles, Hero Subtitles |
| `text-4xl` | 36px | `tracking-tighter` | `leading-10` (40px) | Main Landing Headers |
| `text-5xl` to `9xl` | 48px to 128px | `tracking-tighter` | `leading-none` to `leading-tight` | Display text, Large Stats |

### Typography Guidelines
* **The "Tightening" Rule**: As font size increases, **always** reduce tracking. Text sizing `text-3xl` and above **MUST** use `tracking-tight` or `tracking-tighter`.
* **The "Monospace" Rule**: All uppercase or monospace label text (e.g., `font-mono text-xs uppercase`) **MUST** use `tracking-wider` or `tracking-widest` to remain readable.
* **Readable Body Width**: Restrict body text columns to a maximum width of `max-w-2xl` or `max-w-3xl` (approx. 60–80 characters per line) to prevent eye strain.

---

## 4. The Color System (Semantics & Contrast)

Tailwind CSS uses a shade scale from 50 (lightest) to 950 (darkest). High-end UIs use specific gray palettes and well-tinted accents.

### Recommended Gray Families
* **Slate (`slate`)**: Neutral gray with a cool blue undertone. Best for tech, SaaS, and developer portals (matches tailwindcss.com).
* **Zinc (`zinc`)**: Extremely neutral, modern, clean gray. Best for minimalist, high-end design systems.
* **Gray (`gray`)**: Classic, balanced gray. Safe choice for most standard applications.

### Dynamic Contrast Ratios
To achieve WCAG AA compatibility and premium aesthetics, follow these pairing scales:
* **Light Mode Base**:
  - Background: `bg-slate-50` or `bg-white`
  - Main Heading: `text-slate-900`
  - Body Text: `text-slate-700`
  - Secondary/Muted: `text-slate-500`
  - Borders: `border-slate-200` (or `border-slate-100` for inner grids)
* **Dark Mode Base**:
  - Background: `bg-slate-950` or `bg-zinc-950`
  - Main Heading: `text-slate-100`
  - Body Text: `text-slate-300`
  - Secondary/Muted: `text-slate-400`
  - Borders: `border-slate-800` (or `border-white/5`)

### Accent Tints & Interactive States
* **Primary Accent Color**: Select a vibrant primary (e.g., Indigo `bg-indigo-600`, Violet `bg-violet-600`, or Sky `bg-sky-500`).
* **Active State Modifiers**:
  - Hover: Darken/brighten by 100 steps (e.g., `bg-indigo-600 hover:bg-indigo-700` in light mode).
  - Focus Ring: Always add a visible ring on keyboard focus: `focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2 focus-visible:outline-none`.

---

## 5. Elevation, Borders & Glassmorphism

Avoid harsh dark borders. Utilize soft, natural-looking shadows and borders to create depth and structure.

### Elevation (Shadows)
* **Flat Surfaces**: No shadow, soft border `border border-slate-200/80` or `bg-slate-50`.
* **Low Elevation (Buttons, Input Fields)**: `shadow-sm` or `shadow`.
* **Medium Elevation (Cards, Dropdowns)**: `shadow-md` or `shadow-lg shadow-slate-200/50`.
* **High Elevation (Modals, Overlays)**: `shadow-xl` or `shadow-2xl`.
* **Soft Shadows**: Always blend shadows with light mode colors. Add opacity modifiers to make shadows softer: `shadow-slate-200/50` or `shadow-indigo-500/10`.

### Radii & Borders
* **Card Roundedness**: Use `rounded-xl` (12px) or `rounded-2xl` (16px) for cards, dialogs, and sections.
* **Component Roundedness**: Use `rounded-lg` (8px) for buttons, inputs, and list items.
* **Badges/Chips**: Use `rounded-full` for badges, tags, and avatars.
* **Inner Radii Rule**: When nesting elements, the outer element's radius should be larger than the inner element's radius (`outer_radius = inner_radius + padding`).

### Glassmorphism (Blur Effects)
Create premium, overlay panels using background opacity combined with backdrop blur:
- Class combination: `bg-white/80 backdrop-blur-md border border-slate-200/50` (Light mode)
- Class combination: `bg-slate-950/70 backdrop-blur-md border border-white/5` (Dark mode)

---

## 6. Dark Mode Architecture

Tailwind CSS dark mode uses the `dark:` prefix. Build a deep, glowing slate/zinc environment instead of a flat black look.

### Checklist for Dark Mode
1. **Background Hierarchy**:
   - Page Background: `bg-slate-950`
   - Card Background: `bg-slate-900/50` or `bg-slate-900`
   - Inner Items (table rows, inputs): `bg-slate-950/50` or `bg-slate-900/30`
2. **Text Hierarchy**:
   - Title: `dark:text-white`
   - Body: `dark:text-slate-300`
   - Muted Labels: `dark:text-slate-400`
3. **Borders**:
   - Replace gray borders with thin, transparent white borders: `dark:border-white/10` or `dark:border-slate-800`.
4. **Accent Glows**:
   - Use radial glows on cards: `bg-radial-glow` using background-gradients and radial-masking (see code template below).

---

## 7. Transitions & Micro-Interactions

An interface feels alive when interactions are smooth. Always add micro-animations for hover, focus, and state transitions.

* **Transition Standard**: Apply `transition-all duration-200 ease-in-out` (or `duration-150`) to any element that changes color, shadow, or transform on hover.
* **Transformations on Hover**:
  - Translate upward slightly: `hover:-translate-y-0.5`
  - Scale up slightly: `hover:scale-[1.015]`
  - Shadow expansion: `shadow-md hover:shadow-xl`
* **Interactive Lists**: When items in a list are clickable, show a subtle hover background: `hover:bg-slate-50 dark:hover:bg-slate-900/50`.

---

## 8. Premium Visual Details (Tailwind CSS Signature Glows)

The Tailwind website is famous for its glowing grids and neon radial gradients. You can implement these details using simple utility classes.

### SVG Grid Backdrop Pattern
Create a mesh grid backdrop with a fading radial mask:
```html
<div class="absolute inset-0 -z-10 h-full w-full bg-white bg-[radial-gradient(#e2e8f0_1px,transparent_1px)] [background-size:16px_16px] [mask-image:radial-gradient(ellipse_50%_50%_at_50%_50%,#000_70%,transparent_100%)]"></div>
```
For dark mode:
```html
<div class="absolute inset-0 -z-10 h-full w-full bg-slate-950 bg-[radial-gradient(#1e293b_1px,transparent_1px)] [background-size:24px_24px] [mask-image:radial-gradient(ellipse_60%_50%_at_50%_50%,#000_60%,transparent_100%)]"></div>
```

### Neon Radial Glow Background
Create a soft color wash background element:
```html
<div class="absolute top-0 left-1/4 -z-10 h-[400px] w-[600px] rounded-full bg-indigo-500/10 blur-[120px] filter"></div>
<div class="absolute top-20 right-1/4 -z-10 h-[350px] w-[500px] rounded-full bg-purple-500/10 blur-[100px] filter"></div>
```

---

## 9. Code Templates (Copy-Paste Ready Components)

### A. The Classic 3-Column Documentation Layout
```html
<div class="min-h-screen bg-white text-slate-900 dark:bg-slate-950 dark:text-slate-100 flex flex-col">
  <!-- Top Navigation Header -->
  <header class="sticky top-0 z-40 w-full border-b border-slate-200 bg-white/80 backdrop-blur-md dark:border-slate-800 dark:bg-slate-950/80">
    <div class="mx-auto flex h-16 max-w-8xl items-center justify-between px-4 sm:px-6 lg:px-8">
      <div class="flex items-center gap-6">
        <span class="text-xl font-bold tracking-tight text-slate-900 dark:text-white flex items-center gap-2">
          <div class="h-6 w-6 rounded-md bg-gradient-to-tr from-indigo-500 to-violet-500"></div>
          BrandConsole
        </span>
      </div>
      <div class="flex items-center gap-4">
        <!-- Command Search Bar Mockup -->
        <button class="hidden lg:flex items-center gap-3 rounded-lg border border-slate-200 bg-slate-50 px-3 py-1.5 text-sm text-slate-400 hover:border-slate-300 dark:border-slate-800 dark:bg-slate-900/50 dark:hover:border-slate-700">
          <svg class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
          Search documentation...
          <kbd class="font-sans font-semibold text-xs text-slate-400 bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 px-1.5 py-0.5 rounded">Ctrl K</kbd>
        </button>
      </div>
    </div>
  </header>

  <!-- Sidebar & Grid Area -->
  <div class="mx-auto w-full max-w-8xl flex-grow lg:flex px-4 sm:px-6 lg:px-8">
    <!-- Left Navigation Sidebar -->
    <aside class="hidden lg:block lg:w-64 lg:shrink-0 border-r border-slate-200 dark:border-slate-900 pr-6 py-8 sticky top-16 h-[calc(100vh-4rem)] overflow-y-auto">
      <nav class="space-y-8">
        <div>
          <h3 class="text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-3">Getting Started</h3>
          <ul class="space-y-2">
            <li><a href="#" class="block text-sm font-medium text-indigo-600 dark:text-indigo-400">Introduction</a></li>
            <li><a href="#" class="block text-sm text-slate-600 hover:text-slate-900 dark:text-slate-400 dark:hover:text-slate-100 transition-colors">Installation</a></li>
            <li><a href="#" class="block text-sm text-slate-600 hover:text-slate-900 dark:text-slate-400 dark:hover:text-slate-100 transition-colors">Configuration</a></li>
          </ul>
        </div>
      </nav>
    </aside>

    <!-- Main Content Area -->
    <main class="flex-grow min-w-0 lg:px-8 py-8">
      <div class="max-w-3xl">
        <h1 class="text-3xl font-bold tracking-tight text-slate-900 dark:text-white sm:text-4xl mb-4">Core Architecture</h1>
        <p class="text-lg text-slate-600 dark:text-slate-400 leading-relaxed mb-6">Learn how to customize and scale your design using utility classes.</p>
        <div class="rounded-xl border border-slate-200/80 bg-slate-50/50 p-6 dark:border-slate-800 dark:bg-slate-900/30">
          <p class="text-sm leading-relaxed text-slate-700 dark:text-slate-300">Inner documentation card example content.</p>
        </div>
      </div>
    </main>

    <!-- Right Sidebar Table of Contents -->
    <aside class="hidden xl:block xl:w-64 xl:shrink-0 pl-6 py-8 sticky top-16 h-[calc(100vh-4rem)] overflow-y-auto">
      <h3 class="text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-3">On this page</h3>
      <ul class="space-y-2.5 text-sm border-l border-slate-200 dark:border-slate-800 pl-4">
        <li><a href="#" class="block text-slate-500 hover:text-slate-900 dark:text-slate-400 dark:hover:text-slate-100 transition-colors">Overview</a></li>
        <li><a href="#" class="block text-slate-500 hover:text-slate-900 dark:text-slate-400 dark:hover:text-slate-100 transition-colors">Quick start guide</a></li>
        <li><a href="#" class="block text-slate-500 hover:text-slate-900 dark:text-slate-400 dark:hover:text-slate-100 transition-colors">Configuration properties</a></li>
      </ul>
    </aside>
  </div>
</div>
```

### B. Premium Interactive Card with Glow
```html
<div class="relative group overflow-hidden rounded-2xl border border-slate-200/80 bg-white p-6 transition-all duration-300 ease-in-out hover:-translate-y-1 hover:shadow-xl hover:shadow-slate-200/50 dark:border-slate-800 dark:bg-slate-900 dark:hover:border-slate-700/80 dark:hover:shadow-indigo-500/5">
  <!-- Subtle glowing overlay on hover -->
  <div class="absolute -inset-px -z-10 rounded-2xl bg-gradient-to-r from-indigo-500 to-violet-500 opacity-0 blur transition-all duration-300 group-hover:opacity-10 group-hover:blur-md"></div>
  
  <div class="flex items-center gap-4 mb-4">
    <div class="flex h-10 w-10 items-center justify-between rounded-lg bg-indigo-50/80 text-indigo-600 dark:bg-indigo-950/50 dark:text-indigo-400 pl-2.5">
      <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
    </div>
    <h3 class="text-lg font-semibold tracking-tight text-slate-900 dark:text-white">API Acceleration</h3>
  </div>
  <p class="text-sm text-slate-600 dark:text-slate-400 leading-relaxed mb-4">Speed up your backend deployments globally with edge database routing.</p>
  <div class="flex items-center gap-1.5 text-sm font-semibold text-indigo-600 dark:text-indigo-400 group-hover:text-indigo-700 dark:group-hover:text-indigo-300 transition-colors">
    Explore feature
    <svg class="h-4 w-4 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
  </div>
</div>
```

---

## 10. Common Pitfalls & Anti-Patterns

1. **Harsh Pure Colors**: Using `bg-black` or `text-black` on bright backgrounds, or `border-gray-500` for layout borders. Instead, use soft opacity tints (e.g., `border-slate-200` or `border-slate-800`).
2. **Missing Focus Rings**: Relying on default browser blue focus outlines or removing focus outlines entirely. Use `focus-visible:ring-2 focus-visible:ring-indigo-500` for polished focus indications.
3. **Random Unconstrained Values**: Using classes like `h-[340px]`, `w-[512px]`, or `p-[17px]`. Instead, stick to standard spacing increments like `h-80`, `w-128`, or `p-4` to preserve the visual system integrity.
4. **Header Scale Inconsistencies**: Setting headings to large sizes (`text-3xl` or `text-4xl`) but keeping letter spacing wide (`tracking-normal`). Remember: large fonts require **tight** letter-spacing (`tracking-tight` or `tracking-tighter`).
