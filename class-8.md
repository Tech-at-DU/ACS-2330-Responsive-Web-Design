# Class 8: Responsive Navigation and the Hamburger Menu

The hamburger menu is one of the most common patterns in responsive web development. Every developer encounters it. It brings together everything from the first half of this course: media queries, CSS display toggling, Flexbox, ARIA, and React state.

**If you already added `isOpen`/`aria-expanded`/`aria-hidden` to your `Title` component in class-7**, keep that state and those attributes — today just adds the CSS classes and media query that actually show/hide the nav, plus the close-on-navigate and close-on-outside-click behavior. You are not starting over.

This is the last piece of Assignment 3. It's due at the end of next class (class-9), so leave class today with the **Must have** list below fully checked off.

---

## Assignment 3: Final Rubric (Whole Site)

This is the full grading rubric for A3, covering everything built across classes 3–9. It's also in class-9, but you're seeing it here first — with two class days still left to close gaps before it's graded.

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

Note on the last row: Tailwind conversion happens next class (class-9) — nothing to check off there yet.

---

## Warmup: Self-Assess Your SFPOPOS Progress (10 mins)

Assignment 3 is due at the end of next class. Before starting today's lesson, audit your SFPOPOS project against everything it's supposed to cover so far. Check off what's actually working — not what you meant to do. Anything unchecked is today's priority, before the hamburger menu.

**Mobile-first & media queries (class-3)**
- [ ] All media queries use `min-width` (mobile-first), not `max-width`
- [ ] At least two breakpoints, matching layout changes in your wireframe
- [ ] Media queries at the bottom of each `.module.css` file, ascending order

**Flexbox (class-4)**
- [ ] Detail page switches from stacked (mobile) to row (desktop)
- [ ] `order` used anywhere your wireframe calls for reordering on mobile
- [ ] All images are fluid (`width: 100%; height: auto`) — none overflow or distort
- [ ] Sticky footer works on both short and long pages

**Grid (class-5)**
- [ ] Spaces grid uses `repeat(auto-fill, minmax(...))` — manual column breakpoints removed
- [ ] Detail page uses `grid-template-areas`, correct at both mobile and desktop

**Accessibility (class-6)**
- [ ] Semantic HTML in place: `header`, `nav`, `main`, `footer`, `figure`/`figcaption`
- [ ] Every image has meaningful alt text (or `alt=""` if purely decorative)
- [ ] Whole site usable by keyboard alone, with a visible focus indicator everywhere
- [ ] Lighthouse accessibility score recorded

**ARIA & contrast (class-7)**
- [ ] `aria-label` on every icon-only button
- [ ] `aria-expanded` wired to the hamburger's open/closed state
- [ ] Every text/background pair checked against WebAIM, failures fixed to 4.5:1+
- [ ] Tab order audited — no leftover positive `tabindex` values
- [ ] Lighthouse score same or higher than class-6

If more than a couple of these are unchecked, use the first part of class today to close the gaps — the hamburger menu below assumes this foundation is already solid.

---

## Objectives

- Build a hamburger menu component in React
- Wire open/closed state with `useState`
- Apply ARIA attributes for accessibility
- Use media queries to show the hamburger on mobile and full nav on desktop
- Close the menu on navigation and outside click

---

## The Pattern

A responsive nav has two modes:

```
Mobile (< 768px)          Desktop (≥ 768px)
┌─────────────────┐       ┌────────────────────────────────┐
│ SFPOPOS      ☰  │       │ SFPOPOS        List   About    │
└─────────────────┘       └────────────────────────────────┘
    ↓ tap ☰
┌─────────────────┐
│ SFPOPOS      ✕  │
├─────────────────┤
│ List            │
│ About           │
└─────────────────┘
```

Mobile: hamburger button controls a collapsible nav panel.
Desktop: full nav always visible, hamburger button hidden.

---

## Step 1: State

Add `useState` to your `Title` component to track whether the menu is open:

```jsx
import { useState } from 'react'

function Title() {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <header className="Title">
      ...
    </header>
  )
}
```

---

## Step 2: The Hamburger Button

The button needs a visible icon and accessible labels. Build the icon with three CSS spans — no image or icon library required:

```jsx
<button
  className="Title__menu-btn"
  aria-label={isOpen ? "Close navigation menu" : "Open navigation menu"}
  aria-expanded={isOpen}
  onClick={() => setIsOpen(!isOpen)}
>
  <span></span>
  <span></span>
  <span></span>
</button>
```

```css
.Title__menu-btn {
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  min-width: 44px;   /* touch target minimum */
  min-height: 44px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
}

.Title__menu-btn span {
  display: block;
  width: 24px;
  height: 2px;
  background: currentColor;
}
```

`aria-label` changes based on state — screen readers announce the current action. `aria-expanded` tells screen readers whether the controlled menu is open. `44px` minimum satisfies WCAG touch target requirements.

---

## Step 3: The Nav

