# Class 13: Project 2 Lab — Peer Review, Fix, Deploy, Rehearse

Presentations are Thursday. Tonight is about getting Project 2 finished and meeting the requirements — not adding new features. You'll find out exactly what's missing (from a peer, against a checklist), fix it with help in the room, get it deployed, and rehearse your presentation once so Thursday has no surprises.

## Objectives

- Score a peer's Project 2 against the Project 2 rubric
- Turn feedback into a prioritized fix list and work through it
- Deploy Project 2 to a live URL and test it on a real phone
- Rehearse the 5-minute class-14 presentation

---

## Today's Time Plan (2:45 total)

| Time | Activity |
|------|----------|
| 10 min | Blocker triage + self-check at 375px |
| 45 min | Peer review against the Project 2 rubric |
| 5 min | Break |
| 75 min | Lab: fix list, deploy, phone test (checkpoint at 35 min) |
| 20 min | Presentation dry run in pairs |
| 10 min | Exit ticket — submit live URL and repo |

No lecture tonight. Every minute is spent on your project.

---

## Blocker Triage + Self-Check (10 mins)

**Blockers first.** Look at what you wrote in the class-12 exit ticket under "what's still blocking you." If it's still blocking you, put your name and the blocker on the board (or in the class channel) now. The instructor works through this list during lab time — the earlier it's posted, the sooner you get help.

**Self-check.** Open your project in DevTools at 375px (iPhone SE). Scroll every page top to bottom. Write down anything that's obviously broken before your partner finds it. This is the start of your fix list.

---

## Peer Review (45 mins)

Pair up with someone you did **not** pair with for the class-10 UX test. Fresh eyes find more.

Before you start, give your partner:
- Your repo link (and live URL if you have one)
- Your **A4 UX test summary** — the 2–3 changes you said you'd make
- Your **updated wireframes**

Each review takes 20 minutes. Spend the last 5 minutes writing up feedback for each other.

