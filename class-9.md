# Introduction to Media Queries with Tailwind CSS

In the previous classes, you used vanilla CSS to create a responsive website. In this lesson, you will use Tailwind to create a responsive website. 

## Lecture and Demonstration:

For this assignment, you can use either a site you have previously created, which you will update to make it responsive, or you can choose an existing site that you will recreate as a responsive site. 

In both cases, you will use Tailwind CSS. 

## What is Tailwind

Tailwind is a very popular CSS framework. Read about it here: https://tailwindcss.com

## Setup Tailwind

To use Tailwind you need to install and set up its packages. How you do this depends on the type of project you are working on. 

**HTML/CSS/JS** 

Initialize a new npm project with:

```
npm init -y
```

Then follow the guide here: https://tailwindcss.com/docs/installation

**React**

Follow the instructions here: https://tailwindcss.com/docs/guides/create-react-app

**Note!** If you started with an existing project you should remove the existing styles because these may interfere with TailwindCSS styles! If you want to keep the existing styles you should recreate them with TailWind classes! 

## Intro to Tailwind

Tailwind works via utility classes that you apply to elements in your work. What does that mean? Imagine you have: 

```HTML
<p class="text-3xl font-bold underline">Hello World</p>
```

The classes added above would make the text appear as 3xl, bold, and underlined. 

What's `text-3xl`? Take a look here: https://tailwindcss.com/docs/font-size#setting-the-font-size 

`text-3xl` makes the text `1.953rem`

`font-bold` and `underline` I'll assume are self-explanatory. 

These classes all provide utility. You will be combining these utility classes to create the styles you envision. 

This is different from defining a single class that has all of the features. Something like:

```HTML
<p class="important-text">Hello World</p>
<style>
  .important-text {
    font-size: 2rem;
    font-weight: bold;
    text-decoration: underline;
  }
</style>
```

## Tailwind classes 

Tailwind has a lot of classes. Too many to describe. 

1. **Layout** - Classes that help with structuring and positioning elements, such as container, grid, flex, float, clear, and display classes.
2. **Typography** - Classes that help with styling text and fonts, such as font, text, leading, tracking, and whitespace classes.
3. **Backgrounds** - Classes that help with setting background colors and images, such as bg, bg-opacity, bg-gradient-to, and bg-blur classes.
4. **Borders** - Classes that help with styling borders, such as border, border-opacity, border-solid, border-dashed, and border-double classes.
5. **Tables** - Classes that help with styling tables, such as a table, table-auto, table-fixed, and table-caption classes.
6. **Forms** - Classes that help with styling form elements, such as form, input, select, checkbox, radio, label, and placeholder classes.
7. **Effects** - Classes that help with adding effects, such as shadow, opacity, transition, transform, and scale classes.
8. **Interactivity** - Classes that help with adding interactivity, such as hover, focus, active, and group-hover classes.
9. **SVG** - Classes that help with styling SVG elements, such as fill-current and stroke-current classes.
10. **Accessibility** - Classes that help with making content more accessible, such as sr-only, not-sr-only, focus-within, and focus-visible classes.

Note that this list is not exhaustive and there may be additional categories or classes within each category.

When using TailwindCSS when you're not sure what the class name is search the TailwindCSS site, the documentation is very good. 

https://tailwindcss.com

## Tailwind responsive classes 

Tailwind provides the following responsive class names that implement media queries with the following breakpoints. 

| Breakpoint prefix | Minimum width | CSS |
|:-----------------:|:-------------:|:---:|
| sm | 640px | @media (min-width: 640px) { ... } |
| md | 768px | @media (min-width: 768px) { ... } |
| lg | 1024px | @media (min-width: 1024px) { ... } |
| xl | 1280px | @media (min-width: 1280px) { ... } |
| 2xl | 1536px | @media (min-width: 1536px) { ... } |

Use the responsive classes like this: 

```HTML
<!-- Width of 16 by default, 32 on medium screens, and 48 on large screens -->
<img class="w-16 md:w-32 lg:w-48" src="...">
```

The responsive class is applied as a prefix to another class with a colon. The docs say: 

> This works for every utility class in the framework, which means you can change literally anything at a given breakpoint — even things like letter spacing or cursor styles.

https://tailwindcss.com/docs/responsive-design

## Tailwind containers

The container class sets the max-width of an element to match the min-width of the current breakpoint. This is useful if you’d prefer to design for a fixed set of screen sizes instead of trying to accommodate a fully fluid viewport.

