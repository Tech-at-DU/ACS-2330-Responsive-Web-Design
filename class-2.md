# Class 2: Wireframes to Code

Students arrive with wireframes from the class-1 homework. This session finishes the wireframes and translates them into a CSS implementation plan.

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