Open the [Project 2 rubric and requirements checklist](./project-2.md#rubric) side by side with your partner's project.

1. **Run the checklist.** Go through every item in the [Requirements Checklist](./project-2.md#requirements-checklist). Mark each as pass or fail — no partial credit, no "sort of." If something isn't clearly working, mark it fail. Checking is the job — "looks fine" is not checking. Check the code and the DOM, not just what's on screen.
2. **Score the rubric.** For each of the 7 rubric categories, rate your partner's project Does not meet / Meets / Exceeds. A checklist fail in a category almost always means **Does not meet** for that category.

This is the same rubric the project is graded on. A Does not meet tonight is a fail on Thursday unless it gets fixed.

### Feedback Format

Write your feedback in three sections and send it to your partner (DM, shared doc, or GitHub issue on their repo):

**Rubric scores:**
One line per category — the rating and the reason. Example: "Navigation — Does not meet: `aria-expanded` stays `false` when the menu is open."

**Fails (must fix before presentation):**
List every checklist item that failed. Be specific — "images missing alt text on the About page, hero and team photos" is better than "accessibility issues." Include the page and element.

**Suggestions (nice to have):**
Two or three things that would improve the project but aren't on the checklist. These are optional — fails come first.

---

## Lab: Fix, Deploy, Phone Test (75 mins)

### First 5 min — build your fix list

Combine your self-check notes and your partner's fails into one list, sorted into three groups:

| Must fix (Does not meet / checklist fails) | Should fix (hurts the demo) | Could fix (only if time) |
|------------------------------|-----------------------------|--------------------------|
| No `aria-expanded` on menu button | Hero text too big at 375px | Hover animation on cards |
| Horizontal scroll on Contact page | | |

Work top to bottom. Do not touch the "could" column until the "must" column is empty. A finished, plain project beats a beautiful one with a broken menu.

### Common fixes

| Problem | Where to look |
|---------|---------------|
| Horizontal scroll at 375px | Find the culprit: DevTools → Elements, hover elements until one sticks out past the edge. Usually a fixed `w-[600px]`, a wide image (add `max-w-full`), or a long unbroken string (add `break-words`) |
| Lighthouse below 90 | Lighthouse lists each failing item and the element. Usually contrast, missing alt, missing labels, or buttons without names — see [class-6](./class-6.md) and [class-7](./class-7.md) |
| Hamburger missing ARIA | `aria-label="Open menu"`, `aria-expanded={isOpen}`, `aria-controls` pointing to the menu `id` — see [class-8](./class-8.md) |
| Desktop-first classes | Base class should be mobile. `flex-col md:flex-row`, not `flex-row max-md:flex-col` — see [class-9](./class-9.md) |
| Full-screen hero jumps on phone | Replace `h-screen` with `h-dvh` — see [class-12](./class-12.md) |
| Headings too big on mobile | `text-[clamp(1.75rem,5vw,3rem)]` — see [class-12](./class-12.md) |

### Checkpoint (~35 min in)

Stop. Count your "must fix" items left. If it's more than two, raise your hand — tell the instructor which ones. Don't wait until the end of class to discover you're stuck.

### Deploy

If your project is not already live, deploy it now. You'll present Thursday from a live URL, and testing on a real phone is the only way to catch some problems.

For a Vite + React project, either works in under 10 minutes:

- **Vercel:** [vercel.com](https://vercel.com) → Add New Project → import your GitHub repo → Deploy. Vite is detected automatically.
- **Netlify:** [netlify.com](https://netlify.com) → Add new site → Import from Git → build command `npm run build`, publish directory `dist`.

Every push to `main` redeploys automatically after that.

If you use React Router and a page 404s when you refresh it, add a rewrite so all routes serve `index.html`:
- Vercel — `vercel.json`: `{ "rewrites": [{ "source": "/(.*)", "destination": "/" }] }`
- Netlify — `public/_redirects`: `/*  /index.html  200`

Add the live URL to your repo's README and the GitHub "About" section.

### Real phone test

Open your live URL on your own phone. DevTools at 375px is a simulation — a real phone is the test. Check:

- [ ] Hamburger menu works with your thumb
- [ ] Nothing jumps when the address bar shows and hides
- [ ] Form inputs (if any) bring up the right keyboard and don't zoom the page
- [ ] Images load and aren't huge

Anything that fails goes on your fix list.

---

## Presentation Dry Run (20 mins)

Thursday's format is in [class-14](./class-14.md): 5 minutes — mobile view (2 min), desktop view (1 min), one technical decision (1 min), what you'd change (1 min).

With your peer review partner, run it once for real. The partner keeps time and stops you at 5:00.

**Presenter:** use the live URL, not localhost. Say your technical decision out loud — if it takes more than a minute, cut it down.

**Partner:** after the run, give two notes:
1. One thing that worked
2. Where time ran over, or what was unclear

Then switch.

Before you leave, write down:
- Which page you'll show for the responsive pattern
- Your one technical decision, in one sentence
- Your one "what I'd change"

---

## Exit Ticket (10 mins)

Submit:
1. Your **live URL**
2. Your **GitHub repo link** (verify it's the latest push)
3. Your self-assessed rubric score for each category, and your remaining "must fix" items — or "none"

If anything is still in "must fix," that's your plan for Wednesday. Office hours are available — use them before Thursday, not after.

---

## Before Thursday

- [ ] Every "must fix" item done — every rubric category at Meets or better
- [ ] Lighthouse accessibility ≥ 90
- [ ] No horizontal scroll at 375px
- [ ] Live URL works on your phone
- [ ] Final version pushed to GitHub and redeployed
- [ ] Presentation points written down: responsive page, technical decision, what you'd change

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Peer review quality | Checklist items skipped or marked pass without checking | All items checked, every rubric category scored with a reason, fails identified with page and element | Feedback is specific and actionable, and checks the code (mobile-first, ARIA) and not only what's on screen |
| Responsiveness | Horizontal scroll or broken layout on mobile | No overflow, layout changes at breakpoints, tested on a real phone | Intentional mobile-specific adjustments (text size, spacing, interaction) |
| Accessibility | Below 90 Lighthouse score | 90+ Lighthouse, alt text and labels present | 90+, keyboard navigation verified, ARIA attributes correct |
| Plan → Build | Site doesn't match wireframes, UX findings not applied | Wireframe pages built, UX test changes visible in the site | Can explain each change from wireframe to final build and why |
| Lab progress | Same issues at end of class as at start | All "must fix" items addressed, project deployed | Project polished, deployed, and presentation rehearsed — no known issues |
