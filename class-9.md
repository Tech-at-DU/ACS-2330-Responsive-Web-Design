# Class 9: Tailwind CSS

For the first half of this course you built responsive layouts with vanilla CSS — media queries, Flexbox, Grid, display toggling. Tailwind CSS does all of the same things using utility classes applied directly in HTML. The concepts don't change. The syntax does.

This is intentional. Understanding what `md:flex-row` means requires knowing what `@media (min-width: 768px) { flex-direction: row }` means. You know that now.

## Objectives

- Install and configure Tailwind in a React/Vite project
- Read and write Tailwind utility classes
- Use responsive prefixes to replace media queries
- Rebuild SFPOPOS layout sections using Tailwind

---

## Setup

Install Tailwind in your React/Vite project:

```bash
npm install tailwindcss @tailwindcss/vite
```

Add the Tailwind plugin to `vite.config.js`:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
})
```

Add this import to your main CSS file (e.g. `index.css`):

```css
@import "tailwindcss";
```

For other project types or the latest instructions: https://tailwindcss.com/docs/installation

**Important:** Tailwind's base styles will reset some of your existing CSS. When adding Tailwind to an existing project, audit your styles — you'll likely need to recreate some of them using Tailwind classes. Mixing vanilla CSS and Tailwind is possible but can cause conflicts.

---

## Utility Classes

Tailwind styles elements through classes applied directly in HTML or JSX. Each class maps to one or a few CSS properties.

```jsx
<p className="text-2xl font-bold underline">Hello World</p>
```

Equivalent vanilla CSS:

```css
p {
  font-size: 1.5rem;
  font-weight: 700;
  text-decoration: underline;
}
```

There is no separate CSS file — the classes are the styles. When you don't know a class name, search the Tailwind docs: https://tailwindcss.com

---

## Vanilla CSS → Tailwind Translation

You already know these patterns in vanilla CSS. Here's how they map to Tailwind:

| Vanilla CSS | Tailwind class |
|-------------|---------------|
| `display: flex` | `flex` |
| `flex-direction: column` | `flex-col` |
| `flex-direction: row` | `flex-row` |
| `flex-wrap: wrap` | `flex-wrap` |
| `justify-content: space-between` | `justify-between` |
| `align-items: center` | `items-center` |
| `flex: 1` | `flex-1` |
| `display: grid` | `grid` |
| `grid-template-columns: repeat(3, 1fr)` | `grid-cols-3` |
| `gap: 1rem` | `gap-4` |
| `display: none` | `hidden` |
| `display: block` | `block` |
| `width: 100%` | `w-full` |
| `min-height: 100vh` | `min-h-screen` |
| `padding: 1rem` | `p-4` |
| `margin: 0 auto` | `mx-auto` |

Tailwind uses a spacing scale where `4` = `1rem`, `2` = `0.5rem`, `8` = `2rem`, etc.

---

## Responsive Prefixes

This is the key concept. Tailwind breakpoints are `min-width` based — mobile first, exactly like the media queries you wrote in class-3.

| Prefix | Min-width | Equivalent media query |
|--------|-----------|----------------------|
| *(none)* | all sizes | default styles |
| `sm:` | 640px | `@media (min-width: 640px)` |
| `md:` | 768px | `@media (min-width: 768px)` |
| `lg:` | 1024px | `@media (min-width: 1024px)` |
| `xl:` | 1280px | `@media (min-width: 1280px)` |

Prefix any utility class with a breakpoint to apply it only at that size and above:

```html
<!-- Stack on mobile, side by side on tablet and up -->
<div class="flex flex-col md:flex-row gap-4">
  <div>Left</div>
  <div>Right</div>
</div>
```

This is `flex-direction: column` by default, switching to `flex-direction: row` at `768px`. That's the stack-to-row pattern from class-4, in one line.

---

## Key Patterns in Tailwind

### Responsive Grid

```jsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  {spaces}
</div>
```

1 column on mobile, 2 on tablet, 3 on desktop.

### Hide and Show

```html
<!-- Hamburger: visible on mobile, hidden on desktop -->
<button class="block md:hidden">☰</button>

<!-- Full nav: hidden on mobile, visible on desktop -->
<nav class="hidden md:flex">...</nav>
```

`hidden` = `display: none`. `md:flex` overrides it at 768px.

### Container

Tailwind's `container` sets `max-width` to match the current breakpoint. Add `mx-auto` to center it:

```html
<div class="container mx-auto px-4">
  <!-- content constrained to breakpoint width, centered -->
</div>
```

### Sticky Footer

Same structure as class-4, Tailwind classes instead of CSS:

```jsx
<div className="flex flex-col min-h-screen">
  <div className="flex-1">
    <Title />
    <Outlet />
  </div>
  <Footer />
</div>
```

`flex-1` on the content div grows it to fill available space, pushing the footer to the bottom.

### NavLink with Tailwind

React Router's `NavLink` uses a function for `className`. Concatenate base classes with active/inactive conditionals:

```jsx
<NavLink
  className={({ isActive }) =>
    'block px-3 py-2 ' + (isActive ? 'font-bold text-white' : 'font-normal text-slate-300')
  }
  to="/"
>
  List
</NavLink>
```

Note the space after `py-2` — required to separate from the next class string.

---

## Challenge: Rebuild SFPOPOS with Tailwind

Apply Tailwind to your SFPOPOS project. Work through these in order:

1. **Install Tailwind** and verify it's working (add a `text-red-500` class to any element — if it turns red, Tailwind is active)
2. **Spaces grid** — replace CSS grid with Tailwind responsive grid classes
3. **Header/Nav** — replace Flexbox CSS with Tailwind flex classes
4. **Sticky footer** — replace CSS with Tailwind flex classes
5. **NavLink active styles** — use the function pattern above

Test at 375px (mobile) and 1024px (desktop) after each step.

**Stretch challenge:** Style the hamburger button from class-8 using only Tailwind classes. Remove its CSS file entirely.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Setup | Tailwind not working or base styles broken | Tailwind installed and applying styles correctly | Old conflicting CSS removed or reconciled |
| Responsive grid | Grid not responsive or uses vanilla CSS | Tailwind responsive grid classes applied, correct column counts per breakpoint | `gap`, `container`, `mx-auto` used appropriately |
| Flex layout | Header or footer layout broken | Flexbox layout rebuilt with Tailwind, matches vanilla CSS result | Responsive direction changes use prefix classes correctly |
| Hide/show | Hamburger and full nav visible simultaneously | Correct show/hide at breakpoint using `hidden` and `md:flex` | All responsive display changes use Tailwind prefix classes |
