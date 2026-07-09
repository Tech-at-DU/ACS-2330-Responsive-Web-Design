# Class 3: Media Queries

Media queries are the CSS mechanism that makes responsive design work. They let you apply different styles at different screen sizes — the foundation of everything else in this course.

## Warmup (5 mins)

Show your implementation checklist to the person next to you. For each item on their list, ask: "what CSS property will this use?" If they can't answer, help them figure it out — use the translation table from class-2.

If you already wrote a media query in class-2, show it working. If not, you'll write your first one today.

## Objectives

- Write media queries using `min-width` (mobile-first)
- Define breakpoints for your project
- Apply media queries to SFPOPOS using your wireframe implementation checklist

---

## Media Query Syntax

The `@media` rule applies a block of CSS only when a condition is true:

```css
@media (min-width: 768px) {
  body {
    background-color: blue;
  }
}
```

This rule only applies when the screen is **768px wide or larger**. Below 768px, it does nothing.

### `min-width` vs `max-width`

There are two ways to write breakpoints:

```css
/* max-width: desktop-first — styles apply BELOW this width */
@media (max-width: 768px) {
  /* mobile overrides go here */
}

/* min-width: mobile-first — styles apply ABOVE this width */
@media (min-width: 768px) {
  /* desktop enhancements go here */
}
```

**This course uses `min-width` (mobile-first).** Write your default styles for mobile. Use media queries to add or change styles as the screen gets larger. This matches how Tailwind CSS works and is the current industry standard.

You'll see `max-width` in older codebases and tutorials — now you know the difference.

---

## CSS Pixels vs Physical Pixels

Screen sizes can be confusing. A phone screen might have 1125 physical pixels across, but CSS sees it as 375px. Why?

Phones have high pixel density — more physical pixels packed into a smaller area. The browser normalizes this with a **device pixel ratio**. An iPhone with a 3x ratio reports 375 CSS pixels even though the physical resolution is 1125px.

**CSS pixels are what matter for media queries.** When you write `min-width: 375px`, you're targeting CSS pixels, not physical pixels.

Common device widths in CSS pixels:
- iPhone SE: 375px
- iPhone 14 Pro: 393px
- iPad Mini: 768px
- iPad Pro: 1024px
- Desktop: 1280px+

---

## Breakpoints

Breakpoints are the screen widths where your layout changes. You don't need one for every device — you need one wherever your layout needs to change.

Common breakpoints:

| Name | Width | Typical target |
|------|-------|----------------|
| Mobile (default) | < 640px | Phones |
| Small | 640px | Large phones, small tablets |
| Medium | 768px | Tablets |
| Large | 1024px | Laptops |
| XL | 1280px | Desktops |

For most projects, **two or three breakpoints** cover the range well. Start with mobile default + one tablet breakpoint + one desktop breakpoint.

```css
/* Mobile: default styles, no media query needed */
.grid {
  display: grid;
  grid-template-columns: 1fr;
}

/* Tablet and up */
@media (min-width: 768px) {
  .grid {
    grid-template-columns: 1fr 1fr;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
```

Notice the order: mobile default first, then media queries in ascending order. Each query builds on the previous.

---

## Testing Media Queries

**Quick test:** set a background color in a media query and resize the browser. When the color changes, your query is working.

```css
@media (min-width: 768px) {
  body {
    background: fuchsia;
  }
}
```

**In Chrome:**
- Right-click → Inspect → click the device icon (top-left of DevTools)
- Select a device or drag to resize

**In Safari:**
- Safari → Settings → Advanced → check "Show Develop menu in menu bar"
- Develop → Enter Responsive Design Mode

Test at each of your breakpoints. Test on a real phone if you can.

---

## Media Query Features

Width is the most common media feature but not the only one:

| Feature | Example | Use case |
|---------|---------|----------|
| `min-width` / `max-width` | `(min-width: 768px)` | Screen size breakpoints |
| `orientation` | `(orientation: landscape)` | Phone rotated sideways |
| `prefers-color-scheme` | `(prefers-color-scheme: dark)` | Dark mode |
| `prefers-reduced-motion` | `(prefers-reduced-motion: reduce)` | Accessibility — skip animations |
| `hover` | `(hover: hover)` | Desktop only (touch devices don't hover) |

The `hover` feature is particularly useful: `@media (hover: hover)` lets you safely use hover styles only on devices that support them.

---

## Challenge

Open your SFPOPOS project and your implementation checklist from class-2. Work through the checklist and implement each responsive change using media queries.

Start with the spaces grid on the home page:

```css
/* Mobile default — single column */
.POPOSList-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

/* Tablet and up — two columns */
@media (min-width: 768px) {
  .POPOSList-grid {
    grid-template-columns: 1fr 1fr;
  }
}

/* Desktop and up — three columns */
@media (min-width: 1024px) {
  .POPOSList-grid {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
```

Then continue with the other items on your checklist. Place all media queries **at the bottom of each CSS file**, in ascending `min-width` order.

**Stretch challenge:** Add `prefers-reduced-motion` to any CSS transitions or animations in your project:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none;
    animation: none;
  }
}
```

This is a one-liner that makes your site more accessible for users with vestibular disorders.

---

## End of Class Checkpoint

Before you leave, show your neighbor one working media query in your SFPOPOS project — resized in browser dev tools to prove it fires at the right breakpoint. If you can't show one working, stay and get help before next class.

By end of class you should have at minimum:
- Spaces grid responsive (1 col mobile → 3 col desktop)
- At least one other checklist item implemented

The rest of the checklist continues in class 4.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Mobile-first | Using `max-width` (desktop-first) or no media queries | Using `min-width`, default styles apply to mobile | All default styles work well on mobile before any media queries are applied |
| Breakpoints | One or no breakpoints, or breakpoints chosen arbitrarily | Two or more breakpoints that match layout changes in wireframes | Breakpoints chosen based on content needs, not just common device sizes |
| Implementation | Few checklist items implemented | Most checklist items implemented with correct CSS | All checklist items implemented, code is clean and well-organized |
| Testing | Not tested at different sizes | Tested in browser dev tools at each breakpoint | Tested on a real mobile device |
