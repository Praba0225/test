HTML Interview Guide – Part 5 (Advanced HTML5, Performance, Browser Rendering & Scenario-Based Questions)

This section covers advanced HTML interview topics commonly asked in interviews for developers with 2+ years of experience and in technical rounds at larger companies.


---

Q81. What is HTML5?

Answer

HTML5 is the latest major version of HTML. It introduced semantic elements, built-in multimedia support, new form controls, browser storage, and several APIs that reduce the need for external plugins.

Features

Semantic elements

Audio and video support

Canvas

SVG support

Local Storage

Session Storage

Improved forms

Geolocation API

Drag and Drop API

Web Workers (JavaScript API used with HTML pages)



---

Interview Tip

Question: Why was HTML5 introduced?

Answer: To make web applications more powerful by improving semantics, multimedia support, forms, and browser APIs without relying heavily on plugins like Flash.


---

Q82. What are HTML5 APIs?

HTML5 works with several browser APIs to provide advanced features.

Some commonly used APIs include:

Geolocation API

Drag and Drop API

Web Storage API

History API

Web Workers

WebSocket API

File API



---

Q83. Explain the Geolocation API.

The Geolocation API allows a webpage to request the user's current location. The browser asks the user for permission before sharing location data.

JavaScript Example

navigator.geolocation.getCurrentPosition(
  (position) => {
    console.log(position.coords.latitude);
    console.log(position.coords.longitude);
  }
);

Flow

Website requests location
          ↓
Browser asks permission
          ↓
User allows or denies
          ↓
Location returned (if allowed)


---

Interview Question

Does a website automatically know the user's location?

No. The user must grant permission first.


---

Q84. What is Drag and Drop?

Drag and Drop allows users to move elements using the mouse or another pointing device.

Example use cases:

Trello boards

File uploads

Kanban applications

Dashboard widgets


Common HTML attribute:

<div draggable="true">
    Drag me
</div>

JavaScript handles the drag events.


---

Q85. What are Web Workers?

Web Workers allow JavaScript to run tasks in a background thread, helping keep the user interface responsive.

Why?

Without Web Workers:

Heavy Calculation
        ↓
Browser UI freezes

With Web Workers:

Heavy Calculation
        ↓
Worker Thread
        ↓
UI remains responsive


---

Uses

Image processing

Large calculations

Data parsing

Background tasks



---

Q86. What is the History API?

The History API lets JavaScript update the browser history without reloading the page.

Common methods:

history.back();

history.forward();

history.go(-1);

Modern single-page applications also use methods such as pushState() and replaceState().


---

Used In

Single Page Applications (SPAs)

Client-side routing



---

Q87. What is the File API?

The File API lets users select files and allows JavaScript to read information about those files (subject to browser security rules).

Example:

<input type="file">

Common uses:

Image preview

PDF upload

Resume upload



---

Q88. What is Browser Rendering?

Browser rendering is the process of converting HTML, CSS, and JavaScript into the visual page users see.

Simplified Rendering Process

HTML
   ↓
DOM Tree

CSS
   ↓
CSSOM Tree

DOM + CSSOM
      ↓
Render Tree
      ↓
Layout
      ↓
Paint
      ↓
Display


---

Step-by-Step

Step 1

Browser downloads HTML.

Step 2

Creates the DOM (Document Object Model).

Step 3

Downloads CSS and creates the CSSOM.

Step 4

Combines them into the Render Tree.

Step 5

Calculates element sizes and positions (Layout).

Step 6

Paints pixels to the screen.


---

Q89. What is the DOM?

DOM stands for Document Object Model.

It is an object representation of the HTML document that JavaScript can read and modify.

HTML:

<p>Hello</p>

DOM representation:

Document

   |

 html

   |

 body

   |

  p

   |

Hello

JavaScript can update the DOM dynamically.


---

Q90. Difference Between DOM and HTML

HTML	DOM

Source markup	In-memory object model
Static file	Can change dynamically
Written by developers	Managed by the browser and accessible via JavaScript



---

Q91. What is Progressive Enhancement?

Progressive Enhancement means building the basic functionality first so it works for everyone, then adding advanced features for browsers that support them.

Layers

HTML
↓

CSS
↓

JavaScript

If JavaScript fails, users should still be able to access essential content whenever possible.


---

Q92. What is Graceful Degradation?

Graceful Degradation starts with a full-featured experience and ensures the application still functions reasonably on older browsers.


---

Difference

Progressive Enhancement	Graceful Degradation

Build basic first	Build advanced first
Add enhancements	Reduce features if needed
Prioritizes broad accessibility	Prioritizes modern experience



---

Q93. How can HTML Performance be Improved?

1. Use Semantic HTML

Cleaner structure and easier maintenance.


---

2. Optimize Images

Use:

Appropriate image dimensions

Modern formats (when supported)

Compression

