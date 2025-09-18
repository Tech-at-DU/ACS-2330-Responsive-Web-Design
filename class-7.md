# Accessibility Part 2

Modifying an existing site to improve accessibility. 


- Semantic HTML
- What is ARIA 
- What are roles? 
- ARIA states and properties

## Semantic HTML and Web Accessibility

Semantic HTML, which refers to the use of HTML elements that carry meaning and convey the structure and purpose of content, plays a crucial role in web accessibility. Here's how semantic HTML can impact web accessibility:

- Enhances Screen Reader Accessibility: Semantic HTML elements, such as headings, paragraphs, lists, and form inputs, provide meaningful information to screen readers, allowing users to navigate and understand the content more effectively.
- Improves Keyboard Accessibility: Semantic HTML elements are naturally keyboard accessible, meaning they can be easily navigated and interacted with using the keyboard alone. This is important for users who rely on keyboard navigation due to motor disabilities or other reasons.
- Supports Responsive Design: Semantic HTML provides a clear structure and hierarchy to web content, which is crucial for responsive web design. By using semantic elements like `<header>`, `<nav>`, `<main>`, `<aside>`, and `<footer>`, web developers can create a well-structured document that is easily adaptable to different screen sizes and devices.
- Facilitates SEO: Semantic HTML elements help search engines understand the structure and meaning of web content, which can improve search engine optimization (SEO). Properly using semantic elements, such as `<h1>` for headings and `<p>` for paragraphs, can make content more accessible and discoverable for search engines and users alike.
- Provides Context and Clarity: Semantic HTML elements convey the intended purpose and meaning of content, making it more understandable and usable for all users. For example, using `<figure>` and `<figcaption>` elements for images, `<cite>` for citations, and `<blockquote>` for quotes can provide additional context and clarity to the content.
- Enhances Assistive Technology Support: Many assistive technologies, including screen readers, rely on semantic HTML elements to interpret and present web content to users with disabilities. By using semantic HTML, web developers ensure that their content is compatible with a wide range of assistive technologies, improving accessibility for users with disabilities.

In summary, using semantic HTML in web development improves web accessibility by providing meaningful structure, supporting assistive technologies, enhancing keyboard accessibility, facilitating responsive design, improving SEO, and providing clarity and context to web content. It is an essential practice for creating inclusive and accessible web experiences.

**Challenge** Look through your SFPOPOS site and upgrade all of the generic tags with semantic tags to improve accessibility and SEO. 

For example: The nav bar at the top of the page is top level navigation as such it should use the `<nav>` tag. 

```HTML
<!-- Uses the div tag around navigation -->
<div className="Title__nav" role="navigation">
	<NavLink 
		className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
		to="/">List</NavLink>
	<NavLink 
		className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
		to="/about">About</NavLink>
	<RandomSpace />
</div>
```

Becomes: 

```HTML
<!-- Better to use the nav tag here!  -->
<nav className="Title__nav" role="navigation">
	<NavLink 
		className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
		to="/">List</NavLink>
	<NavLink 
		className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
		to="/about">About</NavLink>
	<RandomSpace />
</nav>
```

The header tag around the navbar should use the header tag: 

```HTML
<!-- The header uses the div tag -->
<div className="Title">
	<div>
		<h1>SFPOPOS</h1>
		<small className="Title-Subtitle">San Francisco Privately Owned Public Open Spaces</small>
	</div>
	<nav className="Title__nav" role="navigation">
		<NavLink 
			className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
			to="/">List</NavLink>
		<NavLink 
			className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
			to="/about">About</NavLink>
		<RandomSpace />
	</nav>
</div>
```

Becomes: 

```HTML
<!-- Better to use the header tag! -->
<header className="Title">
	<div>
		<h1>SFPOPOS</h1>
		<small className="Title-Subtitle">San Francisco Privately Owned Public Open Spaces</small>
	</div>
	<nav className="Title__nav" role="navigation">
		<NavLink 
			className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
			to="/">List</NavLink>
		<NavLink 
			className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
			to="/about">About</NavLink>
		<RandomSpace />
	</nav>
</header>
```

Continue through all of your components and repeat the process. 

- `<header>`: Used to define the header or the top section of a web page or a section within a web page. It typically contains branding, logos, navigation menus, and other introductory content.
- `<nav>`: Used to define a navigation section of a web page. It typically contains links to other pages or sections of the website.
- `<main>`: Used to define the main content area of a web page. It should not include headers, footers, or sidebars, and should represent the primary content of the page.
- `<aside>`: Used to define content that is tangentially related to the content around it, such as sidebars, pull quotes, or additional information.
- `<article>`: Used to define a self-contained piece of content that could be distributed and reused independently, such as a news article, blog post, or forum post.
- `<section>`: Used to define a section of content that is thematically related and can be treated as an independent unit, such as a group of related articles, a group of related form elements, or a group of related images.
- `<figure>`: Used to define any content that is referenced from the main content, such as an image, a chart, or a video.
- `<figcaption>`: Used to provide a caption or description for a <figure> element.
- `<footer>`: Used to define the footer or the bottom section of a web page or a section within a web page. It typically contains copyright information, contact details, and other auxiliary content.
- `<blockquote>`: Used to define a block of quoted content, such as a quote from another source or a citation.

