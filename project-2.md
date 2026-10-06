# Project 2: Responsive Website

Build a responsive website with React and Tailwind CSS. It can be something new, or an existing project from a previous course that you rebuild to be responsive. It's planned with wireframes, UX tested, and presented in [class-14](./class-14.md).

**Due:** Thu, Oct 8 (class 14) — 35% of your final grade. You must pass Project 2 to pass the course.

## Requirements

Your project must be:

- **Responsive** — works at phone (375px), tablet (768px), and desktop (1280px) widths
- **Mobile-first** — built for mobile first, with Tailwind `md:` / `lg:` prefixes adding the desktop layout
- **Built with Tailwind CSS** — responsive prefixes, not vanilla media queries
- **Navigable on mobile** — a hamburger menu with ARIA on small screens
- **Accessible** — semantic HTML, alt text, labels, keyboard navigation, Lighthouse accessibility ≥ 90
- **Planned and UX tested** — built from your wireframes, with the changes from your UX test applied (A4)
- **Deployed** — live at a public URL, with the code on GitHub

---

## Rubric

To pass, every category must be **Meets** or **Exceeds**. A **Does not meet** in any category is a requirement to fix before you submit.

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| **Responsive layout** | Horizontal scroll or content cut off at 375px, or desktop is a stretched phone layout | No overflow at 375 / 768 / 1280px; at least one layout changes between mobile and desktop | Layout is tuned at each size — spacing, type, and column counts all change on purpose |
| **Mobile-first Tailwind** | Vanilla media queries, or desktop-first classes (`max-md:`) throughout | Base classes are the mobile layout; `sm:` / `md:` / `lg:` add larger-screen changes; spacing uses the Tailwind scale | Uses modern CSS where it fits — `clamp()` type, `dvh`, or container queries — and can explain why |
| **Navigation** | No working nav on mobile, or hamburger doesn't open/close | Hamburger opens and closes on mobile, has `aria-label` and updating `aria-expanded`, full nav shown on desktop | Menu is fully keyboard-usable, closes on link click / Escape / outside click, focus is managed |
| **Accessibility** | Lighthouse accessibility below 90, or images missing alt text / inputs missing labels | Lighthouse ≥ 90 on every page; alt text, labels, and `aria-label` on icon buttons present; Tab works through the page with visible focus | 95+ on every page; semantic landmarks (`header`, `nav`, `main`, `footer`); contrast checked beyond Lighthouse |
| **Touch and mobile UX** | Tap targets too small or text unreadable without zooming at 375px | Buttons and links ≥ 44px tall; no text smaller than ~14px on mobile; tested on a real phone | Forms (if any) use the right input types and `autocomplete`; no layout jumps when the phone's address bar moves |
| **Plan → Build** | Site doesn't match the wireframes; UX test changes not applied | Every wireframe page is built; site matches the wireframes at mobile and desktop; the 2–3 UX test changes are visible in the site | Can explain each change from wireframe to final build and the reason for it |
| **Code and deployment** | Not deployed, or console errors, or everything in one file | Live URL works; repo is pushed and the README has the live URL; components are split clearly; no console errors or commented-out blocks | Clean commit history; README explains the project, how to run it, and what changed after UX testing |

---

## Requirements Checklist

Use this checklist to find out where you stand on each rubric category. It's what you'll use in the class-13 peer review, and it's what you should run against your own project before you submit.

Mark each item pass or fail — no partial credit, no "sort of." If something isn't clearly working, it fails. Check the code and the DOM, not just what you see on screen.

### Responsive layout

- [ ] Works at 375px — no horizontal scroll, no content cut off
- [ ] Works at 768px — nothing awkward in the in-between size
- [ ] Works at 1280px — layout uses available space, not a stretched phone layout
- [ ] At least one layout changes between mobile and desktop (column count, stack to row, etc.)
- [ ] No fixed pixel widths causing overflow on mobile

### Mobile-first Tailwind

- [ ] Base classes are the mobile layout, `md:` / `lg:` add the desktop changes
- [ ] Tailwind responsive prefixes used — not vanilla CSS media queries
- [ ] No hardcoded pixel values that should be Tailwind spacing scale
- [ ] Utility classes are legible — not a wall of 30+ classes on one element without reason

### Navigation

- [ ] Hamburger menu appears on mobile and opens and closes
- [ ] Menu button has `aria-label` and `aria-expanded` that updates (check in the Elements panel)
- [ ] Menu is reachable and usable with the keyboard (Tab to it, Enter to open)
- [ ] Desktop shows the full nav — no hamburger at 1280px

### Accessibility

- [ ] All images have `alt` text (check the DOM)
- [ ] All form inputs (if any) have visible labels above the input
- [ ] Icon-only buttons have `aria-label`
- [ ] Lighthouse accessibility score ≥ 90 on every page
- [ ] Can Tab through the page without getting stuck, and focus is visible

