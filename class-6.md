# Accessibility and Inclusive Design

Objective: Students will learn the principles of accessibility and inclusive design, and how to implement them in web development. They will also learn how to use tools like screen readers and browser plugins to test the accessibility of their websites.

### What is accessibility?

Accessibility in web development refers to designing and developing websites that can be used by people with disabilities or impairments. This ensures that all users, regardless of their abilities, can access web content and services. 

Accessibility is crucial because it promotes inclusivity, improves user experience, enhances search engine optimization, expands the reach of a website, and mitigates legal risks. By ensuring accessibility, web developers can create a more inclusive digital world where everyone has equal access to information and services.

**Laws and regulations related to accessibility (e.g. Americans with Disabilities Act)**

It is important for web developers to be aware of laws and regulations related to accessibility, such as the Americans with Disabilities Act (ADA), Section 508 of the Rehabilitation Act, and the Web Content Accessibility Guidelines (WCAG). These regulations ensure that websites are accessible to individuals with disabilities, such as those who are blind or have low vision, deaf or hard of hearing, or have physical or cognitive disabilities. Compliance with these laws and regulations not only ensures equal access for individuals with disabilities but also mitigates legal risks for businesses and organizations. Therefore, web developers should incorporate accessibility into their development process to ensure compliance with these regulations and promote inclusivity for all users.

**Common barriers to accessibility (e.g. visual, auditory, motor impairments)** 

Accessibility barriers are obstacles that prevent individuals with disabilities from accessing and using digital content and services. Common barriers to accessibility include visual impairments, such as blindness or low vision, auditory impairments, such as deafness or hard of hearing, and motor impairments, such as difficulty using a mouse or keyboard. Other barriers may include cognitive or neurological impairments, such as dyslexia, autism, or environmental factors, such as poor lighting or loud background noise. These barriers can prevent individuals with disabilities from fully participating in the digital world, including accessing educational resources, conducting online transactions, and engaging in social media. 

To ensure accessibility for all users, web developers should consider these barriers when designing and developing digital content and services and provide alternative formats or assistive technologies to accommodate different types of disabilities.

### Inclusive design principles

Suppose a web developer is creating a new e-commerce site. To ensure diversity and inclusivity, the developer could design the site's interface to be easily navigable using assistive technologies, such as screen readers, for users with visual impairments. They could also provide alternative formats for visual content, such as image descriptions, to make the content accessible to users who are blind or have low vision. 

Additionally, the developer could consider the language and cultural background of the site's target audience, using clear and concise language and avoiding cultural stereotypes that could exclude certain groups of people. _Finally, the developer could conduct user testing with people from a diverse range of backgrounds and abilities to ensure that the site is usable and accessible to as many people as possible.

**Challenge** Turn on Voice over and follow the tutorial.

A large portion of the world is browsing the web with accessibility features. To reach this audience it is important to understand accessibility. 

https://accessiblyapp.com/blog/web-accessibility-statistics/

**Challenge:** Considering the information above what changes need to be made to the SFPOPOS site? 

- Considering the paragraphs above, how would you rewrite your user stories?
- What changes to text content and labeling need to be made to your site?
- Are there any changes you can make that would make the site more engaging to a wider audience? 

Why?

Designing for diversity and inclusivity is important because it ensures that digital content and services are accessible and usable by the widest possible audience. By considering the needs of individuals with different abilities, cultural backgrounds, and experiences, web developers can create content and services that are more inclusive, welcoming, and engaging to a broader range of people. This can lead to increased engagement, better user experiences, and ultimately, greater success for businesses and organizations. Moreover, designing for diversity and inclusivity promotes ethical and moral principles of equality and social justice, contributing to a more inclusive and equitable society.

**Prioritizing user needs and preferences**

Prioritizing user needs and preferences in web development involves understanding and designing for the goals and behaviors of the website's target audience. This approach is user-centered and puts the needs and preferences of users at the forefront of the design process. User research and feedback are essential for identifying user needs and preferences and determining which features and functionalities are most important to them. This information can inform the design and development of the website, ensuring that it meets the needs and preferences of its users.

**Challenge**

- What questions would you ask when conducting user research to improve the SFPOPOS site?

Prioritizing user needs and preferences is important because it leads to a better user experience and higher user engagement. When users can easily find the information or services they need and the website is designed in a way that resonates with them, they are more likely to spend time on the site, return to it in the future, and share it with others. Moreover, user-centered design can lead to a competitive advantage, as users are more likely to choose a website that meets their needs over one that does not. Therefore, prioritizing user needs and preferences is a key consideration for web developers who want to create effective and successful websites.

**Providing multiple ways to access information and perform actions**

Providing multiple ways to access information and perform actions is an important consideration in web development to ensure that all users, regardless of their abilities or technological limitations, can access the content and functionalities of a website.

