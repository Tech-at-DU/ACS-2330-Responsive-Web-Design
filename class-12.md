# Class 12: Modern Responsive CSS

This class covers three modern CSS features that solve problems you've already encountered — stepped font sizes, fixed viewport units on mobile, and components that don't know how wide their container is. These are all browser-supported and increasingly expected on production sites.

## Objectives

- Use `clamp()` to create fluid typography that scales smoothly between breakpoints
- Use `min()` and `max()` for flexible sizing without media queries
- Use dynamic viewport units to fix mobile browser chrome issues
- Understand container queries and when to reach for them
- Apply any of the above to Project 2

---

## The Problem with Stepped Font Sizes

In class-3 you wrote font-size media queries like this:

```css
body { font-size: 16px; }

@media (min-width: 768px) {
  body { font-size: 18px; }
}

@media (min-width: 1024px) {
  body { font-size: 20px; }
}
```

This creates steps — the font jumps at each breakpoint. Between 768px and 1024px the font stays 18px regardless of how much space is available. On a 500px screen it jumps immediately to 18px even though there's not much more room than at 400px.

`clamp()` solves this with smooth, continuous scaling.

---

## `clamp()` — Fluid Typography

`clamp(min, preferred, max)` sets a value that:
- Never goes below `min`
- Scales fluidly based on the `preferred` value
- Never exceeds `max`

```css
h1 {
  font-size: clamp(1.5rem, 5vw, 3rem);
}
```

At 320px wide: `5vw = 16px = 1rem` — clamp holds at `1.5rem` minimum.
At 768px wide: `5vw = 38.4px = 2.4rem` — scales freely.
At 1200px wide: `5vw = 60px = 3.75rem` — clamp holds at `3rem` maximum.

The font scales smoothly across the entire range without a single media query.

### Practical formula

The `vw` unit alone doesn't account for a fixed base. A more reliable approach mixes `rem` and `vw`:

```css
/* clamp(minimum, base + scale, maximum) */
h1 { font-size: clamp(1.75rem, 1rem + 3vw, 3.5rem); }
h2 { font-size: clamp(1.5rem,  1rem + 2vw, 2.5rem); }
h3 { font-size: clamp(1.25rem, 1rem + 1vw, 2rem); }
p  { font-size: clamp(1rem,    0.9rem + 0.5vw, 1.25rem); }
```

The `1rem + 3vw` part means: start at 1rem, grow by 3% of the viewport width. This tends to feel natural at all sizes.

### With Tailwind

Tailwind doesn't have built-in `clamp()` utilities, but you can use arbitrary values:

```html
<h1 class="text-[clamp(1.75rem,1rem+3vw,3.5rem)]">
  Fluid Heading
</h1>
```

Or define it in a CSS file alongside your Tailwind import and apply a custom class.

---

## `min()` and `max()`

These functions are simpler versions of `clamp()` — pick the smaller or larger of two values.

### `min()` — never exceeds the smaller value

```css
/* Full width but never more than 600px */
.container {
  width: min(100%, 600px);
}
```

This replaces the common pattern `width: 100%; max-width: 600px` — in one property.

### `max()` — never goes below the larger value

```css
/* At least 44px tall regardless of content */
button {
  height: max(44px, 2.75rem);
}

/* Font never smaller than 1rem */
p {
  font-size: max(1rem, 1.5vw);
}
```

### Combining with Tailwind

```html
<!-- Max-width container that fills width on mobile -->
<div class="w-[min(100%,600px)] mx-auto px-4">
```

---

## Dynamic Viewport Units

You've used `100vh` for full-screen sections. On mobile, this breaks.

**The problem:** On iOS, the browser URL bar collapses as you scroll, changing the actual visible height. `100vh` is calculated including the URL bar in its expanded state — so a `100vh` element is taller than the screen when the page loads.

```
┌──────────────────┐  ← top of screen
│   URL bar (50px) │
├──────────────────┤
│                  │
│  100vh starts    │
│  here (wrong)    │
│                  │
│                  │
└──────────────────┘  ← 100vh ends here (below fold)
```

**The fix — dynamic viewport units:**

