# Class 7: ARIA and Color Contrast

Semantic HTML gets you most of the way to an accessible site. ARIA fills the gaps — it communicates state, labels elements that have no visible text, and describes dynamic behavior that HTML alone can't express.

## Objectives

- Apply ARIA attributes to interactive components
- Label icon-only buttons and controls correctly
- Communicate open/closed state with `aria-expanded`
- Check and fix color contrast across the site

---

## What is ARIA?

ARIA (Accessible Rich Internet Applications) is a set of HTML attributes that add semantic meaning screen readers can't get from HTML structure alone.

**The first rule of ARIA:** don't use it if a native HTML element does the job. A `<button>` is already announced as a button. A `<nav>` is already announced as navigation. ARIA is for filling gaps, not replacing semantic HTML.

Three types of ARIA attributes:
- **Roles** — what an element is (`role="dialog"`, `role="alert"`)
- **Properties** — what an element is like (`aria-label`, `aria-describedby`, `aria-required`)
- **States** — what an element is doing right now (`aria-expanded`, `aria-checked`, `aria-disabled`)

---

## The Most Useful ARIA Attributes

### `aria-label`

Provides a text label for elements with no visible text. Most common use: icon-only buttons.

```html
<!-- Without aria-label, screen reader says "button" — useless -->
<button>
  <svg><!-- hamburger icon --></svg>
</button>

<!-- With aria-label, screen reader says "Open navigation menu" -->
<button aria-label="Open navigation menu">
  <svg><!-- hamburger icon --></svg>
</button>
```

Every icon button needs an `aria-label`. This includes your hamburger menu, any close buttons, social media icons, and search buttons.

### `aria-expanded`

Communicates whether a collapsible element (menu, accordion, dropdown) is open or closed. Critical for hamburger menus.

```jsx
const [isOpen, setIsOpen] = useState(false)

<button
  aria-label="Open navigation menu"
  aria-expanded={isOpen}
  onClick={() => setIsOpen(!isOpen)}
>
  <svg><!-- hamburger icon --></svg>
</button>

<nav aria-hidden={!isOpen}>
  {/* nav links */}
</nav>
```

When `aria-expanded` is `false`, screen readers announce "Open navigation menu, collapsed." When `true`: "Open navigation menu, expanded." The user knows the state without seeing it.

### `aria-hidden`

Hides an element from the accessibility tree. Use it for decorative elements that add visual noise without meaning.

```html
<!-- Decorative icon next to labeled text — hide the icon -->
<span aria-hidden="true">★</span>
<span>Favorite</span>

<!-- Closed menu — hide from screen readers entirely -->
<nav aria-hidden="true">...</nav>
```

Don't use `aria-hidden="true"` on elements that contain focusable content — keyboard users will still reach them.

### `aria-labelledby`

Points to another element as the label. Use when the label already exists in the DOM.

```html
<h2 id="spaces-heading">Public Spaces</h2>
<section aria-labelledby="spaces-heading">
  <!-- section content -->
</section>
```

Screen readers announce the section as "Public Spaces region" without duplicating any text.

### `aria-describedby`

Points to an element that provides additional description — form hints, error messages.

```html
<label for="email">Email</label>
<input type="email" id="email" aria-describedby="email-hint">
<span id="email-hint">We'll never share your email.</span>
```

### `aria-current`

Marks the current item in a set — current page in nav, current step in a process.

```jsx
<NavLink
  to="/"
  aria-current={isActive ? "page" : undefined}
>
  List
</NavLink>
```

React Router's `NavLink` handles this automatically if you use its `isActive` pattern, but it's worth knowing what's happening under the hood.

---

## ARIA Roles

Only use `role` when you can't use the correct semantic element.

```html
<!-- If you must use a div as a button (avoid this when possible) -->
<div role="button" tabindex="0" onclick="...">Click me</div>

<!-- But prefer actual button -->
<button onclick="...">Click me</button>
```

Common roles you might need:
- `role="dialog"` — modal dialog boxes
- `role="alert"` — important message that screen reader announces immediately
- `role="status"` — non-urgent status update (form saved, item added to cart)
- `role="tab"` / `role="tabpanel"` — tab interface

```html
<!-- Announce a success message without moving focus -->
<div role="alert">Your changes have been saved.</div>
```

---

## Color and Contrast

Low contrast is one of the most common accessibility failures. Text that looks fine to most sighted users can be unreadable for people with low vision or color blindness.

**WCAG contrast requirements:**

| Text type | Minimum ratio (AA) |
|-----------|-------------------|
| Normal text (< 18pt or < 14pt bold) | 4.5:1 |
| Large text (≥ 18pt or ≥ 14pt bold) | 3:1 |
| UI components (borders, icons) | 3:1 |

Contrast ratio is the difference in luminance between foreground and background. 1:1 = no contrast (same color), 21:1 = maximum (black on white).

**Check your contrast:**

Use the WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/

Enter your foreground and background colors. The tool tells you whether you pass AA or AAA for each text size.

Common failures:
- Light gray text on white (`#aaaaaa` on `#ffffff` = 2.3:1 — fails)
- White text on medium-blue (`#ffffff` on `#4a90e2` = 3.0:1 — fails for normal text)
- Placeholder text in inputs (almost always too light)

**Don't rely on color alone.** If you use color to communicate status (red = error, green = success), also use an icon, text, or pattern. Colorblind users can't distinguish red from green.

```html
<!-- Bad — color only -->
<span style="color: red">Invalid email</span>

<!-- Good — color + icon + text -->
<span style="color: red">
  <span aria-hidden="true">✗</span> Invalid email address
</span>
```

---

## Challenge

**Part 1: Hamburger menu ARIA**

If you've started building your hamburger menu, add:
- `aria-label` on the toggle button
- `aria-expanded` tied to the open/closed state
- `aria-hidden` on the nav when closed

If you haven't built the hamburger yet, annotate your wireframe with these ARIA attributes — you'll implement them in class-8.

**Part 2: Icon audit**

Find every icon-only interactive element in SFPOPOS. Add `aria-label` to each one.

**Part 3: Contrast check**

Using the WebAIM Contrast Checker, check every text/background color combination in your SFPOPOS site:
- Body text on background
- Nav link text on nav background  
- Card text on card background
- Button text on button background
- Any placeholder text in forms

Document which pass and which fail. Fix the failures by adjusting color values until the ratio meets 4.5:1 for normal text.

**Part 4: Re-run Lighthouse**

After making ARIA and contrast fixes, re-run your Lighthouse accessibility audit. Your score should have increased from class-6.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Icon labels | Icon buttons have no labels | All icon-only buttons have `aria-label` | Labels are specific and descriptive ("Open navigation menu" not "menu") |
| `aria-expanded` | Not used | Used on hamburger or collapsible element, tied to open/closed state | State updates correctly on toggle, `aria-hidden` used on the controlled element |
| Contrast | Multiple contrast failures | All normal text passes 4.5:1 | All text including placeholders and UI components passes WCAG AA |
| Lighthouse score | Lower than class-6 score | Same or higher than class-6 score | 90+ |
