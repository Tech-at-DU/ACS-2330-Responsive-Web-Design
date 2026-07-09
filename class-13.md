# Class 13: Peer Review Lab

This class is structured time to get your Project 2 as close to complete as possible before presentations. You'll give and receive structured feedback, then use the remaining time to act on it.

## Objectives

- Review a peer's Project 2 against the rubric criteria
- Receive and prioritize actionable feedback
- Implement fixes and improvements before the final presentation

---

## How This Class Works

The first 60 minutes is structured peer review. You review one project, they review yours. Reviews are done against the pass/fail checklist below — not opinions, just the checklist.

The remaining 80 minutes is lab time. Fix what's broken, implement what's missing, polish what's close.

---

## Peer Review Checklist

Clone or open your partner's project. Go through every item. Mark each as pass or fail — no partial credit, no "sort of." If something isn't clearly working, mark it fail.

### Responsive Layout

- [ ] The site works on mobile (375px) — no horizontal scroll, no content cut off
- [ ] The site works on desktop (1280px) — layout uses available space
- [ ] At least one layout changes between mobile and desktop (column count, stack to row, etc.)
- [ ] No fixed pixel widths causing overflow on mobile

### Tailwind CSS

- [ ] Tailwind responsive prefixes used (`sm:`, `md:`, `lg:`) — not vanilla CSS media queries
- [ ] No hardcoded pixel values that should be Tailwind spacing scale
- [ ] Utility classes are legible — not a wall of 30+ classes on one element without reason

### Navigation

- [ ] Navigation is present and functional on mobile
- [ ] If there is a hamburger menu: it opens and closes, focus works, clicking outside closes it
- [ ] If no hamburger: nav is accessible and readable on mobile without one

### Accessibility

- [ ] All images have `alt` text (check the DOM, not just visually)
- [ ] All form inputs (if any) have visible labels above the input
- [ ] Icon-only buttons have `aria-label`
- [ ] Lighthouse accessibility score ≥ 85 (run it now if needed)
- [ ] Keyboard navigation: can Tab through the page without getting stuck

### Touch and Mobile UX

- [ ] Buttons and links are at minimum 44px tall
- [ ] Text is readable at 375px without zooming
- [ ] No text smaller than ~14px on mobile

### Code Quality

- [ ] No commented-out code blocks left in
- [ ] Component structure is clear — not everything in one file
- [ ] No console errors in the browser

---

## Feedback Format

Write your feedback in two sections:

**Fails (must fix before presentation):**
List every item that failed the checklist. Be specific — "images missing alt text" is better than "accessibility issues." Include the element or page where you found the problem.

**Suggestions (nice to have):**
Two or three things that would improve the project but aren't on the checklist. These are optional — address the fails first.

Share your written feedback with your partner before the lab period starts.

---

## Lab Time (80 mins)

Prioritize your fixes in this order:

1. **Checklist fails** — anything that got a fail is a requirement, not optional
2. **Lighthouse accessibility** — if you're below 85, find and fix the specific failures (Lighthouse tells you what they are)
3. **Mobile layout** — if anything overflows or breaks at 375px, fix it now
4. **Polish** — only after the above are done

If you're not sure how to fix something, ask. Use class time to get unstuck, not to discover problems at 11pm before presentations.

---

## End of Class

By end of class you should have:
- [ ] All checklist fails addressed
- [ ] Lighthouse accessibility ≥ 85
- [ ] No horizontal scroll on mobile
- [ ] Project pushed to GitHub (verify your submitted repo link is current)

If you're not there, use office hours or time before next class.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Peer review quality | Checklist items skipped or marked pass without checking | All items checked, fails clearly identified with specific location | Written feedback includes specific elements and pages, actionable |
| Responsiveness | Horizontal scroll or broken layout on mobile | No overflow, layout changes at breakpoints | Intentional mobile-specific adjustments (text size, spacing, interaction) |
| Accessibility | Below 85 Lighthouse score | 85+ Lighthouse, alt text and labels present | 90+, keyboard navigation verified, ARIA attributes correct |
| Lab progress | Same issues at end of class as at start | Checklist fails addressed, project is presentable | Project is polished and ready — no known issues |
