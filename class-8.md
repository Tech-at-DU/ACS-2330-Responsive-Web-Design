# Class 8: Responsive Navigation and the Hamburger Menu

The hamburger menu is one of the most common patterns in responsive web development. Every developer encounters it. It brings together everything from the first half of this course: media queries, CSS display toggling, Flexbox, ARIA, and React state.

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
  const [menuOpen, setMenuOpen] = useState(false)

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
  className="Title-menu-btn"
  aria-label={menuOpen ? "Close navigation menu" : "Open navigation menu"}
  aria-expanded={menuOpen}
  onClick={() => setMenuOpen(!menuOpen)}
>
  <span></span>
  <span></span>
  <span></span>
</button>
```

```css
.Title-menu-btn {
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

.Title-menu-btn span {
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
  className={`Title-nav${menuOpen ? ' Title-nav--open' : ''}`}
  aria-hidden={!menuOpen}
>
  <NavLink to="/" onClick={() => setMenuOpen(false)}>List</NavLink>
  <NavLink to="/about" onClick={() => setMenuOpen(false)}>About</NavLink>
</nav>
```

`onClick={() => setMenuOpen(false)}` on each `NavLink` closes the menu when the user navigates — without this, the menu stays open after clicking a link.

---

## Step 4: CSS

Mobile-first — nav is hidden by default, hamburger button is visible. Media query flips both at the desktop breakpoint:

```css
/* Mobile: hide nav, show button */
.Title-nav {
  display: none;
  flex-direction: column;
}

.Title-nav--open {
  display: flex;
}

/* Desktop: always show nav, hide button */
@media (min-width: 768px) {
  .Title-nav {
    display: flex;
    flex-direction: row;
  }

  .Title-menu-btn {
    display: none;
  }
}
```

Note: `aria-hidden` on the nav doesn't affect CSS visibility — you still need `display: none` to hide it visually.

---

## Step 5: Smooth Open/Close Animation

`display: none` can't be animated. To get a smooth slide-in, use `max-height` instead:

```css
.Title-nav {
  max-height: 0;
  overflow: hidden;
  flex-direction: column;
  transition: max-height 0.3s ease;
}

.Title-nav--open {
  max-height: 300px;  /* larger than the nav will ever be */
}

@media (min-width: 768px) {
  .Title-nav {
    max-height: none;
    overflow: visible;
    flex-direction: row;
    transition: none;
  }

  .Title-menu-btn {
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
  const [menuOpen, setMenuOpen] = useState(false)
  const navRef = useRef(null)

  useEffect(() => {
    function handleClickOutside(e) {
      if (navRef.current && !navRef.current.contains(e.target)) {
        setMenuOpen(false)
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
  const [menuOpen, setMenuOpen] = useState(false)
  const headerRef = useRef(null)

  useEffect(() => {
    function handleClickOutside(e) {
      if (headerRef.current && !headerRef.current.contains(e.target)) {
        setMenuOpen(false)
      }
    }
    document.addEventListener('mousedown', handleClickOutside)
    return () => document.removeEventListener('mousedown', handleClickOutside)
  }, [])

  return (
    <header className="Title" ref={headerRef}>
      <h1>SFPOPOS</h1>
      <button
        className="Title-menu-btn"
        aria-label={menuOpen ? "Close navigation menu" : "Open navigation menu"}
        aria-expanded={menuOpen}
        onClick={() => setMenuOpen(!menuOpen)}
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
      <nav
        className={`Title-nav${menuOpen ? ' Title-nav--open' : ''}`}
        aria-hidden={!menuOpen}
      >
        <NavLink to="/" onClick={() => setMenuOpen(false)}>List</NavLink>
        <NavLink to="/about" onClick={() => setMenuOpen(false)}>About</NavLink>
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
