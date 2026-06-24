# Class 6: Accessibility and Inclusive Design

Accessibility is the practice of building websites that work for everyone — including people with visual, auditory, motor, and cognitive disabilities. This class covers why it matters, how to build accessibly from the start, and how to test what you've built.

## Objectives

- Explain why accessibility matters for developers (legal, ethical, business)
- Apply semantic HTML to improve screen reader and keyboard accessibility
- Write meaningful alt text for images
- Test a site with keyboard navigation and browser accessibility tools

---

## Why Accessibility Matters

**Legal:** The Americans with Disabilities Act (ADA) and Section 508 of the Rehabilitation Act require accessibility for government and many commercial websites. Businesses have faced lawsuits for inaccessible websites — this is not theoretical.

**Scale:** Roughly 1 in 4 adults in the US has some form of disability. Globally, over 1 billion people have a disability that affects how they use the web. An inaccessible site excludes a significant portion of your potential users.

**SEO:** Accessibility improvements — semantic HTML, alt text, logical heading structure — are the same things search engines use to understand your content. Accessible sites rank better.

**Code quality:** Accessible code is better code. Proper semantic structure, clear labels, and logical tab order make sites easier to maintain and debug.

The Web Content Accessibility Guidelines (WCAG) are the technical standard. Most legal requirements reference WCAG 2.1 Level AA compliance.

---

## Semantic HTML

Semantic HTML means using the right HTML element for the right purpose. Browsers and screen readers use element type to understand the role of content — a `<nav>` is navigation, a `<button>` is interactive, an `<h1>` is a top-level heading.

Using `<div>` for everything strips that meaning.

**Common semantic elements and when to use them:**

| Element | Use for |
|---------|---------|
| `<header>` | Site header or section header |
| `<nav>` | Navigation links |
| `<main>` | Primary page content (one per page) |
| `<section>` | Thematically grouped content |
| `<article>` | Self-contained content (blog post, card) |
| `<aside>` | Secondary content, sidebars |
| `<footer>` | Site footer or section footer |
| `<figure>` + `<figcaption>` | Image with caption |
| `<button>` | Anything the user clicks to trigger an action |
| `<a>` | Navigation to another page or location |

**SFPOPOS example — before:**

```jsx
<div className="Title">
  <div className="Title__nav">
    <NavLink to="/">List</NavLink>
    <NavLink to="/about">About</NavLink>
  </div>
</div>
```

**After:**

```jsx
<header className="Title">
  <nav className="Title__nav">
    <NavLink to="/">List</NavLink>
    <NavLink to="/about">About</NavLink>
  </nav>
</header>
```

Same visual result. Completely different meaning to a screen reader.

---

## Alt Text

Every `<img>` needs an `alt` attribute. Screen readers read it aloud in place of the image.

**Rules:**
- Describe what the image communicates, not what it looks like
- If the image is purely decorative, use `alt=""` (empty string — tells screen reader to skip it)
- Don't start with "Image of..." or "Photo of..." — screen readers already announce it's an image
- Be specific: `alt="Interior courtyard at 101 California with benches and trees"` not `alt="courtyard"`

```html
<!-- Bad -->
<img src="space.jpg" alt="image">

<!-- Decorative — skip it -->
<img src="divider.png" alt="">

<!-- Good -->
<img src="space.jpg" alt="Rooftop garden at 555 Mission St with seating area and city views">
```

---

## Keyboard Navigation

Every interactive element on your site should be reachable and usable with a keyboard alone. Users with motor disabilities navigate by keyboard. So do power users.

**Test it now:**
1. Open your SFPOPOS site
2. Don't touch the mouse
3. Press Tab to move forward through interactive elements, Shift+Tab to go back
4. Press Enter or Space to activate buttons and links

What to check:
- Can you reach every link and button?
- Can you tell where you are? (focus indicator — the outline around the focused element)
- Does the tab order make sense? (usually top-to-bottom, left-to-right)
- Can you use the nav, click cards, and navigate to detail pages?

**Never remove the focus outline** with `outline: none` unless you replace it with a custom visible indicator. Removing it breaks keyboard navigation for sighted keyboard users.

```css
/* Bad — hides focus completely */
:focus { outline: none; }

/* Good — custom focus style */
:focus {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}
```

---

## Headings

Screen reader users navigate pages by jumping between headings. The heading structure is like a table of contents — it needs to make sense in order.

- One `<h1>` per page (the page title)
- `<h2>` for major sections
- `<h3>` for subsections
- Don't skip levels (no `<h1>` → `<h3>` without an `<h2>`)
- Don't choose heading level based on font size — use CSS for size, heading level for structure

---

## Testing Tools

**WAVE** — browser extension that overlays accessibility issues directly on the page. Shows missing alt text, empty links, contrast failures, heading structure.

- https://wave.webaim.org
- Install the Chrome or Firefox extension

**Lighthouse** — built into Chrome DevTools. Run an accessibility audit: right-click → Inspect → Lighthouse tab → Accessibility → Analyze.

Scores 0–100. Aim for 90+. The report gives specific issues with links to fix them.

**VoiceOver (Mac)** — the built-in screen reader. Use it to experience your site the way a blind user does.

- Turn on: Cmd + F5 (or System Settings → Accessibility → VoiceOver)
- Navigate: VO key (Caps Lock) + Arrow keys
- Quick start guide: https://support.apple.com/guide/voiceover/welcome/mac

Use VoiceOver on a site you use every day first. Then use it on SFPOPOS. The frustration you feel is what inaccessible sites impose on users who have no alternative.

---

## Challenge

**Part 1: Semantic HTML audit**

Go through every component in your SFPOPOS project. Replace generic `<div>` and `<span>` tags with semantic elements where appropriate. Use the table above as a guide.

At minimum:
- Site header → `<header>`
- Navigation → `<nav>`
- Main content area → `<main>`
- Site footer → `<footer>`
- Space images → `<figure>` + `<figcaption>`

**Part 2: Alt text**

Add meaningful alt text to every image in the project. For the SFPOPOS spaces, write alt text that describes the space (what it looks like, where it is).

**Part 3: Keyboard test**

Navigate your entire SFPOPOS site using only the keyboard. Document every place where:
- You can't reach something
- You lose track of where you are (no focus indicator)
- The tab order doesn't make sense

Fix what you can.

**Part 4: Run Lighthouse**

Run a Lighthouse accessibility audit on each page. Note your score. Fix the issues Lighthouse identifies and re-run. Target 90+.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Semantic HTML | Mostly `<div>` tags, no semantic structure | Major structural elements use correct semantic tags | All elements use appropriate semantic tags, structure makes sense as an outline |
| Alt text | Missing or generic (`alt="image"`) | All images have descriptive alt text | Alt text is specific and meaningful — describes what the image communicates |
| Keyboard navigation | Major elements unreachable by keyboard | All interactive elements reachable and usable by keyboard | Tab order is logical, focus indicator is visible on all elements |
| Lighthouse score | Below 70 | 70–89 | 90+ |
