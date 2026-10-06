# Class 13: Project 2 Lab — UX Test, Peer Review, Fix, Rehearse

Presentations are Thursday. Tonight is about getting Project 2 finished and meeting the requirements — not adding new features. You'll watch a classmate use your built site, find out exactly what's missing (against the rubric), fix it with help in the room, and rehearse your presentation once so Thursday has no surprises.

Most of tonight runs in Zoom breakout rooms with a partner. The instructor won't be in your room, so everything you need is written out below as numbered steps. Follow them in order and watch the clock.

## Objectives

- UX test a peer's built Project 2 and observe a peer using yours
- Score a peer's Project 2 against the [Project 2 rubric](./project-2.md#rubric)
- Turn feedback into a prioritized fix list and work through it
- Rehearse the 5-minute class-14 presentation

---

## Today's Time Plan (2:45 total)

| Time | Where | Activity |
|------|-------|----------|
| 15 min | Main room | **Part 1 — Get ready:** deploy, write UX tasks, prepare your share message |
| 55 min | Breakout room | **Part 2 — UX test + peer review** with your partner |
| 5 min | — | Break |
| 60 min | Main room | **Part 3 — Lab:** fix list, fixes, real phone test |
| 20 min | Breakout room (same partner) | **Part 4 — Presentation practice** |
| 10 min | Main room | **Part 5 — Exit ticket** |

No lecture tonight. Every minute is spent on your project.

**Zoom chat disappears when a breakout room closes.** Keep your notes in a file on your computer, and send feedback as a GitHub issue (steps below) — not in Zoom chat.

---

## Part 1 — Get Ready (Main room, 15 mins)

Do these on your own before breakout rooms open.

### Step 1: Post your blocker (1 min)

If something has been blocking you since class 12, post it in Zoom chat: `Blocker: <your name> — <what's stuck>`. The instructor works through this list during the lab.

### Step 2: Deploy your site (8 mins)

Your partner needs a **live URL** to test your site from their own computer. If you're already deployed, skip to Step 3.