Note that, unlike containers you might have used in other frameworks, Tailwind’s container does not center itself automatically and does not have any built-in horizontal padding.

To center a container, use the mx-auto utility:

```HTML
<div class="container mx-auto">
  <!-- ... -->
</div>
```

It's a good idea to use this for the top-level layout element, for example, headers, footers, and grid containers. 

https://tailwindcss.com/docs/container

You can use the following "formula" to create a container that extends to the edges of the screen while "corraling" the content to the width of the container element. 

To make this work these elements must not be inside of another container or have a width applied. You will be defining a container with a width here. 

```HTML
<footer className="Footer text-slate-50 bg-slate-900">
  <div className='container max-w-screen mx-auto items-center flex justify-between p-4'>
    <POPOSCount />
    <span>© {year}</span>
  </div>
</footer>
```

The footer element extends to the width of the window. The `div.container` uses the container class to corral the content in the width of the container. This wouldn't work as expected if `footer` also had the class `container`!

The other styles arrange the POPOSCount and Copyright to eh left and right of the container. 

Notice, I set the background color and text colors on the parent element and everything inside the footer inherits these, which is easier than setting the colors on elements individually. 

## TailWind Grid Responsive

Use Tailwind's grid to arrange elements in a grid. 

- grid - declare an element as a grid
- gap-# - set the gap in Tailwind units
- grid-cols-# - set the number of cols

Use the responsive prefixes to set change grid classes for each of the breakpoints. For example: 

```HTML
<div className="POPOSList grid xl:grid-cols-4 lg:grid-cols-3 md:grid-cols-2 sm:grid-cols-1 container max-w-screen grid gap-4 mx-auto items-center p-4">
  {spaces}
</div>
```

- xl:grid-cols-4 - 4 columns at 1280px 
- lg:grid-cols-3 - 3 columns at 1024px 
- md:grid-cols-2 - 2 columns at 768px
- sm:grid-cols-1 - 1 column at 640px

## Tailwind flexible images

You may need to get images to resize based on the available space. After setting up your grid the images may not fill the "grid cells". Get images to expand with: 

```
w-full
```

## NavLink and Tailwind

React Router uses a function in the class of a NavLink to set a class when the link is active or inactive. With Tailwind you will need to have some Tailwind classes that apply to the element all of the time, and some classes that appear when the link is active. To do this use a function for the class that returns a string of class names that apply all of the time. Concatenate that class with the ternary operator to add the classes that should be added when the element is active, and the classes that appear when the element is active. 

```JS
<NavLink 
  className={({ isActive }) => 'block p-2 ' + (isActive ? "text-slate-900 font-bold" : "font-thin")}
  to="/">Location</NavLink>
```

In the example above, the link should have the style `block p-2` all of the time. Notice the space after `p-2` you must have this to create a space between this and the next class name! 

The ternary that follows must appear in parenthesis! The string returned from this ternary must be calculated first, before concatenating with the previous string! 

If the link is active the classes: `text-slate-900 font-bold` are added, if not active the class: `font-thin` is added. 

- Active -> 'block p-2 text-slate-900 font-bold'
- Not Active -> 'block p-2 font-thin'

## Tailwind Sticky footer

A sticky footer is a footer that sticks to the bottom of the screen _when the page height is smaller than the content_. Then the page is larger than the content the footer will stay below the content. 

Use this formula with Tailwind to create a sticky footer. 

The HTML structure must have a parent element with two children. The first child will contain the content of your page except for the footer! The second child will be the footer. Something like this: 

```HTML
<main>
  <div class="content"></div>
  <footer></footer>
</main>
```

The first div would have your header and content. In the SFPOPOS tutorial it might look like this: 

```HTML
<main>
  <div className="content">
    <Title />
      <Outlet />
    </div>
  <Footer />
</main>
```

use the classes `flex flex-col h-screen justify-between`. For example: 

```HTML
<main class="flex flex-col h-screen justify-between">
  <div class="content"></div>
  <footer></footer>
</main>
```

## Responsive Tailwind Examples

Try these examples and apply them to your work. 

### 1. Breakpoints in practice

```html
<p class="text-sm md:text-lg lg:text-2xl">
  Responsive text: small on mobile, bigger on tablets, largest on desktops.
</p>
```

### 2. Stack to row

