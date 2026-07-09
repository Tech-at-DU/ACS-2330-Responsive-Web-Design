# Class 14: Final Presentations

This is the last class. Each student presents Project 2. Presentations are short and structured — you're not giving a lecture, you're demonstrating a working product and reflecting on what you built.

## Objectives

- Present Project 2 on both mobile and desktop
- Articulate one specific technical decision you made
- Identify what you'd do differently with more time

---

## Presentation Format

Each student gets **5 minutes**. Presentations run back to back — be ready when it's your turn.

### What to show

**1. Mobile view (2 min)**

Open your site on an actual phone or in Chrome DevTools at 375px (iPhone SE). Show:
- The home page — does the layout work?
- The navigation — show the hamburger menu opening and closing
- One other page that demonstrates a responsive pattern (grid, form, or other layout change)

**2. Desktop view (1 min)**

Resize to full desktop. Show the same pages. The differences between mobile and desktop should be visible and intentional.

**3. One technical decision (1 min)**

Tell us one specific thing you implemented and why you made it the way you did. Examples:
- "I used `grid-template-areas` for the detail page because my wireframe had a layout that was hard to express with flex"
- "I added container queries to the card component so it works in both the grid and the sidebar"
- "I used `clamp()` on the headings instead of media queries because..."

Don't summarize everything. Pick one thing you're proud of or that you learned the most from.

**4. What you'd change (1 min)**

One honest answer: what would you do differently if you had more time? This isn't self-deprecation — it shows you can evaluate your own work.

---

## Before Presentations Start

Run through this checklist before class begins:

- [ ] Project is running (start it now, don't debug during your turn)
- [ ] Mobile view is ready — device or DevTools open at 375px
- [ ] You know which page shows the hamburger menu
- [ ] You've picked your one technical decision
- [ ] GitHub repo is pushed — final version, not a WIP commit

If you're demoing on your phone, have the URL open before class. There's no time to type a URL during your 5 minutes.

---

## Grading

Project 2 is 35% of your grade. Presentations are not graded separately — the presentation is your opportunity to show that the project works. A project that works on mobile and desktop speaks for itself.

See [project-2.md](./project-2.md) for the full rubric.

---

## After Presentations

After everyone has presented, we'll take 15 minutes for group reflection:

- What was the hardest part of making a site responsive?
- What's the one thing you'll do differently on your next project?
- What concept from this course will you use most in your work going forward?

There are no wrong answers. This is a chance to hear how other people approached the same problems.

---

## What You've Built

Over these 7 weeks you've covered:

- Responsive wireframing and planning
- Mobile-first media queries
- Responsive Flexbox and Grid patterns
- Hamburger menu with React state and ARIA
- Tailwind CSS utility classes and responsive prefixes
- Accessibility: semantic HTML, keyboard navigation, screen reader support, color contrast
- Responsive forms
- Modern CSS: `clamp()`, container queries, dynamic viewport units
- UX testing methodology

These are not beginner skills. Responsive design, accessibility, and Tailwind CSS are all standard expectations in front-end job descriptions. You've practiced all three together.