**Vercel (recommended for Vite + React):**
1. Push your latest code to GitHub.
2. Go to [vercel.com](https://vercel.com) → sign in with GitHub.
3. **Add New** → **Project** → find your repo → **Import**.
4. Leave the settings as they are (Vite is detected) → **Deploy**.
5. Copy the URL it gives you (`https://your-project.vercel.app`) and open it to check it works.

**Netlify (alternative):** [netlify.com](https://netlify.com) → **Add new site** → **Import an existing project** → GitHub → pick your repo → build command `npm run build`, publish directory `dist` → **Deploy**.

**Page 404s when you refresh it?** You're using React Router and need a rewrite so every route serves `index.html`:
- Vercel — add `vercel.json` to the project root: `{ "rewrites": [{ "source": "/(.*)", "destination": "/" }] }`
- Netlify — add `public/_redirects` containing: `/*  /index.html  200`

Push, and it redeploys on its own.

**Deploy failing and you can't fix it in 8 minutes?** Stop. Post `Deploy stuck: <your name>` in chat and move on. In the breakout room you'll share your screen instead (see the fallback in Part 2). Fix the deploy during the lab.

### Step 3: Write 3 UX test tasks (4 mins)

Pull them from your user stories — the most important things a visitor comes to your site to do. Write each as a **goal, not instructions**:

- Good: "Find out what time the gallery opens on Saturday."
- Bad: "Click the hamburger menu, then click Hours."

If the task tells the tester where to click, you're not testing anything.

### Step 4: Write your share message (2 mins)

Put this in a text file so you can paste it into breakout chat:

```
Name:
Live URL:
Repo:
Wireframes: (link)
My UX test changes from A4 (the 2-3 things I said I'd change):
1.
2.
3.
```

Don't paste your UX tasks — your partner shouldn't see them before the test.

---

## Part 2 — UX Test + Peer Review (Breakout room, 55 mins)

The instructor will put you in a breakout room with a partner. If you're in a room of 3, see [Groups of 3](#groups-of-3) below.

### Step 1: Set up (3 mins)

1. Turn cameras on and say hi.
2. Decide who is **Partner A** and who is **Partner B**: A is whoever's first name comes first alphabetically.
3. Both paste your share message into the breakout chat.
4. Both copy your partner's share message into your own notes file — the chat will be gone when the room closes.
5. Open your partner's live URL to make sure it loads.

### Step 2: UX test Partner A's site (10 mins)

**Partner B is the tester. Partner A is the observer.**

**B (tester):**
1. Open A's live URL in Chrome.
2. Turn on phone view: open DevTools (`Cmd+Option+I` / `Ctrl+Shift+I`) → toggle the device toolbar (`Cmd+Shift+M` / `Ctrl+Shift+M`) → pick **iPhone SE** from the device menu at the top.
3. **Share your screen** in Zoom.
4. Use the mouse like a finger: click and scroll only, no DevTools.
5. **Think out loud the whole time** — "I'm looking for... I expected this to... I'm not sure if..."

**A (observer):**
1. Read your first task out loud. Say nothing else.
2. **Don't help, don't explain, don't defend.** Silence is hard — that's the point. If B is stuck for more than a minute, say "Let's move on" and read the next task.
3. Take notes in this table as you watch:

| Task | Completed? (Yes / Partly / No) | Where they hesitated or went wrong | What they said (exact words) |
|------|-----------|---------------------|----------------|
| | | | |
| | | | |
| | | | |

4. After the 3 tasks, ask B one question: "What was the most confusing part?" Write down the answer.

**Watch the clock:** about 7 minutes testing, 3 minutes for A to finish notes.

**Fallback — A's site isn't deployed:** A shares their screen with DevTools at iPhone SE instead. B tells A where to click and scroll ("click the menu icon," "scroll down"). A does **exactly** what B says — nothing more — and still says nothing else.

### Step 3: UX test Partner B's site (10 mins)

Switch roles and repeat Step 2. **A is the tester, B is the observer.**

### Step 4: Peer review — both at once (20 mins)

Now you switch from visitor to reviewer. You'll each review your partner's project **at the same time**, working quietly. Stay in the room so you can ask questions — "where's your nav component?"

1. Open your partner's live URL, their repo, and the [Requirements Checklist](./project-2.md#requirements-checklist) side by side.
2. Go through **every** checklist item. Mark each **pass** or **fail** — no partial credit, no "sort of." If something isn't clearly working, it fails. Check the code and the DOM, not just what's on screen.
   - Responsive: check 375px, 768px, and 1280px in device mode
   - Accessibility: run Lighthouse (DevTools → **Lighthouse** tab → check **Accessibility** → **Analyze page load**)
   - Plan → Build: compare the site to their wireframes and their 3 UX test changes from the share message
3. Rate each of the 7 [rubric](./project-2.md#rubric) categories: **Does not meet / Meets / Exceeds**. A checklist fail in a category almost always means **Does not meet**.

This is the same rubric the project is graded on. A Does not meet tonight is a fail on Thursday unless it gets fixed.

### Step 5: Send your feedback (7 mins)

Post your review as a **GitHub issue** on your partner's repo so it doesn't get lost: go to their repo → **Issues** → **New issue** → title `Peer review — <your name>` → paste and fill in this template → **Submit**.

```
## Rubric scores
- Responsive layout:
- Mobile-first Tailwind:
- Navigation:
- Accessibility:
- Touch and mobile UX:
- Plan → Build:
- Code and deployment:

## Fails (must fix before Thursday)
- [ ]
- [ ]

## Suggestions (nice to have)
-
-
```

Write a rating and a reason for each rubric line. Example: `Navigation — Does not meet: aria-expanded stays false when the menu is open.`

Be specific in fails: "images missing alt text on the About page, hero and team photos" beats "accessibility issues." Include the page and element.

If your partner's repo has issues turned off, paste the review into a DM instead.

### Step 6: Talk it through (5 mins)

Each person takes 2 minutes:
1. Read your partner's issue.
2. Ask about anything that's unclear.
3. Say your top fix out loud — the one thing you'll do first in the lab.

Then wait for the room to close, or return to the main room.

### Groups of 3

Rotate so everyone tests one person and is tested by one person: **A tests B, B tests C, C tests A.** Shorten each UX test to 7 minutes. For the peer review, each person reviews the same person they tested. Everything else is the same.

---

## Break (5 mins)

---

## Part 3 — Lab (Main room, 60 mins)

Work on your own. Stay in Zoom with your mic muted. For help, post in chat or use the **Raise hand** reaction — the instructor may pull you into a breakout room to help.

### Step 1: Build your fix list (5 mins)

Combine your UX test notes and your partner's GitHub issue into one list, sorted into three groups:

| Must fix | Should fix | Could fix |
|----------|------------|-----------|
| Rubric **Does not meet**, checklist fails, UX tasks the tester **couldn't complete** | UX hesitation or confusion, anything that hurts the demo | Only if time is left |
| *No `aria-expanded` on menu button* | *Hero text too big at 375px* | *Hover animation on cards* |
| *Horizontal scroll on Contact page* | | |

Work top to bottom. Do not touch the "could" column until the "must" column is empty. A finished, plain project beats a beautiful one with a broken menu.

### Step 2: Fix (until the checkpoint)

Check items off in the GitHub issue as you go. Commit and push after each fix — your live site redeploys every time.

**Common fixes:**

| Problem | Where to look |
|---------|---------------|
| Horizontal scroll at 375px | Find the culprit: DevTools → Elements, hover elements until one sticks out past the edge. Usually a fixed `w-[600px]`, a wide image (add `max-w-full`), or a long unbroken string (add `break-words`) |
| Lighthouse below 90 | Lighthouse lists each failing item and the element. Usually contrast, missing alt, missing labels, or buttons without names — see [class-6](./class-6.md) and [class-7](./class-7.md) |
| Hamburger missing ARIA | `aria-label="Open menu"`, `aria-expanded={isOpen}`, `aria-controls` pointing to the menu `id` — see [class-8](./class-8.md) |
| Desktop-first classes | Base class should be mobile. `flex-col md:flex-row`, not `flex-row max-md:flex-col` — see [class-9](./class-9.md) |
| Full-screen hero jumps on phone | Replace `h-screen` with `h-dvh` — see [class-12](./class-12.md) |
| Headings too big on mobile | `text-[clamp(1.75rem,5vw,3rem)]` — see [class-12](./class-12.md) |
| UX tester couldn't find something | Move it higher on the page, put it in the nav, or rename the link to the words the tester used |

### Step 3: Checkpoint (~30 mins in)

Stop. Count your "must fix" items left. If it's more than two, post in chat: `Checkpoint: <your name> — <number> must-fix left: <list>`. Don't wait until the end of class to discover you're stuck.

If your deploy failed in Part 1, fix it now — you need a live URL for Thursday.

### Step 4: Real phone test (5 mins, before the lab ends)

Open your live URL on your own phone. DevTools at 375px is a simulation — a real phone is the test. Check:

- [ ] Hamburger menu works with your thumb
- [ ] Nothing jumps when the address bar shows and hides
- [ ] Form inputs (if any) bring up the right keyboard and don't zoom the page
- [ ] Images load and aren't huge

Anything that fails goes on your fix list.

Add your live URL to your repo's README and the GitHub **About** section.

---

## Part 4 — Presentation Practice (Breakout room, 20 mins)

Same partner as Part 2. Thursday's format is in [class-14](./class-14.md): 5 minutes total.

### Step 1: Partner A presents (5 mins)

**A (presenter):** share your screen and present from your **live URL**, not localhost:
1. **Mobile view (2 min)** — DevTools at iPhone SE: home page, open and close the hamburger menu, one other page with a responsive pattern
2. **Desktop view (1 min)** — same pages at full width
3. **One technical decision (1 min)** — one thing you built and why you built it that way
4. **What you'd change (1 min)** — one honest answer. Something from tonight's UX test is a good choice.

**B (timekeeper):** start a 5-minute timer. Call out "2 minutes," "3 minutes," "4 minutes." Stop A at 5:00, even mid-sentence.

### Step 2: Feedback for A (3 mins)

B gives two notes:
1. One thing that worked
2. Where time ran over, or what was unclear

### Step 3: Switch (8 mins)

Repeat Steps 1–2 with **B presenting** and **A keeping time**.

### Step 4: Write down your plan (2 mins)

Each person writes down:
- Which page you'll show for the responsive pattern
- Your one technical decision, in one sentence
- Your one "what I'd change"

**Groups of 3:** shorten feedback to 1 minute each.

---

## Part 5 — Exit Ticket (Main room, 10 mins)

Submit:
1. Your **live URL**
2. Your **GitHub repo link** (verify it's the latest push)
3. Your self-assessed rubric rating for each category, and your remaining "must fix" items — or "none"

If anything is still in "must fix," that's your plan for Wednesday. Office hours are available — use them before Thursday, not after.

---

## Before Thursday

- [ ] Every "must fix" item done — every rubric category at Meets or better
- [ ] Every item in your peer review issue checked off or answered
- [ ] Lighthouse accessibility ≥ 90
- [ ] No horizontal scroll at 375px
- [ ] Live URL works on your phone
- [ ] Final version pushed to GitHub and redeployed
- [ ] Presentation points written down: responsive page, technical decision, what you'd change

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| UX test | Tasks tell the tester where to click, or author helped during the test | 3 goal-based tasks, author stayed silent, hesitations and quotes recorded | Failed tasks and hesitations turned into specific fix-list items |
| Peer review quality | Checklist items skipped or marked pass without checking | All items checked, every rubric category rated with a reason, fails identified with page and element, posted as an issue | Feedback is specific and actionable, and checks the code (mobile-first, ARIA) and not only what's on screen |
| Responsiveness | Horizontal scroll or broken layout on mobile | No overflow, layout changes at breakpoints, tested on a real phone | Intentional mobile-specific adjustments (text size, spacing, interaction) |
| Accessibility | Below 90 Lighthouse score | 90+ Lighthouse, alt text and labels present | 90+, keyboard navigation verified, ARIA attributes correct |
| Plan → Build | Site doesn't match wireframes, UX findings not applied | Wireframe pages built, UX test changes visible in the site | Can explain each change from wireframe to final build and why |
| Lab progress | Same issues at end of class as at start | All "must fix" items addressed, project deployed | Project polished, deployed, and presentation rehearsed — no known issues |