```html
<div class="flex flex-col md:flex-row gap-4">
  <div class="bg-blue-300 p-4">Box 1</div>
  <div class="bg-blue-400 p-4">Box 2</div>
  <div class="bg-blue-500 p-4">Box 3</div>
</div>
```

### 3. Hide and show

```html
<div>
  <p class="block md:hidden text-red-600">Shown only on mobile</p>
  <p class="hidden md:block text-green-600">Shown only on desktop</p>
</div>
```

### 4. Responsive Navbar

```html
<nav class="bg-gray-800 text-white p-4 flex flex-col md:flex-row justify-between">
  <div class="font-bold">Logo</div>
  <ul class="flex flex-col md:flex-row gap-2 md:gap-6 mt-2 md:mt-0">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

### 5. Card Grid

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
  <div class="bg-white shadow p-4">Card 1</div>
  <div class="bg-white shadow p-4">Card 2</div>
  <div class="bg-white shadow p-4">Card 3</div>
  <div class="bg-white shadow p-4">Card 4</div>
</div>
```

### 6. Hero Section

```html
<section class="flex flex-col md:flex-row items-center p-8 bg-blue-100">
  <div class="md:w-1/2">
    <h1 class="text-2xl md:text-5xl font-bold">Hero Title</h1>
    <p class="mt-4">This is some hero text that changes size.</p>
    <button class="mt-4 px-4 py-2 bg-blue-600 text-white rounded">Get Started</button>
  </div>
  <div class="md:w-1/2 mt-6 md:mt-0">
    <img src="https://placehold.co/400x300" alt="Hero image" class="rounded-lg shadow">
  </div>
</section>
```

### 7. Responsive Images

```html
<img src="https://placehold.co/600x400"
     alt="Sample"
     class="w-full object-cover h-48 md:h-96 lg:h-[600px] rounded-lg" />
```

### 8. Pricing Table

```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
  <div class="bg-gray-100 p-6 rounded shadow">Basic Plan</div>
  <div class="bg-blue-200 p-6 rounded shadow md:col-span-1 lg:col-span-1">Pro Plan</div>
  <div class="bg-gray-100 p-6 rounded shadow">Enterprise</div>
</div>
```

### 9. Responsive Footer

```html
<footer class="bg-gray-900 text-white p-6 grid grid-cols-1 md:grid-cols-3 gap-6">
  <div>
    <h3 class="font-bold">About</h3>
    <p>Short description.</p>
  </div>
  <div>
    <h3 class="font-bold">Links</h3>
    <ul class="space-y-2">
      <li><a href="#">Home</a></li>
      <li><a href="#">Services</a></li>
    </ul>
  </div>
  <div>
    <h3 class="font-bold">Contact</h3>
    <p>info@example.com</p>
  </div>
</footer>
```

### 10. Typography scaling

```html
<h1 class="text-sm md:text-base lg:text-xl">Scaling Headline</h1>
```

### 11. Responsive spacing

```html
<div class="bg-green-200 p-2 md:p-6 lg:p-12">
  Responsive padding adjusts at breakpoints.
</div>
```

### 12. Responsive backgrounds

```html
<div class="h-40 bg-red-300 md:bg-yellow-300 lg:bg-green-300">
  Background color changes as screen grows.
</div>
```

### 13. Dark mode + responsiveness

```html
<div class="p-6 bg-gray-100 dark:bg-gray-900 md:dark:bg-black">
  Try toggling dark mode in Tailwind config.
</div>
```

### 14. Dashboard Layout

```html
<div class="flex">
  <aside class="hidden md:block w-64 bg-gray-200 p-4">Sidebar</aside>
  <main class="flex-1 p-6">Main content area</main>
</div>
```

### 15. Gallery/Portfolio

```html
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
  <img src="https://placehold.co/200" class="rounded-lg hover:scale-105 transition" />
  <img src="https://placehold.co/200" class="rounded-lg hover:scale-105 transition" />
  <img src="https://placehold.co/200" class="rounded-lg hover:scale-105 transition" />
  <img src="https://placehold.co/200" class="rounded-lg hover:scale-105 transition" />
</div>
```

### 16. Blog Layout

```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
  <main class="md:col-span-2 bg-white p-4 shadow">Blog content</main>
  <aside class="bg-gray-100 p-4 shadow">Sidebar</aside>
</div>
```

## Homework Challenge

Start working on your [final project](./project-2.md). 