Toggle a CSS class on the nav based on state. Use `aria-hidden` to hide the closed nav from screen readers:

```jsx
<nav
  className={`Title__nav${isOpen ? ' Title__nav--open' : ''}`}
  aria-hidden={!isOpen}
>
  <NavLink to="/" onClick={() => setIsOpen(false)}>List</NavLink>
  <NavLink to="/about" onClick={() => setIsOpen(false)}>About</NavLink>
</nav>
```

`onClick={() => setIsOpen(false)}` on each `NavLink` closes the menu when the user navigates — without this, the menu stays open after clicking a link.

---

## Step 4: CSS

Mobile-first — nav is hidden by default, hamburger button is visible. Media query flips both at the desktop breakpoint:

```css
/* Mobile: hide nav, show button */
.Title__nav {
  display: none;
  flex-direction: column;
}

.Title__nav--open {
  display: flex;
}

/* Desktop: always show nav, hide button */
@media (min-width: 768px) {
  .Title__nav {
    display: flex;
    flex-direction: row;
  }

  .Title__menu-btn {
    display: none;
  }
}
```

Note: `aria-hidden` on the nav doesn't affect CSS visibility — you still need `display: none` to hide it visually.

---

## Step 5: Smooth Open/Close Animation

`display: none` can't be animated. To get a smooth slide-in, use `max-height` instead:

```css
.Title__nav {
  max-height: 0;
  overflow: hidden;
  flex-direction: column;
  transition: max-height 0.3s ease;
}

.Title__nav--open {
  max-height: 300px;  /* larger than the nav will ever be */
}

@media (min-width: 768px) {
  .Title__nav {
    max-height: none;
    overflow: visible;
    flex-direction: row;
    transition: none;
  }

  .Title__menu-btn {
    display: none;
  }
}
```

---

## Step 6: Close on Outside Click

The menu should close when the user clicks anywhere outside it. Use a `useEffect` with a document-level click listener:

```jsx
import { useState, useEffect, useRef } from 'react'

function Title() {
  const [isOpen, setIsOpen] = useState(false)
  const navRef = useRef(null)

  useEffect(() => {
    function handleClickOutside(e) {
      if (navRef.current && !navRef.current.contains(e.target)) {
        setIsOpen(false)
      }
    }

    document.addEventListener('mousedown', handleClickOutside)
    return () => document.removeEventListener('mousedown', handleClickOutside)
  }, [])

  return (
    <header className="Title" ref={navRef}>
      ...
    </header>
  )
}
```

---

## Full Component

```jsx
import { useState, useEffect, useRef } from 'react'
import { NavLink } from 'react-router-dom'

function Title() {
  const [isOpen, setIsOpen] = useState(false)
  const headerRef = useRef(null)

  useEffect(() => {
    function handleClickOutside(e) {
      if (headerRef.current && !headerRef.current.contains(e.target)) {
        setIsOpen(false)
      }
    }
    document.addEventListener('mousedown', handleClickOutside)
    return () => document.removeEventListener('mousedown', handleClickOutside)
  }, [])

  return (
    <header className="Title" ref={headerRef}>
      <h1>SFPOPOS</h1>
      <button
        className="Title__menu-btn"
        aria-label={isOpen ? "Close navigation menu" : "Open navigation menu"}
        aria-expanded={isOpen}
        onClick={() => setIsOpen(!isOpen)}
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
      <nav
        className={`Title__nav${isOpen ? ' Title__nav--open' : ''}`}
        aria-hidden={!isOpen}
      >
        <NavLink to="/" onClick={() => setIsOpen(false)}>List</NavLink>
        <NavLink to="/about" onClick={() => setIsOpen(false)}>About</NavLink>
      </nav>
    </header>
  )
}

export default Title
```

---

## Challenge

Implement the hamburger menu in your SFPOPOS project following the steps above.

**Must have:**
- [ ] Hamburger button visible on mobile, hidden on desktop
- [ ] Full nav visible on desktop, hidden on mobile
- [ ] Menu opens and closes on button tap
- [ ] `aria-label` changes based on open/closed state
- [ ] `aria-expanded` reflects current state
- [ ] Menu closes when a nav link is clicked
- [ ] Touch target is at least 44×44px

**Stretch challenges:**
- Add a smooth open/close animation using `max-height` transition
- Close the menu on outside click using `useEffect`
- Animate the hamburger icon into an X when open (CSS transform on the spans)

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Functionality | Menu doesn't open/close or nav is broken on one size | Menu opens/closes on mobile, full nav on desktop | Closes on link click and outside click |
| CSS | Hamburger and nav visible simultaneously, or layout broken | Correct show/hide at breakpoint | Smooth transition on open/close |
| ARIA | No ARIA attributes | `aria-label` and `aria-expanded` present and correct | `aria-hidden` on nav, label changes with state |
| Touch target | Button too small to tap reliably | Button is at least 44×44px | Button has visible focus style for keyboard users |
