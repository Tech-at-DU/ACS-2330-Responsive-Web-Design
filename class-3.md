# Media Queries

Media queries are a feature of Cascading Style Sheets (CSS) that **allow developers to apply different styles to a web page based on the characteristics of the device or browser** that is being used to view it. 

This allows the layout and design of a web page to be optimized for different screen sizes, resolutions, and device types, such as smartphones, tablets, desktops, and laptops. 

Media queries use a series of conditions and rules to define the styles that should be applied for each device or browser, based on its properties such as viewport width, device orientation, and pixel density. Media queries can help ensure that web pages are accessible and user-friendly across a wide range of devices and platforms.

## Objectives 

- Describe media queries
- Use Media Queries
- Define break points 
- Use break points to create responsive pages

## Media Query syntax

The "@media" CSS syntax is used to **define a set of CSS rules that apply only to specific media types** or media features. 

The syntax starts with "@media" followed by a media query, which specifies the conditions under which the rules should apply. The media query can include various media features such as "screen", "print", "max-width", "min-width", "orientation", and others. Inside the media query, the CSS rules that should apply to the specified media type or feature are defined within curly brackets. For example, the following code applies a blue background color to the body element only when the viewport width is less than or equal to 600 pixels:

```CSS
@media (max-width: 600px) {
  body {
    background-color: blue;
  }
}
```

### What type of media? 

The `@media` rule in CSS can be used to apply different styles based on a variety of media types, including:

1. **all**: This is the default media type and applies to all devices and media.
2. **screen**: This applies to devices with a screen, such as desktop monitors, laptops, tablets, and smartphones.
3. **print**: This applies to printed documents and pages.

That's right media defines "print" as a type. If you were to print your web page you could apply styles specifically for print! 

Let's do an example. Imagine you made an online resume. It's got color and images, it's really fancy. It wouldn't look great in print, the fonts would be too large, the pictures would make everything spill over on to multiple pages, and the background color would make the text hard to read, and use up a recruiters ink cartriges! 

We might fix it like this: 

```CSS
/* imagine all of the fancy styles here */
body {
  background-color: tomato;
  color: beige;
  font-size: 17px;
}

/* After all of that we apply a media query
These styes only apply when the media type 
is print!
NOTE! All of the styles above also apply! 
These overwrite some of the above styles. 
*/
@media print {
  body {
    background-color: white;
    color: black;
    font-size: 10px;
  }
}
```

The `@media` block contains styles that are only applied when the media type and features match. Otherwise the style in the block are not used. 

This means that the `@media` block should be placed _after_ your other styles! In this way these rules will overwrite the rules that came before!

## The W3C CSSWG says:

Looking to the future! The CSS Working Group says this:

> **NOTE:** It is expected that all of the _media types_ will also be deprecated in time, as _appropriate media features_ are defined which capture their important differences.

https://developer.mozilla.org/en-US/docs/Web/CSS/@media

**Who is the CSSWG?** The CSSWG (CSS Working Group) is a group of individuals who are involved in the development and maintenance of the Cascading Style Sheets (CSS) language. The group is part of the World Wide Web Consortium (W3C), which is a community of organizations and individuals working to develop web standards.

What does that mean? Above, the `@media` query defines the media type as `print`. You can also describe media features. Here's an example: 

```CSS
@media screen and (max-width: 480px) {
  /* CSS styles that apply to mobile here! */
  body {
    background-color: fuchsia;
  }
}
```

In this example the media type is screen, and `max-width` is a *feature*. The rules in the block only apply when the media type is screen **and** the width of the screen is 480px or smaller (`max-width: 480px`). 

This rule applies to smaller screens and doesn't apply to larger screens! **The CSSWG is going to remove media types in the future and we will only use media features!**

Here are some commonly used media features in Media Queries Level 5:

1. **width**: This feature applies styles based on the width of the viewport.
2. **height**: This feature applies styles based on the height of the viewport.
3. **orientation**: This feature applies styles based on the orientation of the viewport, either portrait or landscape.
4. **aspect-ratio**: This feature applies styles based on the aspect ratio of the viewport.
5. **color**: This feature applies styles based on the number of colors supported by the device.
6. **monochrome**: This feature applies styles based on the number of monochrome (black and white) colors supported by the device.
7. **prefers-reduced-motion**: This feature applies styles based on the user's preference for reduced motion on the device.
8. **prefers-color-scheme**: This feature applies styles based on the user's preferred color scheme, either light or dark.
9. **hover**: This feature applies styles based on whether the device supports hover interactions.
10. **pointer**: This feature applies styles based on the primary input mechanism of the device, such as coarse for touchscreens or fine for mouse-driven devices.

