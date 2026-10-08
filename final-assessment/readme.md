# Final Assessment

**Time:** 45 minutes, in class. Open notes, open docs (MDN, your own projects). No AI tools and no copying from classmates.

We have a new image editing app. It works, but it has no styles and poor accessibility. Your job is to make it **responsive** and **accessible**.

## Getting Started

1. Download `Archive.zip` and unzip it. It contains `index.html`, `dali.png`, and this readme.
2. Open `index.html` in your browser. Move the sliders to see what the app does.
3. Add your styles in a `<style>` tag or a linked `styles.css`. Plain CSS only — no Tailwind or frameworks for this one.

You can change the HTML however you like, **but do not change the `id` attributes on the inputs.** The JavaScript uses them.

---

## Part 1: Responsive Layout (60%)

Build the layout **mobile-first**: your base styles are for mobile, then use `min-width` media queries to add the tablet and desktop layouts.

| Screen | Width | Media query |
|--------|-------|-------------|
| Mobile | under 600px | none (base styles) |
| Tablet | 600px – 839px | `@media (min-width: 600px)` |
| Desktop | 840px and up | `@media (min-width: 840px)` |

### Mobile (base styles)

- The page stacks vertically: **image on top**, form below.
- The image fills the width of the screen without overflowing (no horizontal scroll at 375px).
- Form controls are almost the full width of the screen and centered.
- Each label sits **above** its slider, with the label text centered.

![assessment mobile](./assessment-mobile.png)

### Tablet (600px and up)

- Still stacked vertically: **image on top**, form below.
- Each label sits to the **left** of its slider, on the same line.
- Label text is right-aligned so the labels line up against the sliders.
- All sliders are the same width and take up about three quarters of the row.

![assessment tablet](./assessment-tablet.png)

### Desktop (840px and up)

- Two boxes side by side, each 400px × 400px, centered on the page.
- **Form on the left, image on the right.**
- Form controls stack vertically, with each label above its slider, left-aligned.

![assessment desktop](./assessment-desktop.png)

> **Hint:** In the HTML the form comes *before* the image, but on mobile and tablet the image needs to be on top. Think about which Flexbox or Grid property can change the visual order without changing the HTML.

---

## Part 2: Accessibility (40%)

Do each of these:

- [ ] Use semantic landmarks: wrap the app in `<main>`, and add an `<h1>` that names the app.
- [ ] Give the image meaningful `alt` text.
- [ ] Every slider has a label that a screen reader will announce (check this in DevTools → Accessibility panel).
- [ ] Sliders show a **visible focus style** when you Tab to them. Don't remove the outline without replacing it.
- [ ] You can operate every slider with only the keyboard (Tab to it, arrow keys to change it).
- [ ] Text has enough color contrast (4.5:1) if you add colors.
- [ ] Run Lighthouse → Accessibility. Aim for **90 or higher**. Take a screenshot of your score.

---

## Stretch Goals (optional)

Finished early? Try any of these:

- Use `clamp()` for the heading size so it scales smoothly between mobile and desktop.
- Show each slider's current value next to its label using an `<output>` element (you'll need a little JavaScript).
- Wrap the sliders in a `<fieldset>` with a `<legend>` like "Image filters".
- Add a `prefers-reduced-motion` or `prefers-color-scheme: dark` media query.
- Make the form a container and use a **container query** instead of a media query to switch the label layout.

---

## Grading

| Area | Points | What we're looking for |
|------|--------|------------------------|
| Mobile layout | 20 | Image on top, full-width controls, labels above and centered, no horizontal scroll |
| Tablet layout | 20 | Image on top, labels left and right-aligned, sliders equal width |
| Desktop layout | 20 | Two 400×400 boxes side by side, form left, image right |
| Semantic HTML + alt text | 15 | `<main>`, `<h1>`, meaningful `alt` |
| Keyboard + focus | 15 | Every slider reachable and usable by keyboard with a visible focus style |
| Lighthouse Accessibility | 10 | Score of 90+ (screenshot included) |
| **Total** | **100** | Passing is 70 |

Stretch goals don't add points, but they can make up for small misses elsewhere.

## Submit Your Work

Before time is up, submit to Gradescope:

1. Your `index.html` (and `styles.css` if you used one)
2. A screenshot of your Lighthouse Accessibility score

Check your work at 375px, 700px, and 1200px wide in DevTools before you submit.