Multiple ways of access could include providing alternative text descriptions for images, videos or other visual content, so that users with visual impairments can understand what is being displayed. Another example could be offering keyboard shortcuts and alternative input methods, such as voice commands or touch gestures, to accommodate users with mobility impairments who may not be able to use a mouse or standard keyboard.

Providing multiple ways of access is important because it ensures that all users can interact with a website, regardless of their abilities or technological limitations. **This promotes inclusivity and reduces the risk of exclusion, which can occur when a website is designed with only one type of user in mind.** By providing multiple ways of access, web developers can ensure that users with disabilities, as well as those who may have limited access to technology or slow internet connections, can still engage with a website and its content in a meaningful way. This can lead to increased engagement and satisfaction for all users, regardless of their backgrounds and abilities.

**Challenge:** Make a list of the things that limit a users ability to access your site? 

### Techniques for accessible web development

Consider your the SFPOPOS site and consider the list below. Find the elements on the list that exist and ask yourself if they are adequate. Indentify the things that are missing and consider how you can implement these. 

- **Semantic HTML** (You've used this before!)
- **Alt text for images** (You've also seen this!)
- **ARIA attributes** Read about ARIA here: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA
- **Proper use of color and contrast** Check your color and contrast here: https://webaim.org/resources/contrastchecker/
- **Keyboard navigation** Read up about accessibility and keyboard navigation: https://www.smashingmagazine.com/2022/11/guide-keyboard-accessibility-html-css-part1/
- **Captions and transcripts** (for video and audio content) 

### Tools for testing accessibility

You'll use the tools below to navigate a web site of your choice. Pick a website you use everyday. Browse it with in accessibility mode doing all of the things you would normally do. Repeat the process with your SFPOPOS site. 

- Screen readers (e.g. NVDA, VoiceOver)
- Browser plugins (e.g. WebAIM's WAVE tool)
- Keyboard-only navigation (You'll use the tab key in accessibility mode)

Second you'll use one the tools below to check the accessibility features of the site you chose. 

You will also check the color contrast for colors on the site. Do this for any background color where text appears. 

- WAVE Chrome extension idenitifies accessibilities in the borwser. 
- https://wave.webaim.org
- [WAVE Extension instructions](https://www.google.com/search?q=how+to+use+wave+chrome+extension&rlz=1C5CHFA_enUS815US815&oq=how+to+use+the+wave+chrome+&aqs=chrome.1.69i57j0i22i30l2j0i390i650l2.8628j0j7&sourceid=chrome&ie=UTF-8)
- [Install Lighthouse chrom extension](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk)
- https://webaim.org/resources/contrastchecker/
- Write better alt text for images: https://accessibility.huit.harvard.edu/describe-content-images

## Screen readers 

To really get a feel for how people with disabilities use a computer try the screen reader. 

- Safari: https://support.apple.com/guide/voiceover/welcome/mac
- Chrome: https://support.google.com/accessibility/answer/7031755?hl=en

## Challenge: What is Accessibility?

Answer these questions on GradeScope: 

- What is Accessibility in web design and why is it important?
- Why is semantic HTML and ARIA, and how are they related? 

## Challenge: Accessibility Review!

Review and evaluate the accessibility of a website of your choice. This can be any site you like, a site you use everyday is preferable, buy soap and fuzzy slippers on Amazon, check out cat pictures on reddit, order Airpods Max on the Apple store. 

- Browse the site with the keyboard and screen reader
- Run an accessiblity review using the tools above

Repeat the process with your SFPOPOS site. 

- Browser the website **with your keyboard** and a screen reader. This is a tedious and annoying process. Do not give up or skip this out of frustration. Sympathize with the segment of the population that does this everyday. 
- While using the screent identify the areas that can be improved. Look at:
  - Naming and labels
  - The order elements appear
  - Alt text

If you are unable to use the mouse you'll use the keyboard to navigate. This can be especially frustrating. Put your developer hat on for a few minutes, as if you ever take it off. You can move through each element on the page using the arrow keys. You can also move through navigational and control elements like buttons and text inputs using the tab, and option + tab, and the shift key and you can move backwards. 

To enabled tabbing through the links on a page, in Chrome use the tab key, in Safari use option + tab. 

Notice the order of things on the screen as you tab over them. Does this makes sense? You can control the tab order using the `tabindex` attribute. Read about it here: https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex

Spend some time playing with this. It gets frustrating really fast. Think about how it would be to use this site every day? The challenge is to reduce the frustration of this process.

Think of all of the ways you can improve the acccessibility of the site you are studying. 

Use lighthouse to score your pages. You can do as much work on your site as you like. I will score this assignment on the lowest scoring page. My solution project from the tutorial scored 81%. 
