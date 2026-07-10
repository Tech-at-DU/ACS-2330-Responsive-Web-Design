# Class 2: Wireframes to Code

You should have your wireframes from class 1 homework. In this session you will finish your wire framing, and start translating these into a CSS implementation plan. 

## Objectives

- Complete responsive wireframes for SFPOPOS
- Annotate wireframes with responsive change notation
- Translate wireframe annotations into CSS strategies
- Identify which CSS tools handle which responsive changes

## Part 1: Wireframe Peer Review (20 mins)

Pair up. Exchange wireframes. For each wireframe, check:

- [ ] Mobile wireframe exists for every page
- [ ] Desktop wireframe exists for every page
- [ ] Every responsive change is annotated (`[mobile] → [desktop]`)
- [ ] Navigation behavior is specified (what happens to the nav on mobile?)
- [ ] Column counts are marked on grid/list pages
- [ ] Touch targets are identified (buttons, links, cards)
- [ ] Content order changes are noted

Give your partner specific feedback: "Your detail page is missing a mobile wireframe" or "Nav has no annotation — what happens to it on mobile?"

Fix any gaps before Part 2.

---

## CSS Modules in Vite

Before writing CSS, you need to know where it goes. SFPOPOS was built with Vite and React. Most Vite/React projects use **CSS Modules** — each component has its own scoped CSS file, and class names don't leak between components.

**File structure:**

```
src/
  components/
    Title/
      Title.jsx
      Title.module.css       ← styles for Title only
    POPOSList/
      POPOSList.jsx
      POPOSList.module.css   ← styles for POPOSList only
```

**How to use them — import the CSS file as a JavaScript object:**

```jsx
import styles from './POPOSList.module.css'

function POPOSList() {
  return <div className={styles.grid}>...</div>
}
```

**The hyphen naming rule:**

CSS class names with hyphens are not valid JavaScript identifiers, so they require bracket notation in JSX:

```css
/* POPOSList.module.css */
.grid { ... }            /* dot notation works:   styles.grid */
.POPOSList-grid { ... }  /* requires brackets:    styles['POPOSList-grid'] */
```

To avoid bracket notation entirely, use camelCase in your CSS Modules:

```css
/* Prefer camelCase — no brackets needed in JSX */
.poposList { ... }       /* → styles.poposList */
.popOSListGrid { ... }   /* → styles.popOSListGrid */
```

If SFPOPOS already uses hyphenated class names, you have two options: rename them to camelCase (requires updating JSX too), or use bracket notation consistently. Pick one and be consistent.

**Not using CSS Modules?** If your project uses plain `.css` files (no `.module.css`), class names are applied as plain strings: `className="POPOSList-grid"`. The CSS patterns in this course are the same either way — only the import syntax differs.

---

## Part 2: Wireframe to CSS (30 mins)

Every annotation in your wireframe maps to a CSS strategy. Here's the translation:

| Wireframe annotation | CSS approach |
|---------------------|-------------|
| `1 col → 3 col` | `grid-template-columns` inside a media query |
| `stacked → side by side` | `flex-direction: column` → `flex-direction: row` |
| `hamburger → full nav` | `display: none` / `display: block` toggled by media query + JS state |
| `hidden → visible` | `display: none` on one size, `display: block` on the other |
| `full width → 50% width` | `width: 100%` → `width: 50%` inside a media query |
| `image fills width` | `width: 100%; height: auto;` |
| `text scales` | Font size change inside a media query (or `clamp()` later) |
| `reorder on mobile` | `order` property on flex items |

**Exercise:** Go through every annotation on your wireframes. Write the CSS property or approach next to it. You're building your implementation checklist.

Example for the SFPOPOS spaces grid:

```
Wireframe: 1 col (mobile) → 3 col (desktop)
CSS: grid-template-columns: 1fr (default) → grid-template-columns: 1fr 1fr 1fr (at 768px+)
```

By the end of this exercise you should have a list of CSS changes you need to make. This is your work order for the next few classes.

---

## Part 3: Figma (20 mins)

If you haven't already, move your wireframes into a digital tool. Figma is free and works in the browser.

- https://www.figma.com
- Figma desktop app: https://www.figma.com/downloads/
- 8-minute wireframing tutorial: https://www.youtube.com/watch?v=D4NyQ5iOMF0

Figma wireframing rules:
- Boxes and text only — no color, no images, no fonts
- Use real labels (the text that will actually appear in the UI)
- Name your frames: `Home - Mobile`, `Home - Desktop`, `Detail - Mobile`, etc.

Digital wireframes are easier to share, annotate, and reference while coding. They're also easier to update when your implementation reveals something you didn't plan for.

---

## Part 4: Write Your First Media Query (30 mins)

Don't leave class without proving the translation works. Pick one item from your implementation checklist — ideally the spaces grid column change since every SFPOPOS project has it — and implement it now.

Open your SFPOPOS project and write this:

```css
/* Default — mobile, single column */
.POPOSList-grid {
  display: grid;
  grid-template-columns: 1fr;
}

/* Desktop — three columns */
@media (min-width: 1024px) {
  .POPOSList-grid {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
```

Adjust the class name to match yours. Check it in browser dev tools: resize to 375px — one column. Resize to 1200px — three columns.

**If your grid already uses `grid-template-columns`, you already have the first half.** Just add the media query below it.

This is the loop: wireframe annotation → implementation checklist item → working CSS. You'll repeat this loop for every annotation over the next four classes.

Mark the item done on your checklist. You have at least one item finished before class 3.

---

## Homework

Finalize your wireframes and implementation checklist.

Your submission should include:
- Complete wireframes (mobile + desktop for every page)
- All responsive changes annotated with `[mobile] → [desktop]` notation
- Implementation checklist: for each annotation, what CSS property or approach will you use?

You'll use this checklist in class-3 when you start writing media queries.

### Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Wireframe completeness | Missing pages or sizes | Mobile + desktop wireframe for every page | All pages, all sizes, clearly labeled |
| Annotations | Few or no annotations | Every responsive change annotated with `[mobile] → [desktop]` notation | Annotations are specific enough to write CSS from (column counts, exact behavior) |
| Implementation checklist | Missing or vague | Each annotation maps to a CSS property or approach | Checklist is organized by page and reads like a work order |
| Figma / tool quality | Hard to read, sloppy | Clear and legible, frames named correctly | Well-organized, easy to navigate between pages and sizes |