Lazy loading where appropriate


Example:

<img
src="photo.jpg"
loading="lazy"
alt="Mountain landscape">


---

3. Reduce DOM Size

Instead of deeply nested elements:

<div>

<div>

<div>

<div>

Text

</div>

</div>

</div>

</div>

Prefer simpler structures where possible.


---

4. Avoid Unnecessary Elements

Use only the elements you need.


---

5. Minimize Blocking Resources

Load CSS and JavaScript thoughtfully to improve page rendering.


---

Q94. What is Lazy Loading?

Lazy loading delays loading resources until they are needed.

Example:

<img
src="cat.jpg"
loading="lazy"
alt="Cat">

The image loads when it approaches the viewport.


---

Benefits

Faster initial page load

Reduced bandwidth usage

Better user experience on long pages



---

Q95. What is the Difference Between defer and async?

async

<script
async
src="app.js"></script>

Downloads in parallel with HTML parsing.

Executes as soon as it finishes downloading.

Execution order is not guaranteed between multiple async scripts.


Use when scripts are independent.


---

defer

<script
defer
src="app.js"></script>

Downloads in parallel with HTML parsing.

Executes after the HTML has been fully parsed.

Deferred scripts execute in document order.


Suitable for scripts that depend on the DOM.


---

Comparison

async	defer

Executes immediately after download	Executes after HTML parsing
Order not guaranteed	Order preserved
Good for independent scripts	Good for application scripts



---

Q96. What are Web Components?

Web Components let you create reusable custom HTML elements using web platform standards.

They are built using technologies such as:

Custom Elements

Shadow DOM

HTML Templates


Example:

<user-card></user-card>


---

Benefits

Reusable

Encapsulated

Framework-independent



---

Q97. Difference Between Canvas and SVG (Advanced)

SVG

Vector graphics

Individual shapes remain editable

Better for diagrams and icons


Canvas

Pixel-based

Faster for rendering many changing graphics

Better for games and animations



---

Q98. What are Custom Data Attributes?

Store custom data using data-*.

Example

<div
data-user-id="101"
data-role="admin">
</div>

JavaScript:

element.dataset.userId;


---

Q99. What is Shadow DOM?

Shadow DOM creates an isolated DOM tree for a component.

Benefits:

Encapsulated styles

Reduced style conflicts

Better component reusability


Used extensively in Web Components.


---

Q100. What are the Most Common Advanced HTML Interview Questions?

1. Difference between HTML and DOM?

Answer:

HTML is the document markup.

DOM is the browser's object representation of that document.


---

2. Difference between Canvas and SVG?

SVG is vector-based.

Canvas is pixel-based.


---

3. Difference between async and defer?

async executes as soon as it downloads.

defer waits until the HTML has been parsed and preserves script order.


---

4. Difference between Progressive Enhancement and Graceful Degradation?

Progressive Enhancement builds from a basic, widely compatible experience.

Graceful Degradation starts with advanced features and provides acceptable fallbacks.


---

5. What is Lazy Loading?

Loading resources only when needed.


---

6. Why should the DOM be small?

A simpler DOM generally improves rendering performance and makes maintenance easier.


---

7. Can JavaScript change HTML?

Yes. JavaScript can add, remove, and update elements through the DOM.


---

8. Why are semantic tags better than many <div> elements?

They improve readability, accessibility, and SEO.


---

9. Difference between Local Storage and Session Storage?

Local Storage persists until cleared.

Session Storage is cleared when the browser tab or session ends.


---

10. What are Web Components?

Reusable custom HTML elements built with web platform standards.


---

Scenario-Based Interview Questions

Scenario 1

Question: A page loads slowly because it contains 500 large images. How would you improve it?

Answer:

Compress images.

Use responsive image techniques where appropriate.

Enable lazy loading.

Choose modern image formats when suitable.

Serve appropriately sized images.



---

Scenario 2

Question: Your website doesn't work without JavaScript. What should you improve?

Answer:

Apply progressive enhancement so essential content and core functionality remain available whenever practical, even if JavaScript is unavailable.


---

Scenario 3

Question: Users complain the page freezes during heavy calculations.

Answer:

Move intensive computations to a Web Worker so the main UI thread remains responsive.


---

Scenario 4

Question: An image isn't loading.

Answer:

Check the image path.

Verify the file exists.

Ensure the server serves the file correctly.

Include meaningful alt text so users still receive context if the image fails to load.



---

What's Next?

The next section (Part 6) will focus on 150+ company-style HTML interview questions, including:

Amazon interview questions

Microsoft interview questions

Google interview questions

TCS, Infosys, Wipro, Accenture, Cognizant, Capgemini, IBM interview questions

Tricky HTML questions

Rapid-fire questions

Coding challenges

Real interview scenarios

HR and technical HTML discussions


This final part is designed as a comprehensive interview practice set.