It's important to note that support for these media features may vary across devices and browsers, so it's always a good idea to test your styles across different platforms to ensure they work as intended.

## What is responsive web design? 

Responsive web design is a design approach that creates websites that look good and function well on all devices and screen sizes. It uses flexible layouts, images, and typography that adapt to the user's screen size and orientation. This ensures that the website content is accessible and easy to read, regardless of the user's device.

In short, responsive sites are sites that respond to the device where they are viewed. 

## How do you make sites responsive? 

Websites are always media screen. The big difference between screens is the features. The most important feature is the width of the screen. 

Compare your phone to the your desktop. I have an iPhone 11 pro. The screen is 5.8" diagonally, screen resolution is 1125 x 2436 pixels but it is 375 x 812 points (actual pixels vs points). 

On iOS, the screen size is measured in points rather than pixels. The iPhone 11 Pro has a screen size of 375 points x 812 points, which is equivalent to 1125 x 2436 pixels at a 3x scale factor (which is the device's native scale factor).

Pixels are the smallest unit of measurement on a digital screen, while points are a relative unit of measurement *used in digital design*. Pixels are fixed in number, while points can vary depending on the device's pixel density. Points are used by designers to ensure consistent sizing across different devices.

The width of the iPhone 11 Pro in CSS pixels would be 375px. This is based on the device's screen size of 375 points, which, at the device's native scale factor of x3, translates to 1125 physical pixels.

I'm writing this on my MacBook Pro which has a screen size of: 2880 × 1800. Which is a lot wider than the iPhone 11. The Desktop is wider in CSS pixels and all of the pixels are larger. The macbook has twice the number of pixels but the pixels on the phone are smaller.

Points are always 1/72". A point on the iPhone, is the same size as a point on the MacBook, even though the physical pixels are different!

Remember that media query you looked at earlier? 

```CSS
@media screen and (max-width: 480px) {
  /* CSS styles that apply to mobile here! */
  body {
    background-color: fuchsia;
  }
}
```

This applies to the iPhone 11 Pro but doesn't apply to the MacBook Pro! The max-width of 480px uses the CSS pixels/points and sees that the iPhone 11 is smaller at 375, so the rules inside this media query apply to that device. 

This is the idea of break points!

## What's a break point?

Breakpoints are specific screen widths at which the layout of a web page changes to accommodate different device sizes. They are commonly used in responsive web design to ensure that a website looks good and functions properly on devices of different sizes, such as smartphones, tablets, laptops, and desktops. 

Breakpoints are defined using media queries, which specify the maximum or minimum screen width at which the layout should change. For example, a breakpoint may be set at 768 pixels, which is the screen width at which a tablet switches from a portrait to landscape orientation. At this breakpoint, the layout may change to accommodate the wider screen, such as by rearranging or resizing content, adjusting font sizes, or hiding or revealing certain elements. Breakpoints are an important aspect of creating responsive web designs that are optimized for a variety of devices and screen sizes.

## Mobile break points

Break points can be as detailed as you care to make them. For this challenge assume you need only support desktop and mobile devices.

```CSS
@media screen and (max-width: 480px) {
  /* CSS styles that apply to mobile here! */
  body {
    background-color: fuchsia;
  }
}
```

You will write all of the styles that apply to mobile devices here. You may be overwriting some styles that exist _above_ this rule. **For that reason be sure to place this rule at the bottom of any CSS file!**

Here are common breakpoints used in responsive web design, based on common screen sizes and device types:

- **320px** - common screen width for small smartphones
- **480px** - common screen width for larger smartphones and small tablets
- **768px** - common screen width for tablets in landscape orientation
- **992px** - common screen width for small laptops and desktops
- **1200px** - common screen width for larger laptops and desktops

These are just examples, and the specific breakpoints used may vary depending on the design of the website and the target audience. 

In general, breakpoints should be chosen based on the most common screen sizes of the devices that the website is likely to be viewed on, with additional breakpoints added as needed to accommodate less common sizes or specific design requirements.

Here are some examples. 

**320px:** This media query would target small smartphones such as the iPhone 4s or Samsung Galaxy S3 Mini.
```css
@media (max-width: 320px) {
  /* CSS rules for screens with a maximum width of 320px */
}
```

**480px:** This media query would target larger smartphones such as the iPhone 6 or Samsung Galaxy S5, as well as small tablets such as the iPad Mini.
```css
@media (max-width: 480px) {
  /* CSS rules for screens with a maximum width of 480px */
}
```

**768px:** This media query would target tablets in landscape orientation such as the iPad Air or Samsung Galaxy Tab.
```css
@media (max-width: 768px) {
  /* CSS rules for screens with a maximum width of 768px */
}
```

**992px:** This media query would target small laptops and desktops such as the MacBook Air or Dell XPS 13.
```css
@media (max-width: 992px) {
  /* CSS rules for screens with a maximum width of 992px */
}
```

**1200px:** This media query would target larger laptops and desktops such as the MacBook Pro or Dell XPS 15.
```css
@media (max-width: 1200px) {
  /* CSS rules for screens with a maximum width of 1200px */
}
```

These are just examples, and you can also use `min-width` instead of `max-width` to define breakpoints for larger screens. Additionally, you can combine media features to create more complex media queries that target specific devices or conditions.

Specific devices that fit each media query may vary depending on their screen resolution and pixel density, as well as the orientation of the device. Additionally, users may resize their browser windows or use other devices with different screen sizes, so it's important to test your website's responsiveness across a range of devices and screen sizes.

## Testing Media Queries and Breakpoints

Start with this: 

```CSS
@media screen and (max-width: 480px) {
  body {
    background: fuchsia;
  }
}
```

This sets the background color to a bright color when the screen is 480px or smaller. You can use this idea to let you know when your media query is in effect.

**In Safari:** 

- Turn on developer mode Safari > Settings > Advanced Check the box: "Show Develop menu in menu bar"
- Develop > Enter Responsive Design Mode

**In Chrome:** 

- Right click, choose inspect
- In the upper left of the inspector click the mobile phone icon. 

## Challenge

Your goal is to realize your wire frames (desktop and mobile) using media queries. 

To do this should add a media query for mobile devices. The existing style should handle the desktop version. **This is called desktop first design.** You designed for the desktop (first) and now you are adding modifications that apply when displayed on mobile. 

The code below applies a style 

```CSS
/* Existing styles up here... */

@media screen and (max-width: 480px) {
  /* These styles are applied when 
  the screen size 480 or smaller */
  .POPOSList-grid {
    grid-template-columns: 1fr;
  }
  
  /* add other styles here... */
}
```

Your goal is to make only the changes needed for mobile inside the media query. 

You can apply this media query to any of the style sheets you have used. 

**Stretch Challenge**: Handle more screen sizes. 

The plan above handles both desktop top and mobile. This covers a wide range of viewers but there are a lot screens inbetween: iPad, large phones, phones in landscape, or even extra wide desktop screens. 

Write styles to handle these devices! Check your work on a range of screen sizes and use the longer list of break points above to handle these. 

Using Chrome or Safari in developer mode you can test your site in the browser as if it were displayed on a wide range of screens. For example Safari has all of the standard iOS devices. 

- iPhone SE
- iPhone 8 
- iPhone 8 Plus
- iPad Mini (7.9")
- iPad (9.7")
- iPad Pro (10.5")
- iPad Pro (12.9")

Chrome provides a similar list of options. 

You probably won't be writing a media query for each of these. More likely you'll write a media query for phones, tablets, and desktop. 

Here is an example scenario. Imagine you might have 1 column on phones, two columns tablets or big phones, and three columns on desktop and wider screens. Maybe the media queries might look like this: 

```CSS
/* Default styles */
.POPOSList-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  ...
}

@media screen and (max-width: 960px) {
  .POPOSList-grid {
    grid-template-columns: 1fr 1fr;
  }
}

@media screen and (max-width: 480px) {
  .POPOSList-grid {
    grid-template-columns: 1fr;
  }
}
```

Notice that put the media queries in order! The 960px size over writes "default" styles because it comes later in the stylesheet! The same for the 480px styles, these over write the 960px styles. 

Important! When the 480px styles are in effect the 960px styles are also applied! You will need to take this into account as you work! 

**Stretch Challenge**: Responsive Typography

Use the responsive typography examples to adjust the typography with your media queries. 

Responsive typography in CSS is a technique used to ensure that text on a web page adjusts proportionally to different screen sizes and resolutions. This is done by using relative units and media queries to adjust font sizes, line heights, and other typographic properties based on the screen size and orientation. Responsive typography is important for creating a consistent and readable user experience across a variety of devices and user needs.

Here's an example:

```CSS
/* Default font size and line height for body text */
body {
  font-size: 16px;
  line-height: 1.5;
}

/* Media query for screens smaller than 768px */
@media (max-width: 768px) {
  body {
    font-size: 14px;
    line-height: 1.4;
  }
}

/* Media query for screens smaller than 480px */
@media (max-width: 480px) {
  body {
    font-size: 12px;
    line-height: 1.3;
  }
}
```

In this example, the body element is given a default font size of 16 pixels and a line height of 1.5. Two media queries are then used to adjust the font size and line height for smaller screens. The first media query targets screens smaller than 768 pixels, and reduces the font size to 14 pixels and the line height to 1.4. The second media query targets screens smaller than 480 pixels, and further reduces the font size to 12 pixels and the line height to 1.3.

This example is simplified, and in practice, there are many other typographic properties that can be adjusted to create a responsive typography system. Additionally, the specific font sizes and line heights used will depend on the design of the website and the target audience.

**Stretch Challenge**: Responsive Images

Responsive images in web design refer to the practice of optimizing images to be displayed on a variety of screen sizes and resolutions, from small mobile devices to large desktop monitors. The goal is to ensure that images are not only visually appealing but also load quickly and don't take up too much bandwidth.

There are several techniques that can be used to implement responsive images, including:

Using the `<img>` tag with the srcset attribute: This attribute allows you to provide multiple versions of the same image with different resolutions, and the browser can choose the appropriate one based on the device's screen size and pixel density.
Using the `<picture>` tag: This tag allows you to provide multiple versions of an image with different resolutions, sizes, and formats, and the browser can choose the most appropriate one based on the screen size and other factors.
Using CSS to resize and crop images: This technique involves using CSS properties such as max-width, max-height, and object-fit to adjust the size and layout of images based on the screen size and aspect ratio.
Overall, responsive images are important for creating a visually appealing and fast-loading website that provides a good user experience across a variety of devices and screen sizes. By using the appropriate techniques and optimizing images for web delivery, you can ensure that your website looks great and performs well on all devices, from smartphones to large desktop monitors.

Using the srcset attribute:

```HTML
<img src="image.jpg"
  srcset="image-small.jpg 480w,
    image-medium.jpg 768w,
    image-large.jpg 1200w"
  alt="Responsive image">
```

In this example, the srcset attribute is used to provide three different versions of the same image with different resolutions, specified in the w (width) descriptor. The browser can then choose the appropriate image based on the device's screen size and pixel density.

Using the <picture> tag:

```HTML
<picture>
  <source srcset="image.webp" type="image/webp">
  <source srcset="image.jpg" type="image/jpeg">
  <img src="image.jpg" alt="Responsive image">
</picture>
```

In this example, the <picture> tag is used to provide two versions of the same image in different formats (webp and jpeg), and the browser can choose the appropriate one based on the device's support for the formats. If neither format is supported, the <img> tag is used as a fallback.

Using CSS to resize and crop images:

```CSS
img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
}
```

In this example, the max-width property ensures that the image does not exceed the width of its container, and the height: auto property maintains the aspect ratio of the image. The object-fit: cover property ensures that the image is resized and cropped to fill the available space while preserving its aspect ratio.

## Assess your work

| Category | Does not meet | Meets expectations | Exceeds expectations |
|:--------:|:-------------:|:------------------:|:--------------------:|
| Matches the wire frames | Does not match the frames you submitted | Matches the wire frames | Your attention to detail extends to code elements like class names |
| Media Queries | Yoiu haven't used media queries, or your media queries are not working or only partially functional | Your modia queries are applying styles based on the break points | You site is responding to changes in screen size with elegance and grace! |
| Stretch Challenges | You didn't try the stretch challenges | You tried the stretch challenges | You successfully implemented the stretch challenges |