### Touch and mobile UX

- [ ] Buttons and links are at minimum 44px tall
- [ ] Text is readable at 375px without zooming
- [ ] No text smaller than ~14px on mobile
- [ ] Tested on a real phone, not just DevTools

### Plan → Build

- [ ] Each page in the wireframes exists in the site
- [ ] The layout matches the wireframes at mobile and desktop (or the change is a deliberate improvement the author can explain)
- [ ] Each of the 2–3 changes from the UX test summary is visible in the site — point to where

### Code and deployment

- [ ] Live URL works
- [ ] Latest work is pushed to GitHub, and the README has the live URL
- [ ] Component structure is clear — not everything in one file
- [ ] No console errors in the browser
- [ ] No commented-out code blocks left in

---

## Submit

Submit to Gradescope by class 14:

1. Your **live URL**
2. Your **GitHub repo link**
3. A **self-assessment**: your rating (Does not meet / Meets / Exceeds) for each rubric category, with one sentence of evidence for each

---

## Planning Guide

Use this guide when you plan your project in [class-10](./class-10.md). Your content map, user stories, and wireframes are submitted with A4.

### Create a site map

1. **Identify Website Goals**: Understand the purpose of the website and the key objectives it needs to fulfill. This will help in determining the main sections and pages needed.
2. **List Main Sections**: Identify the primary sections or categories that will make up your website. These could be Home, About Us, Services, Products, Blog, Contact, etc.
3. **Outline Subsections**: Under each main section, outline the subsections or pages that will fall within them. For example, under Services, you might have pages like Consulting, Design, Development, etc.
4. **Establish Navigation Flow**: Determine how users will navigate through your site. Design a logical flow of information starting from the homepage, through main sections, and into subsections.
5. **Use Visual Hierarchy**: Represent the hierarchy of your pages visually. Use indentation, shapes, or connecting lines to show parent-child relationships between sections and pages.
6. **Consider User Experience**: Ensure the sitemap reflects an intuitive and user-friendly structure. Pages should be organized logically, making it easy for visitors to find what they are looking for.
7. **Review and Revise**: After creating the initial sitemap, review it critically. Check for completeness, clarity, and consistency. Make revisions as necessary to refine the structure.
8. **Create Digital Version**: Once finalized, create a digital version of the sitemap using tools like diagramming software, graphic design tools, or sitemap generators available online.
9. **Share and Gather Feedback**: Share the sitemap with stakeholders such as clients, team members, or instructors. Gather feedback to ensure the structure meets the project requirements and goals.
10. **Update as Needed**: Remember that a sitemap is a living document. As the website evolves or requirements change, update the sitemap accordingly to maintain a clear representation of the site's structure.

### Write User stories 

1. **Role**: Start by identifying the user or role for whom the story is being written (e.g., "As a customer," "As an admin").
2. **Action**: Describe what the user wants to accomplish (e.g., "I want to browse products," "I need to update my profile").
3. **Outcome**: Specify the goal or benefit of the action (e.g., "So I can make a purchase easily," "To keep my information up-to-date").
4. **Format**: Write the user story in a simple template like: "As a [role], I want [action], so that [outcome]."
5. **Keep it Simple**: Focus on the essential details and avoid technical jargon or implementation specifics.
6. **Prioritize**: Rank user stories based on importance to guide development and prioritize features.
7. **Iterate**: Refine and update user stories as you gather feedback and requirements evolve during the project.

### Create your wireframes 

1. **Define Purpose and Scope**: Understand the purpose of the webpage or application and define its key functionalities.
2. **Identify Key Elements**: Determine the essential elements to include, such as navigation bars, content sections, buttons, forms, and media.
3. **Sketch Initial Layout**: Start with rough sketches using pen and paper or digital tools. Focus on positioning key elements and defining overall structure.
4. **Use Wireframing Tools**: Transition to digital wireframing tools like Sketch, Figma, Adobe XD, or wireframe.cc to create more refined layouts.
5. **Create Low-Fidelity Wireframes**: Begin with low-fidelity wireframes, emphasizing structure over visual details. Use basic shapes and placeholders for content.
6. **Focus on User Flow**: Ensure a clear and intuitive flow of information. Design how users will navigate through the interface.
7. **Iterate and Refine**: Gather feedback from stakeholders and team members. Revise wireframes based on feedback to improve clarity and usability.
8. **Add Detail**: Gradually add more detail to wireframes, incorporating typography, color schemes, and actual content where appropriate.
9. **Review for Consistency**: Ensure consistency in design elements and alignment throughout the wireframes.
10. **Finalize and Share**: Once approved, finalize the wireframes and share with the development team as a blueprint for implementation.

