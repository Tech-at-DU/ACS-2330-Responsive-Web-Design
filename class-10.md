# Class 10: UX Testing

Before writing a line of code for Project 2, you're going to test your wireframes with real users. This is standard industry practice — catching navigation problems and layout confusion at the wireframe stage costs nothing. Catching them after you've built the site costs significant time.

## Objectives

- Introduce Project 2
- Conduct a UX test of your Project 2 wireframes
- Document findings and apply them to improve your wireframes
- Test specifically for mobile usability

---

## Project 2 Introduction

Your second project is a fully responsive website built with Tailwind CSS. It can be an existing project you've built in a previous course, or something new. See [project-2.md](./project-2.md) for full requirements and rubric.

**By this class you should have:**
- Chosen your project
- Created wireframes (mobile + desktop for each page)
- Annotated wireframes with responsive change notation from class-1

If your wireframes aren't finished, finish them now — you need them for the UX test.

---

## Why Test Wireframes?

You are not a typical user of your own site. You know where everything is, what every button does, and how the navigation works. You've been staring at it for hours.

Your users don't have that context. They see the site fresh. UX testing gives you access to that fresh perspective before you've committed to an implementation.

**Testing wireframes specifically:**
- Users can test a paper sketch or Figma prototype — no code required
- When a user gets confused, you can ask "what did you expect to happen?" without wasting a week of development
- Mobile wireframe testing reveals layout and navigation problems that are invisible on a desktop screen

---

## What to Test

This is a responsive design course. Focus your test on **mobile usability**.

Show testers your **mobile wireframe** first. Tasks should involve navigating the site, finding information, and completing actions — the things users actually do.

Example tasks (adapt to your project):
- "Find [specific content item] and get more information about it"
- "Navigate from the home page to [another page] and back"
- "Find the contact information / sign up for [something]"
- "You want to [accomplish a goal] — show me how you'd do that"

Tasks should be goal-oriented, not instructional. "Click the hamburger menu" is an instruction. "Find the about page" is a task.

---

## Running the Test

### Before: Prepare

- Write 3–5 tasks appropriate for your project
- Have your wireframes ready to show (phone-sized on screen, or printed and held)
- Have a way to take notes

Opening script: *"I'm going to show you a prototype of a website I'm building. I want you to try some tasks. Please think out loud — say whatever comes to mind as you go. There are no wrong answers. I'm testing the design, not you."*

### During: Observe

- Give one task at a time
- **Don't help** — if they get stuck, ask "what would you expect to happen here?" not "here's what to do"
- Note what they **try first** — that tells you where your mental model differs from theirs
- Note where they **hesitate or get confused**
- Write down exact words when possible

**Mobile-specific things to watch:**
- Can they find the navigation on mobile? Do they look for a hamburger?
- Do they scroll naturally, or do they seem lost about where content is?
- Do touch targets (buttons, links) look tappable? Do they try to tap things that aren't interactive?
- Is the content hierarchy clear on a phone-sized view? Do they find key information?

### After: Collect Feedback

Ask 2–3 open questions after tasks are done:
- "What was the hardest part?"
- "What would you change if you could?"
- "Was there anything that surprised you?"

---

## Documenting Findings

For each task, record:

| Task | Completed? | Where they hesitated | What they said |
|------|-----------|---------------------|----------------|
| Find X | Yes / No / Partially | "Looked for nav in bottom bar first" | "I expected a back button here" |

After all testers: identify patterns. If 3 out of 4 people struggled with the same thing, that's a problem worth fixing. One person's confusion might be noise.

Summarize your findings:
- What worked — users completed tasks without help
- What confused users — hesitation, wrong path, gave up
- What to change — specific wireframe updates based on findings

---

## Apply Findings to Wireframes

Pick the top 2–3 issues from your test and update your wireframes. Document what you changed and why.

This updated wireframe is what you'll implement in code. The UX test just saved you from building the wrong thing.

---

## In-Class Activity

Pair up with another student. Take turns:
- One person is the **test provider** — shows wireframes, gives tasks, takes notes
- One person is the **tester** — attempts tasks, thinks out loud

Each person runs the test twice (you test your partner's project, they test yours). 20 minutes per test.

After both tests: spend 10 minutes updating your wireframes based on what you observed.

---

## Submit

Submit to Gradescope:
1. Your wireframes (before and after if you made changes)
2. Notes from your UX test — tasks, what you observed, exact quotes where possible
3. Summary: what you learned and what you changed in response

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Tasks | Fewer than 3 tasks, or tasks are instructions not goals | 3–5 goal-oriented tasks appropriate for the project | Tasks are specific, realistic, and test mobile navigation |
| Observation notes | Vague or missing | Notes for each task — what user tried, where they hesitated | Exact quotes captured, mobile-specific observations noted |
| Findings summary | No summary or just "it went fine" | Clear what worked and what confused users | Patterns identified across multiple testers |
| Wireframe updates | No changes made | At least 2 issues addressed in updated wireframes | Changes are traceable to specific test observations |