Pay close attention to the figure tag. The page is full images that represent real world locations, these are important and relavent content. The figure and figcaption tags can help describe these elements for accessability. 

## ARIA

ARIA (Accessible Rich Internet Applications) attributes are HTML attributes that can be used to improve the accessibility of web content for individuals with disabilities. These attributes can be added to HTML tags to provide additional information about the function, purpose, or state of an element, such as a button, form, or widget.

ARIA attributes include **roles**, which define the type or category of an element, such as "button", "listbox", or "menu", and states, which describe the current condition or value of an element, such as "selected", "disabled", or "expanded". ARIA attributes also include properties, which provide additional information about an element, such as "aria-label" to provide a label for an element or "aria-describedby" to provide a description of an element.

Using ARIA attributes can improve the accessibility of web content by making it easier for individuals with disabilities to interact with a website. For example, ARIA attributes can help screen readers interpret the purpose and function of different elements on a webpage, allowing users with visual impairments to navigate and interact with the content more easily. By providing this additional information, web developers can ensure that their websites are accessible to a wider range of users, including those with disabilities.

**ARIA examples**

ARIA role for navigation menus: If a website has a navigation menu, it's important to make sure that it is accessible to all users, including those who use screen readers. One way to do this is to use the ARIA role attribute to identify the menu as a navigation landmark. For example, the following code could be used to mark up a navigation menu with the ARIA role of "navigation":

```HTML
<!-- ARIA role attribute marks this as navigation -->
<nav role="navigation">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

By adding the role attribute with a value of "navigation", screen readers will be able to identify the navigation menu as a distinct landmark on the page, making it easier for users to navigate to the content they are looking for.

ARIA attribute for form inputs: Forms are an important part of many websites, but they can be challenging for users with disabilities to complete. ARIA attributes can help make forms more accessible by providing additional information about form inputs. For example, the following code could be used to add a label and description to a text input field:

```HTML
<label for="name">Name:</label>
<input type="text" id="name" aria-describedby="name-description">
<!-- The ARIA attribute above says the input is described by the tag below -->
<span id="name-description">Enter your full name.</span>
```

In this example, the "for" attribute on the label element is used to associate the label with the input field, while the "aria-describedby" attribute on the input element is used to associate it with a description of the input field. Screen readers can then read out the label and description together, making it easier for users to understand the purpose of the input field.

Take a look at the ARIA attributes page over at Mozilla: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA

Look at the list of ARIA roles: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles

**Challenge** Add ARIA attributes to your site. Identify everything that you can that would be improved by adding ARIA roles or other attributes.

React docs also have an ARIA page, you should read this: https://legacy.reactjs.org/docs/accessibility.html

https://www.lullabot.com/articles/what-heck-aria-beginners-guide-aria-accessibility

ARIA attributes come in two categories: roles and states. Roles provide semantic meaning to content. States describe the "state" of an element. The first is easy. The second is pretty broad.

- [ARIA Roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles)
- [ARIA States](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes)

For now focus on roles. As a stretch goal read the states lists and find opportunity for these in your page. 

### Color and contrast 

Contrast is the difference in value between two colors. The value of a color is how dark or light a color would appear if you converted it to gray scale. Red for example is is about 50% gray. Blue is often darker and yellow is often lighter. 

It's the value difference that that makes things stand out and the lack of contrast makes things harder to read.

Contrast has been rated for accessibility. Use this site to check your colors. 

https://webaim.org/resources/contrastchecker/

NOTE! For text font size and weight matter. Smaller fonts, and lighter weight fonts are harder to read and require more contrast! Becuase two colors work at one point size doesn't mean they are legible to everyone at every point size. 

**Challenge** Check the color and contrast on your site. Enter the colors into the [WEBAIM Constrast checker](https://webaim.org/resources/contrastchecker/) and check the score. Adjust the contrast for failing scores. 

## Challenge

Update your responsive site using the accessibility best practices. 

### Accessibility Best Practices

1. **Use semantic HTML** – Headings, lists, buttons, and forms should use proper tags.
2. **Provide text alternatives** – Add meaningful `alt` text for images.
3. **Ensure keyboard accessibility** – All functionality should work without a mouse (e.g., tab navigation).
4. **Maintain color contrast** – Text should have a minimum 4.5:1 contrast ratio against backgrounds.
5. **Don’t rely on color alone** – Use text, icons, or patterns in addition to color cues.
6. **Use clear, descriptive links** – Avoid “click here” or “read more.”
7. **Provide labels and instructions** – Forms must have visible labels or ARIA labels.
8. **Use headings logically** – Structure content in order (`h1`, then `h2`, etc.).
9. **Provide captions/transcripts** – For videos and audio.
10. **Avoid flashing/strobing content** – To prevent seizures.
11. **Make text resizable** – Support zoom without breaking layout.
12. **Test with screen readers and tools** – NVDA, VoiceOver, Lighthouse, WAVE.


