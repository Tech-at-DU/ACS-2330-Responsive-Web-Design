# Class 4: Responsive Flexbox Patterns

You already know Flexbox. This class focuses on how to use it specifically for responsive layouts — the patterns you'll reach for every time a layout needs to change between mobile and desktop.

## Objectives

- Use `flex-direction` to switch between stacked and side-by-side layouts
- Use `order` to resequence content on mobile
- Use `vw`, `vh`, and `%` units for fluid sizing
- Implement responsive images
- Show and hide elements across breakpoints
- Apply a sticky footer with Flexbox

---

## Responsive Units

### `%`

Percentage is relative to the **parent element**. Use it to size children proportionally within a container:

```css
.card {
  width: 100%;    /* fills parent on mobile */
}

@media (min-width: 768px) {
  .card {
    width: 50%;   /* two cards side by side on tablet */
  }
}
```

### `vw` and `vh`

`vw` and `vh` are relative to the **viewport**, not the parent. `100vw` = full browser width, `100vh` = full browser height.

```css
.hero {
  height: 100vh;  /* fills the entire screen height */
  width: 100vw;   /* fills the entire screen width */
}
```

Use `vh` for full-screen sections and `vw` for elements that need to span the entire window regardless of their container.

**Note:** `%` and `vw`/`vh` look similar but behave differently when elements are nested. `%` is relative to the parent; `vw`/`vh` always refer to the window.

---

## Stack to Row Pattern

The most common responsive Flexbox pattern: elements stack vertically on mobile, sit side by side on desktop.

```css
.POPOSDetails {
  display: flex;
  flex-direction: column;  /* mobile: stacked */
}

@media (min-width: 768px) {
  .POPOSDetails {
    flex-direction: row;   /* desktop: side by side */
  }
}
```

Apply this to the SFPOPOS detail page — image and text info should sit side by side on desktop, stack on mobile.

---

## Reordering Content with `order`

On mobile, content order often needs to differ from desktop. The `order` property on flex items lets you change sequence without changing the HTML.

Example: on the detail page, the image appears first in the HTML, but on mobile you may want the title and key info first (above the fold), with the image below.

```css
/* Mobile: title first, image second */
.POPOSDetails-image { order: 2; }
.POPOSDetails-info  { order: 1; }

@media (min-width: 768px) {
  /* Desktop: image left, info right — restore HTML order */
  .POPOSDetails-image { order: 1; }
  .POPOSDetails-info  { order: 2; }
}
```

Check your wireframe annotations — any `reorder on mobile` notes become `order` properties.

---

## Hiding and Showing Elements

Sometimes mobile and desktop need completely different elements — a hamburger button on mobile, a full nav on desktop.

```css
/* Default (mobile): show hamburger, hide full nav */
.nav-full     { display: none; }
.nav-hamburger { display: block; }

@media (min-width: 768px) {
  /* Desktop: show full nav, hide hamburger */
  .nav-full      { display: block; }
  .nav-hamburger { display: none; }
}
```

Any `hidden → visible` annotation in your wireframe becomes a `display` toggle.

---

## Responsive Images

**Method 1 — fluid image (most common):**

```css
img {
  width: 100%;
  height: auto;
}
```

`width: 100%` fills the container. `height: auto` maintains aspect ratio. This is all you need for most images.

**Method 2 — `object-fit` for fixed-height containers:**

```css
.card-image {
  width: 100%;
  height: 200px;
  object-fit: cover;  /* crops to fill, no distortion */
}
```

Use this when you need a consistent image height across cards in a grid.

**Method 3 — `srcset` for performance (serve smaller images to small screens):**

```html
<img
  src="image-large.jpg"
  srcset="image-small.jpg 480w,
          image-medium.jpg 768w,
          image-large.jpg 1200w"
  alt="Description"
>
```

The browser picks the most appropriate size. Worth doing for hero images and anything above the fold.

---

## Sticky Footer

A sticky footer sits at the bottom of the viewport when content is short, and stays below content when the page is long. Flexbox makes this straightforward.

HTML structure required:

```jsx
<div className="App">
  <div className="App-content">
    {/* all page content here */}
  </div>
  <Footer />
</div>
```

CSS:

```css
.App {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.App-content {
  flex: 1 0 auto;  /* grows to fill available space */
}

.Footer {
  flex-shrink: 0;  /* never shrinks */
}
```

The `flex: 1 0 auto` on the content area pushes the footer to the bottom. Apply this to SFPOPOS — the About page and detail pages are short enough that the footer floats up without it.

---

## Challenge

Work through your SFPOPOS implementation checklist and apply Flexbox patterns where your wireframe calls for them:

1. **Detail page** — stack to row layout (image + info)
2. **Detail page** — reorder content on mobile if your wireframe calls for it
3. **Nav bar** — use Flexbox to arrange links horizontally on desktop
4. **Sticky footer** — apply to all pages
5. **Images** — apply `width: 100%; height: auto` to all images in the project

Test each change at mobile (375px) and desktop (1024px+) in browser dev tools.

**Stretch challenge:** On the nav bar, use Flexbox to push nav links to the right while keeping the site title on the left:

```css
.Title {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Stack to row | No flex-direction changes across breakpoints | Detail page switches between column and row correctly | Multiple layout areas use stack-to-row, applied appropriately |
| Content order | No use of `order` where wireframe calls for reordering | `order` used correctly to match wireframe | Order changes only applied inside media queries (not affecting desktop) |
| Images | Images overflow or distort at some sizes | All images are fluid (`width: 100%; height: auto`) | `object-fit` used for fixed-height image containers |
| Sticky footer | Footer floats up on short pages | Sticky footer works on all pages | Tested on multiple page types (short and long content) |
