# Class 5: Responsive CSS Grid

CSS Grid is a two-dimensional layout system — it controls both rows and columns simultaneously. Where Flexbox handles one axis at a time, Grid handles the full layout. For responsive design, Grid has patterns that handle column changes with zero media queries.

## Objectives

- Use `fr` units to create fluid grid columns
- Use `repeat()`, `auto-fill`, and `minmax()` for automatically responsive grids
- Use `grid-template-areas` to restructure page layouts at breakpoints
- Apply Grid to the SFPOPOS spaces list

---

## Warmup: CSS Grid Garden (15 mins)

Practice Grid fundamentals with this game before the lesson:

https://cssgridgarden.com

Complete at least the first 20 levels.

---

## The `fr` Unit

`fr` stands for "fraction of available space." It's the Grid equivalent of `flex: 1`.

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;  /* three equal columns */
}
```

Mix `fr` with fixed units:

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;  /* fixed sidebar, fluid content */
}
```

The `1fr` column takes all remaining space after the 250px sidebar is placed.

---

## `repeat()`, `auto-fill`, and `minmax()`

This combination is the most powerful responsive Grid pattern. It creates a fluid column grid that adjusts the number of columns automatically based on available space — **no media queries required**.

```css
.POPOSList-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1rem;
}
```

How it works:
- `minmax(280px, 1fr)` — each column is at least 280px wide, but can grow to fill available space
- `auto-fill` — fit as many columns as possible given that minimum
- Result: 1 column on mobile, 2 on tablet, 3 on desktop — automatically

**`auto-fill` vs `auto-fit`:**

```css
/* auto-fill: empty columns keep their space */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));

/* auto-fit: empty columns collapse — items stretch to fill */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

For card grids, `auto-fill` is usually what you want. For a small number of items that should center or spread out, use `auto-fit`.

Apply `repeat(auto-fill, minmax(...))` to the SFPOPOS spaces grid and remove the media query column changes you wrote in class-3 — this pattern replaces them.

---

## `grid-template-areas` for Layout Changes

`grid-template-areas` lets you name regions of a grid and rearrange them at different breakpoints by simply redefining the template. This is one of the clearest ways to express a layout change.

Example: SFPOPOS detail page with header, image, info, and footer.

```css
/* Mobile: everything stacks */
.POPOSDetails {
  display: grid;
  grid-template-areas:
    "header"
    "image"
    "info"
    "footer";
}

@media (min-width: 768px) {
  /* Desktop: image and info side by side */
  .POPOSDetails {
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      "header header"
      "image  info"
      "footer footer";
  }
}
```

Assign elements to areas:

```css
.POPOSDetails-header { grid-area: header; }
.POPOSDetails-image  { grid-area: image; }
.POPOSDetails-info   { grid-area: info; }
.POPOSDetails-footer { grid-area: footer; }
```

The layout completely restructures between mobile and desktop with no changes to HTML — just the CSS template string. This is exactly the kind of change your wireframe annotations describe.

---

## `gap`

`gap` sets spacing between grid tracks (both rows and columns). Use it instead of margins on grid items:

```css
.grid {
  display: grid;
  gap: 1rem;           /* equal row and column gap */
  /* or */
  gap: 1rem 2rem;      /* row-gap column-gap */
}
```

---

## When to Use Grid vs Flexbox

| Situation | Use |
|-----------|-----|
| Card grid, photo gallery, product list | Grid |
| Nav bar, toolbar, button group | Flexbox |
| Full page layout (header/sidebar/main/footer) | Grid |
| Centering a single item | Flexbox |
| Items that need to wrap fluidly | Either (Grid's `auto-fill` is cleaner) |
| Reordering regions across breakpoints | Grid (`grid-template-areas`) |

In practice you'll use both. Grid handles macro layout; Flexbox handles micro layout within Grid cells.

---

## Challenge

**Part 1:** Apply `repeat(auto-fill, minmax(280px, 1fr))` to the SFPOPOS spaces grid. Remove the manual column breakpoints from class-3 — compare the two approaches. Which is cleaner?

**Part 2:** Convert the SFPOPOS detail page layout to use `grid-template-areas`. Your wireframe annotations for that page describe the mobile and desktop arrangements — implement them.

**Part 3:** Solve the responsive grid challenges:
- https://github.com/Tech-at-DU/Grid-responsive-Challenge
- https://github.com/Tech-at-DU/responsive-web-design-challenge

Submit the second challenge to Gradescope separately.

**Stretch challenge:** Add a sidebar layout to the SFPOPOS About page using `grid-template-areas`:

```
Mobile:              Desktop:
┌──────────┐         ┌────────┬──────────┐
│  header  │         │ header │  header  │
├──────────┤         ├────────┼──────────┤
│  content │         │sidebar │  content │
├──────────┤         │        │          │
│  sidebar │         └────────┴──────────┘
└──────────┘
```

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| `fr` units | Fixed pixel columns | Uses `fr` for at least one column | All fluid columns use `fr`, mixed with fixed where appropriate |
| `auto-fill`/`minmax` | Manual column breakpoints only | `repeat(auto-fill, minmax())` applied to spaces grid | Correct minimum size chosen — cards don't get too narrow or too wide |
| `grid-template-areas` | Not used | Applied to detail page with correct mobile and desktop templates | Area names match element names, layout matches wireframe |
| Challenge repos | Not attempted | Both challenges completed | Stretch challenge completed |
