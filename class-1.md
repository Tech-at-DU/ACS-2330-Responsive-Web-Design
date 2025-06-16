# Class 1: Introduction to Responsive Web Design

## Warmup (10 mins)
- What did you do for spring break? 
- How would you expand the SFPOPOS site? What new features would add? 

## Part 1: Introduction (10 mins)
Responsive web design is an approach to web design that aims to create websites that can adapt to different screen sizes and devices. The concept was introduced by Ethan Marcotte in 2010, who proposed designing websites to be flexible and adaptable to different devices, rather than creating separate mobile and desktop versions of a site. Since then, responsive web design has become more popular as mobile devices have become prevalent, and most modern websites are built using responsive web design techniques. With the increasing popularity of mobile devices and the introduction of new technologies, responsive web design is likely to continue to evolve and adapt to new devices and technologies in the future.

## Part 2: Group Activity (30 minutes)
Your job is to analyze these websites and identify any responsive design techniques that have been used.

- https://www.dropbox.com
- https://dribbble.com/shots/popular/animation
- https://github.com
- https://www.shopify.com/ca
- https://www.magicleap.com/en-us/
- https://www.smashingmagazine.com
- https://slack.com
- https://www.wired.com

**How many of these techniques can you find** in the sites above: 
- https://www.interaction-design.org/literature/article/responsive-design-let-the-device-do-the-work
- https://web.dev/articles/responsive-web-design-basics
- https://www.designitic.com/responsive-web-design-techniques-and-strategies/

**To do this you will need to view the site on a desktop computer and a on a mobile device.** 

Your group will present your findings to the class and discuss the strengths and weaknesses of the website's responsive design.

> **Its best to view a site on a mobile device to really see how it works on mobile devices!** If you don't have a mobile device you can simulate a mobile browsing experience in Chrome or Safari using the Responsive mode. 

- Compare the sites above on both desktop and mobile, side by side! 
- Look for the same elements, like menus, and content boxes, on both desktop and mobile. Ask yourself how these have changed between the two views. Is anything missing on one view or the other? 
- Takes notes, sketch the changes in layout with a simple wireframe.

Do these things! This is important for studying and understanding how these sites are working on desktop and mobile!

Can you find these things: 
- Text changes size
- Number of columns changes
- Flexible boxes
- Elements are removed or moved
- Change from horizontal to vertical layout
- Elements are removed (possibly moved to another area)

## Approaches to responsive design
Responsive design is a design approach that aims to create websites that can adapt to different screen sizes and devices. The principles of responsive design involve using flexible layouts, fluid images, and media queries to ensure that the website looks good and functions well on any device.

1. **Flexible Layouts**: A flexible layout means that the design is not fixed to a specific width or height. Instead, the layout can change and adjust to the available space on the device. This is typically achieved by using relative units like percentages instead of absolute units like pixels for widths and heights. Often you will use layout properties like Flex and Grid with special units like fr (fraction.)
2. **Fluid Images**: Images are an essential part of any website, and they need to be flexible too. A fluid image can adjust its size based on the available space without losing its aspect ratio. This is typically achieved by using the max-width property in CSS.
3. **Media Queries**: Media queries are CSS rules that allow designers to target specific devices based on their screen size or other properties. By using media queries, designers can create different stylesheets that apply to different devices. For example, a designer might create a separate stylesheet for small screens like smartphones, which contains styles that are optimized for that screen size.
4. **Responsive Units**: Responsive units are units of measurement that adjust based on the screen size or device. Two commonly used responsive units are em and rem. Em is a relative unit based on the font size of the parent element, while rem is a relative unit based on the font size of the root element (typically the HTML element). By using responsive units, designers can create flexible layouts that adjust based on the user's device.

Overall, the principles of responsive design aim to create a website that provides a great user experience regardless of the user's device. By using flexible layouts, fluid images, media queries, and responsive units, designers can create websites that are optimized for different screen sizes and devices.

## Wire Framing
Before writing the code to build your websites and make them responsive it is a good idea to have a visual idea of what you are going build!

The subject for this assignment will be the React Fundamentals tutorial. 

Your goal is to draw two wire frames one for the desktop version and one for a mobile version. 

Follow this guide on wire framing: https://careerfoundry.com/en/blog/ux-design/how-to-create-your-first-wireframe/

Wire framing a web site involves creating a visual representation of the website's layout and structure. This representation is called a wireframe, and it's essential to creating a functional and user-friendly website. Here are some steps to help you wireframe a website:

1. **Identify the website's purpose**: Before you start wireframing, identify the website's purpose and goals. This will help you determine the content and features that should be included in the wireframe.
2. **Determine the website's structure**: The structure of the website includes the pages and sections that make up the website. Start by creating a list of the pages you want to include on your website, and then organize them into a logical structure.
3. **Sketch out the wireframe**: Once you have determined the website's structure, sketch out the wireframe on paper or using a digital tool. You can use a simple pen and paper, or use online wireframing tools like Figma, Adobe XD, or Sketch. A wireframe should include the page layout, including the placement of content, images, and navigation elements.
4. **Keep it simple**: Keep the wireframe simple and avoid getting bogged down in design details at this stage. The purpose of the wireframe is to establish the website's layout and structure, not to create a final design.
  - **Draft**, don't draw.
  - **Sketch**, don't illustrate
