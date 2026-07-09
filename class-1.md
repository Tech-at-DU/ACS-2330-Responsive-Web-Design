# Class 1: Introduction to Responsive Web Design

## Warmup (10 mins)

Find your SFPOPOS project and start it. View it in two places:

1. **Desktop browser** — view it normally at full width
2. **Your phone** — open the local URL on your phone (same wifi network required)

Compare the two. Make a list of specific problems you find on mobile: what breaks, what's too small to tap, what's hard to read, what's cut off. You'll be solving these over the next several weeks.

## Part 1: Introduction (10 mins)
Responsive web design is an approach to web design that aims to create websites that can adapt to different screen sizes and devices. The concept was introduced by Ethan Marcotte in 2010, who proposed designing websites to be flexible and adaptable to different devices, rather than creating separate mobile and desktop versions of a site. Since then, responsive web design has become more popular as mobile devices have become prevalent, and most modern websites are built using responsive web design techniques.

**Mobile traffic now exceeds desktop globally.** This course takes a **mobile-first** approach: we design and code for mobile screens first, then scale up to larger screens. This is the industry standard — and it's how Tailwind CSS (which we'll use in the second half of this course) works out of the box. Get used to thinking small first.

## Part 2: Group Activity (30 minutes)

Here are the responsive techniques you'll be hunting for. Learn these — they're the vocabulary for the rest of the course:

| Technique | What to look for |
|-----------|-----------------|
| **Column changes** | Grid goes from 3 columns on desktop to 1 on mobile |
| **Stack to row** | Elements stacked vertically on mobile, side-by-side on desktop |
| **Nav collapse** | Full nav bar on desktop becomes hamburger or bottom bar on mobile |
| **Elements hidden/shown** | Something visible on desktop disappears on mobile, or vice versa |
| **Fluid images** | Images resize with the container instead of clipping or overflowing |
| **Text scaling** | Font sizes change across screen sizes |
| **Touch-sized targets** | Buttons and links are large enough to tap on mobile |

Now find these techniques in real sites. Each group takes one site, views it on both desktop and mobile (use browser dev tools to simulate mobile), and reports back.

**Sites:**
- https://github.com
- https://www.shopify.com
- https://www.smashingmagazine.com
- https://slack.com
- https://www.wired.com
- https://www.dropbox.com
- https://dribbble.com

**For your site, answer:**
- Which techniques from the table above did you find? Give a specific example of each.
- What works well on mobile? What doesn't?
- Sketch the mobile vs desktop layout difference for one page (30 seconds, boxes only).

Each group presents findings. Reference the technique names from the table above — you'll use these terms all semester.

## The four tools of responsive design

These are the CSS tools you'll use throughout this course. You don't need to master them today — just know what each one does. You'll build with all four over the next several weeks.

| Tool | What it does | When you'll use it |
|------|-------------|-------------------|
| **Media queries** | Apply different CSS at different screen widths | Classes 3–4 |
| **Flexbox** | Arrange elements in a row or column, control spacing | Classes 4–8 |
| **CSS Grid** | Arrange elements in rows and columns simultaneously | Class 5 |
| **Responsive units** | Size elements relative to screen or parent (`%`, `vw`, `rem`, `fr`) | Classes 3–4 |

Your wireframes from the homework will map directly to these tools. Every annotation you write — "1 col → 3 col", "stacked → side by side" — has a corresponding CSS property. Class 2 makes that mapping explicit.

## Wire Framing
Before writing any code, plan what you're building. As a developer, wireframes serve one purpose: **give you a layout spec to implement**. You're not designing — you're planning your code. Wireframes answer questions like: What moves? What stacks? What disappears? What changes size?

The subject for this assignment will be the SFPOPOS site you built in the previous course. You already built the desktop version. Now you're planning the mobile version.

