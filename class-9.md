# Class 9: Tailwind CSS

For the first half of this course you built responsive layouts with vanilla CSS — media queries, Flexbox, Grid, display toggling. Tailwind CSS does all of the same things using utility classes applied directly in HTML. The concepts don't change. The syntax does.

This is intentional. Understanding what `md:flex-row` means requires knowing what `@media (min-width: 768px) { flex-direction: row }` means. You know that now.

## Objectives

- Install and configure Tailwind in a React/Vite project
- Read and write Tailwind utility classes
- Use responsive prefixes to replace media queries
- Rebuild SFPOPOS layout sections using Tailwind

---

## Before You Start: Lock In Your Vanilla CSS Version

You should have a finished vanilla CSS version of SFPOPOS from classes 3–8 — media queries, Flexbox, Grid, accessibility, and the hamburger menu all working. Before touching Tailwind, commit and push any last changes, then submit a link to that commit to Gradescope.

**How to get the commit link:**
1. `git add .` / `git commit -m "Finish vanilla CSS version"` / `git push`
2. On GitHub, open that commit and copy its URL (it looks like `github.com/you/sfpopos/commit/<hash>`)
3. Submit that link to Gradescope — this is your checkpoint for the CSS/accessibility/hamburger work graded by the Final Rubric in class-8

**Keep working in the same repo.** Don't fork or start a new project for Tailwind — you're converting this codebase in place, on top of that commit. The commit link is just a marker so your pre-Tailwind work is graded separately from what you build today.

**Why a commit link, not a new repo:** every commit has a unique hash — a permanent, unchangeable pointer to exactly what your code looked like at that moment. Linking to that commit (rather than just "the repo" or "the main branch") means the grader sees the exact state you're claiming credit for, even after you've pushed 50 more commits converting things to Tailwind. The repo keeps moving; the commit link doesn't.

This is standard practice on real engineering teams: tagging a release (`v1.2.0`), linking a specific commit in a status update, or pointing a code reviewer at the commit before a risky refactor so they can diff against it later. A pull request works the same way — it's a link to a fixed set of commits, not a vague pointer at "the branch." Get comfortable grabbing a commit URL now; you'll do it constantly once you're working on a team.

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

## End of Class Checkpoint

Before you leave, confirm Tailwind is working in your SFPOPOS project:
- Add `text-red-500` to any element — it should turn red
- Your spaces grid should show 1 column at 375px (mobile) and 3 columns at 1024px (desktop)
- Header nav should use Tailwind flex classes, not the old CSS

**This is your Assignment 3 submission.** Push your final commit and submit that commit's link to Gradescope — same repo as the vanilla CSS commit you submitted at the start of class, just further along. Your site should be responsive using Tailwind — the vanilla CSS you wrote in classes 3–5 should be replaced with Tailwind responsive prefixes.

---

## Assignment 3: Final Rubric (Whole Site)

You saw this in class-8. It covers everything built across classes 3–9, not just today's Tailwind work — use it as your final check before submitting to Gradescope.

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Mobile-first layout | `max-width` queries or no media queries; layout breaks at some sizes | `min-width` media queries throughout, layout correct at all breakpoints | Breakpoints chosen from content needs, not just device presets |
| Flexbox & Grid | Layouts don't adapt, or still hardcoded to one screen size | Stack-to-row, `order`, sticky footer, and `auto-fill`/`minmax` grid all working | `grid-template-areas` used for the detail page, matches wireframe at every breakpoint |
| Images | Images overflow, distort, or aren't responsive | All images fluid (`width: 100%; height: auto`) | `object-fit` used where a fixed-height container needs it |
| Semantic HTML & alt text | Mostly `div`/`span`, missing or generic alt text | Correct semantic elements throughout, all images have meaningful alt text | Structure reads as a sensible outline; alt text is specific and useful |
| Hamburger menu & ARIA | Menu doesn't open/close, missing ARIA, or nav broken at some size | Menu works on mobile and desktop, `aria-label`/`aria-expanded`/`aria-hidden` present and correct, closes on link click | Smooth open/close transition, closes on outside click, visible keyboard focus style, 44×44px+ touch target |
| Contrast & keyboard access | Contrast failures present, or elements unreachable by keyboard | All text passes 4.5:1, full site keyboard-navigable with visible focus | All text and UI components pass WCAG AA, tab order matches visual order |
| Lighthouse accessibility score | Below 70 | 70–89 | 90+ |
| Tailwind conversion | Vanilla CSS still driving layout, or Tailwind not applied consistently | Grid, Flexbox, and hide/show all rebuilt with Tailwind responsive prefixes, matching prior behavior | Vanilla CSS files removed where fully replaced; `container`/`mx-auto`/`gap` used idiomatically |

---

## Assess your work

The table below is the same-day checkpoint for today's Tailwind work specifically — see the Final Rubric above for how the whole site gets graded.

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Setup | Tailwind not working or base styles broken | Tailwind installed and applying styles correctly | Old conflicting CSS removed or reconciled |
| Responsive grid | Grid not responsive or uses vanilla CSS | Tailwind responsive grid classes applied, correct column counts per breakpoint | `gap`, `container`, `mx-auto` used appropriately |
| Flex layout | Header or footer layout broken | Flexbox layout rebuilt with Tailwind, matches vanilla CSS result | Responsive direction changes use prefix classes correctly |
| Hide/show | Hamburger and full nav visible simultaneously | Correct show/hide at breakpoint using `hidden` and `md:flex` | All responsive display changes use Tailwind prefix classes |