5. **Test and refine**: Once you have created a wireframe, test it with users or stakeholders to get feedback. Use this feedback to refine the wireframe until you have a final version that meets the website's goals and user needs.

By following these steps, you can create a clear and effective wireframe for your website. Remember that wireframing is an iterative process, so be prepared to revise and refine your wireframe as needed.

Tips and guidelines to help you draw a wireframe:

1. **Start with a clear goal**: Before starting, establish a clear goal and purpose for your wireframe. What do you want to achieve with it? What are the most important elements you need to include? These should be something like: 
  - Shows the most relavant and important information first. 
  - Navigation, and other options are clearly labeled and easy to find, and are understandable at a glance.
  - Some information may have to move on the mobile version, and may not be immediately visible. Ask your self how this affects the a vistors experience using the site? 
2. **Keep it simple**: Wireframes are not meant to be detailed designs but rather a rough sketch of the website's structure and layout. Keep it simple and focus on the overall layout and functionality of the site.
3. **Use basic shapes**: Use simple shapes, such as rectangles, circles, and lines, to represent the different elements of the website, including text, images, and buttons.
4. **Consider content hierarchy**: Pay attention to the order and placement of the content on the page. Make sure that the most important content is easily visible and accessible to the user.
5. **Use a grid system**: A grid system helps you create a consistent and organized layout. Use a grid system to align the different elements of the page.
6. **Label your wireframe**: Make sure to label your wireframe and provide a clear explanation of what each element represents. This will make it easier for others to understand your wireframe.
7. **Focus on functionality**: The wireframe should focus on the functionality of the website rather than the visual design. Don't worry about colors, fonts, or images at this stage.
8. **Get feedback**: Once you have created your wireframe, get feedback from other team members or users to see if it meets the website's goals and user needs.

**Tools**: Use any of these tools to create and share your wire frames. 
- https://balsamiq.com
- https://www.figma.com
- https://miro.com
- https://www.invisionapp.com

## In Class Challenge (60 mins)
Using one of the tools above start mocking up the SFPOPOS Site. 



## Homework challenge
You are going to create wireframes for the SFPOPOS site. Before drawing any boxes you need to create an outline and some user stories. 

**Why create user stories?** If you don't ask and answer questions about how the site will be used the design will be flawed. 

**Why create an outline?** Without a catalog of content its very likely you will leave something out. 

Step 1. Write three user stories for the the site. 

Step 2. Make an outline. Before drawing anything you need to create an outline that lists all of the content on the site. An outline is a list with a hierarchy. Show the content as a hierarchy. Your outline should express which which section owns which content elements on which page. Something like. 

```
- SFPOPOS
  - Home
    - Header
      - Page Title: SFPOPOS
      - Sub title: San Francisco Privately Owned Public Open Spaces
    - Nav
      - NavLink: Home
      - NavLink: About
    ...
```

Step 3. Wire frame the React Fundamentals Tutorial (the SF Public Open Spaces Web site.) **You will draw wire frames for the desktop version and a mobile version.**

The your wireframes can describe the tutorial project as it was presented or describe changes that you want to make, it's up to you. Your wire frames don't have to look like the original tutorial. 

The mobile version of the website doesn't exist yet. What this looks like is up to you. **Keep in mind that the mobile site should include all of the elements from the desktop site.** You can rearrange these elements in any way that makes sense. Think about it from a users perspective, what would make the most sense and work best when browsing on a phone? Consult your user stories. 

You can do your work on paper, or in an application like Figma, Adobe XD, or Sketch. You can also draw your wire frames on paper. If you choose to use paper, you must draw draw neatly and not skimp on dectails!

Your wireframes will include the following: 
An outline: 
- Your outline should include everything
- Your outline should describe everything clearly
- Your outline should express the hierarchy 
Wire frame images: 
- Wire frames include all pages 
- Wire frames include a mobile and desktop image for each page
- Wire frames include all elements from the outline
- Includes all elements in both desktop and mobile 
- All elements are clealy labeled 
Stretch goal:
- Identify areas where you can use the repsonsive design ideas in your wire frames. This might things like: 
  - fluid layout
  - flexible images 
  - scaling typography

### Assess your work

| Category | Does not meet expectations | Meets Expectations | Exceeds expectations |
|:--------:|:--------------------------:|:------------------:|:--------------------:|
| Content | Missing content or content can't be identified | Has all content | All content is clearly labeled |
| Elements | Pages are missing elements or elements can't be identified | Each page has all elements | All elements on all pages are clearly idenitifable |
| Desktop and Mobile | Wire frames do not include a desktop or mobile | Includes both desktop and mobile | Desktop and mobile designs are clearly identifiable and make sense |
| Quality | Drawings are poor quality, sloppy, or hard to read, or contain extraneous details | drawings are clear and concise | well presented and the project is clearly identifiable | 
| User stories | Has less than three user stories, or the user stories do not show clear who, what, and why. | User stories are well written | User stories provide actionable direction for software development team |
| Outline | Outline nonexistent or missing elements | Outline contains everything found in the site, is clearly labeled, and shows hierarchy | This outline includes details describing interaction and functionality |