Your goal is to draw two wireframes: one for the desktop version (already exists — document what's there) and one for a mobile version (you design this).

Follow this guide on wire framing: https://careerfoundry.com/en/blog/ux-design/how-to-create-your-first-wireframe/

Wire framing a web site involves creating a visual representation of the website's layout and structure. Here are some steps:

1. **Identify the website's purpose**: Before you start wireframing, identify the website's purpose and goals. This will help you determine the content and features that should be included in the wireframe.
2. **Determine the website's structure**: The structure of the website includes the pages and sections that make up the website. Start by creating a list of the pages you want to include on your website, and then organize them into a logical structure.
3. **Sketch out the wireframe**: Once you have determined the website's structure, sketch out the wireframe on paper or using a digital tool. You can use a simple pen and paper, or use online wireframing tools like Figma, Adobe XD, or Sketch. A wireframe should include the page layout, including the placement of content, images, and navigation elements.
4. **Keep it simple**: Keep the wireframe simple and avoid getting bogged down in design details at this stage. The purpose of the wireframe is to establish the website's layout and structure, not to create a final design.
    - **Draft**, don't draw.
    - **Sketch**, don't illustrate
5. **Test and refine**: Once you have created a wireframe, test it with users or stakeholders to get feedback. Use this feedback to refine the wireframe until you have a final version that meets the website's goals and user needs.

By following these steps, you can create a clear and effective wireframe for your website. Remember that wireframing is an iterative process, so be prepared to revise and refine your wireframe as needed.

Developer-specific wireframing tips:

1. **Start with mobile** — draw the phone layout first. What fits? What doesn't? What has to move or collapse?
2. **Label every element** — you'll be writing CSS class names for these. Vague boxes become vague code. Match the labels from mobile to desktop to make it clear what moves and things change between layouts. 
3. **Mark what changes between sizes** — annotate the wireframe: "this becomes 2 columns on desktop", "this nav collapses to hamburger on mobile."
4. **Keep it simple** — rectangles, lines, and text labels. No color, no fonts, no images. You're writing a spec, not doing design.
5. **Focus on layout and order** — think about which elements appear first on mobile (top of page = most important on a phone).
6. **Note interactions** — if something opens, closes, or changes state, write it down. "Tap hamburger → menu slides in from left."

**Tools**: Use any of these tools to create and share your wire frames. 
- https://balsamiq.com
- https://www.figma.com
- https://miro.com
- https://www.invisionapp.com

## In Class Challenge (60 mins)

Open Figma (or paper) and wireframe two pages of SFPOPOS — mobile version only.

**By end of class you must have:**
- Mobile wireframe for the **Home page** (the spaces list)
- Mobile wireframe for the **Detail page** (one space's detail view)

Use the annotation notation from the wireframing tips: mark column counts, note what the nav does on mobile, mark touch targets. Labels should match the CSS class names already in the project.

Don't start the desktop versions yet — mobile first. The desktop wireframes are homework.

If you finish early: start the About page mobile wireframe, or add annotations to what you have.

## Homework challenge
Plan the responsive version of your SFPOPOS site. This is a planning exercise — you're producing a spec you will implement in code over the next few weeks.

**Step 1. Audit your SFPOPOS site.** Open it on your phone. List every problem: content cut off, text too small, buttons hard to tap, nav unusable, layout broken. This list is your problem statement.

**Step 2. Make a content outline.** List every element on every page. This becomes your checklist — nothing should disappear on mobile that exists on desktop.

```
- SFPOPOS
  - Home
    - Header
      - Page Title: SFPOPOS
      - Subtitle: San Francisco Privately Owned Public Open Spaces
    - Nav
      - NavLink: Home
      - NavLink: About
      - [mobile: collapses to hamburger menu]
    ...
```

**Step 3. Draw wireframes — mobile first.** For each page, draw mobile layout first, then desktop. Annotate every responsive change using this notation:

```
[mobile]   → [desktop]
1 col      → 3 col
stacked    → side by side  
hamburger  → full nav
hidden     → visible
full width → 50% width
```

For each page capture these responsive features:

| Feature | Questions to answer |
|---------|-------------------|
| **Layout** | How many columns on mobile? On desktop? Where do things stack vs sit side by side? |
| **Navigation** | Does the nav collapse? What replaces it on mobile — hamburger, bottom bar, hidden? |
| **Images** | Do images fill full width on mobile? Shrink on desktop? |
| **Content order** | Does anything reorder between mobile and desktop? What appears first on mobile? |
| **Hidden/shown** | Is anything visible on desktop that hides on mobile, or vice versa? |
| **Text** | Does any text change size noticeably between sizes? |
| **Touch targets** | Are buttons and links large enough to tap on mobile (mark anything that needs to be bigger)? |

Use paper, Figma, or any tool. If using paper, draw clearly — this is a spec, not a sketch.

Your wireframes will include:
- Content outline with hierarchy
- Mobile wireframe for each page
- Desktop wireframe for each page
- Annotations on every responsive change using the notation above
- All elements labeled with names you'd use as CSS class names

### Assess your work

| Category | Does not meet expectations | Meets Expectations | Exceeds expectations |
|:--------:|:--------------------------:|:------------------:|:--------------------:|
| Audit | No audit or audit misses obvious mobile problems | Lists concrete problems found on mobile | Problems are specific and mapped to elements (e.g. "nav has no mobile layout", "cards overflow at 375px") |
| Content outline | Missing elements or hierarchy unclear | All pages and elements listed with clear hierarchy | Element names match what you'd use as CSS class names |
| Mobile wireframes | Missing or incomplete mobile layouts | Mobile layout for each page, all elements present | Annotated — notes what changes, collapses, or reorders vs desktop |
| Desktop wireframes | Missing or just a screenshot of the existing site | Desktop layout documented for each page | Shows intentional differences from mobile (column counts, nav layout, spacing) |
| Annotations | No annotations | Marks what changes between mobile and desktop | Includes interaction notes (hamburger opens menu, grid changes columns, etc.) |