| Unit | Meaning | Use when |
|------|---------|----------|
| `dvh` | Dynamic viewport height — updates as browser chrome appears/disappears | Hero sections, full-screen layouts |
| `svh` | Small viewport height — uses the *smallest* viewport (chrome fully visible) | Safe minimum — always fits |
| `lvh` | Large viewport height — uses the *largest* viewport (chrome hidden) | Intentional full-bleed |

```css
/* Before — breaks on mobile */
.hero {
  min-height: 100vh;
}

/* After — works correctly */
.hero {
  min-height: 100dvh;
}
```

**Tailwind:** No built-in `dvh` classes yet, use arbitrary values:

```html
<section class="min-h-[100dvh]">
```

If you've implemented a sticky footer with `min-h-screen` (which maps to `100vh`), replace it with `min-h-[100dvh]` for correct mobile behavior.

---

## Container Queries

Media queries are based on the **viewport** width. Container queries are based on the **parent container** width.

**Why this matters:** A card component sitting in a sidebar (300px wide) needs different styling than the same card in a three-column grid (400px wide) — even though the viewport is the same. Media queries can't distinguish these cases. Container queries can.

### Setup

Mark the parent as a container:

```css
.card-container {
  container-type: inline-size;  /* enables width-based queries */
  container-name: card;         /* optional name for targeting */
}
```

Then query the container in the child's styles:

```css
.card {
  display: flex;
  flex-direction: column;  /* default: stacked */
}

@container (min-width: 400px) {
  .card {
    flex-direction: row;   /* side by side when container is wide enough */
  }
}
```

### Example — the same card in two contexts

```html
<!-- Sidebar: card-container is 280px — card stays stacked -->
<aside class="sidebar">
  <div class="card-container">
    <div class="card">...</div>
  </div>
</aside>

<!-- Main content: card-container is 480px — card goes side by side -->
<main>
  <div class="card-container">
    <div class="card">...</div>
  </div>
</main>
```

Both use the same `.card` CSS. The layout adapts to available space, not viewport size. This is the component-based approach to responsiveness — the card "just works" wherever you drop it.

### Container queries vs media queries

| | Media query | Container query |
|-|-------------|----------------|
| Based on | Viewport width | Parent element width |
| Good for | Full-page layout changes | Reusable components |
| Support | Universal | All modern browsers (2023+) |

Use both. Media queries for macro layout (sidebar appears at desktop). Container queries for micro layout (what's inside the sidebar adapts to its width).

### With Tailwind

Tailwind v3.2+ supports container queries via the `@tailwindcss/container-queries` plugin:

```bash
npm install @tailwindcss/container-queries
```

```html
<div class="@container">
  <div class="flex flex-col @md:flex-row">
    <!-- stacks by default, row when container ≥ 768px -->
  </div>
</div>
```

---

## Project 2 Lab

Apply what you've learned today to Project 2. Suggested targets:

1. **Replace stepped heading sizes** with `clamp()` on your `h1` and `h2` elements
2. **Fix any `100vh` usage** — replace with `100dvh` for correct mobile behavior
3. **Apply container queries** to any reusable card or content component — especially useful if your layout has components appearing in different width contexts
4. **Review your full Project 2 checklist:**
   - Responsive on mobile, tablet, and desktop
   - Tailwind responsive prefixes used throughout
   - Hamburger menu working with ARIA
   - Forms accessible and touch-friendly (if applicable)
   - Lighthouse accessibility ≥ 90
   - UX test findings applied

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Fluid typography | Stepped font sizes only | `clamp()` applied to at least heading sizes | Applied to headings and body, formula is calibrated (not too large on mobile, not too small on desktop) |
| Viewport units | `100vh` causing mobile layout issues | `100dvh` used for full-screen elements | Understands difference between `dvh`, `svh`, and `lvh` and uses each appropriately |
| Container queries | Not attempted | Container type set, `@container` query applies at least one layout change | Reusable component adapts correctly in two different container widths |
| Project 2 progress | Significant requirements unmet | On track — responsive layout working, Tailwind throughout | Checklist complete, ready for final presentation |
