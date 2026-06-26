That's a very broad topic. HTML interview preparation can easily span 200+ questions from beginner to advanced level. A single response can't fit all of that in enough detail.

A practical way to cover everything is to go through it as a complete interview course. Here's a structured roadmap:

1. HTML Basics (30+ Questions)


2. HTML Elements & Attributes (25+ Questions)


3. Forms (40+ Questions)


4. Semantic HTML (30+ Questions)


5. Tables & Lists (20+ Questions)


6. Multimedia (20+ Questions)


7. Meta Tags & SEO (30+ Questions)


8. Accessibility (ARIA) (35+ Questions)


9. HTML5 APIs (30+ Questions)


10. Storage (Cookies, LocalStorage, SessionStorage)


11. Canvas & SVG


12. Responsive HTML


13. Performance Optimization


14. Advanced HTML5 Features


15. Scenario-Based Questions


16. Coding Questions


17. Tricky Interview Questions


18. Frequently Asked Questions in MNCs (TCS, Infosys, Wipro, Accenture, Capgemini, Cognizant, Deloitte, IBM, Amazon, Google, Microsoft)



Below is Part 1 in detail.


---

HTML Interview Guide (Part 1)

Q1. What is HTML?

Answer

HTML stands for HyperText Markup Language.

It is the standard markup language used to create web pages.

HTML provides the structure of a webpage.

It is not a programming language because it cannot perform logic like loops, conditions, or calculations.

CSS is used for styling.

JavaScript is used for functionality.

Example

<!DOCTYPE html>
<html>
<head>
    <title>My Website</title>
</head>
<body>

<h1>Hello World</h1>

</body>
</html>


---

Explanation

Step 1

<!DOCTYPE html>

Tells the browser that this document uses HTML5.


---

Step 2

<html>

Root element.

Everything is written inside it.


---

Step 3

<head>

Contains

Title

Meta tags

CSS links

Scripts


Not visible to users.


---

Step 4

<body>

Contains all visible content.


---

Interview Tip

Question:

Is HTML a programming language?

Correct Answer:

No.

Because HTML does not have

Variables

Loops

Functions

Conditions


It is a markup language.


---

Q2. What is HyperText?

HyperText means text that contains links.

Example

<a href="https://google.com">
Google
</a>

Clicking the link moves to another page.


---

Q3. What is Markup Language?

A markup language uses tags to describe the structure of content.

Example

<h1>Heading</h1>

<p>Paragraph</p>

Tags tell the browser how content is organized.


---

Q4. Explain HTML Page Structure

<!DOCTYPE html>

<html>

<head>

<title>Page</title>

</head>

<body>

Content

</body>

</html>

Explanation

DOCTYPE
      │
      ▼

<html>

    │

    ├── head

    │      ├── title

    │      ├── meta

    │      └── link

    │

    └── body

           ├── h1

           ├── p

           ├── img

           └── button


---

Q5. What is the purpose of <!DOCTYPE html>?

It tells the browser to render the page in HTML5 standards mode.

Without it:

Browser may enter Quirks Mode.

Layout can behave inconsistently.


Example

<!DOCTYPE html>

Always place it at the top.


---

Q6. What are HTML Tags?

Tags define HTML elements.

Example

<h1>Hello</h1>

Opening tag

<h1>

Closing tag

</h1>


---

Q7. What are HTML Elements?

An HTML element consists of:

Opening tag

Content

Closing tag


Example

<p>Hello World</p>

Entire line is one HTML element.


---

Q8. What are Attributes?

Attributes provide additional information.

Example

<img src="cat.jpg" alt="Cat">

Attributes:

src
alt


---

Common attributes

id

class

style

title

href

src

alt

name

value

placeholder

disabled

readonly

required


---

Q9. Difference between Tags and Elements

Tag

<p>

Element

<p>Hello</p>

Interview Answer

Tag is only the opening or closing marker.

Element includes the complete structure with content.


---

Q10. Difference between Block and Inline Elements

Block Elements

Take full width.

Start from a new line.

Examples

<div>

<h1>

<p>

section

article

header

footer

Example

<div>One</div>

<div>Two</div>

Output

One

Two


---

Inline Elements

Take only required width.

Remain on the same line.

Examples

span

a

img

strong

em

label

Example

<span>Hello</span>

<span>World</span>

Output

Hello World


---

Q11. Difference between <div> and <span>

Feature	<div>	<span>

Display	Block	Inline
Width	Full	Content only
New line	Yes	No
Used for	Layout	Small text styling


Example

<div>
Welcome
</div>

<span>
Welcome
</span>


---

Q12. What are Void (Empty) Elements?

These elements do not require closing tags.

Examples

<br>

<hr>

<img>

<input>

<meta>

<link>

<source>

<area>

<base>

<col>

<embed>

<track>

<wbr>

Example

<img src="cat.jpg">

No closing tag is needed.


---

Q13. Difference between HTML4 and HTML5

HTML4	HTML5

No semantic tags	Semantic tags available
No video support	Video supported
No audio	Audio supported
Uses plugins	Built-in multimedia
Limited APIs	Many APIs
No localStorage	localStorage supported



---

Q14. What are Semantic Tags?

Semantic tags describe the meaning of content.

Examples

<header>

<nav>

<main>

<section>

<article>

<aside>

<footer>

<figure>

<figcaption>

<details>

<summary>

Benefits

Better SEO

Better accessibility

Cleaner code

Easier maintenance



---

Q15. Difference between <b> and <strong>

<b>

Only makes text bold.

<b>Important</b>

<strong>

Makes text bold and indicates strong importance.

<strong>Important</strong>

Screen readers emphasize <strong>.


---

Q16. Difference between <i> and <em>

<i>

Displays italic text for stylistic purposes.

<i>Book Title</i>

<em>

Adds emphasis, which screen readers may convey.

<em>Warning</em>


---

Q17. What is the difference between id and class?

id	class

Unique on a page	Can be reused
One element	Many elements
Used for unique identification	Used to group elements
Selected with # in CSS	Selected with . in CSS


Example:

<div id="header"></div>

<p class="note">First</p>
<p class="note">Second</p>


---

Q18. What is the difference between alt and title attributes?

alt

Describes an image if it cannot be displayed.

Used by screen readers.

Important for accessibility and SEO.


<img src="logo.png" alt="Company logo">

title

Shows a tooltip when the user hovers over the element.

Does not replace alt.


<img src="logo.png" alt="Company logo" title="Open company homepage">


---

Q19. Why is the alt attribute important?

The alt attribute:

Helps users with screen readers understand the image.

Displays descriptive text if the image fails to load.

Improves accessibility.

Can provide SEO benefits by giving search engines context.



---

Q20. What is the difference between data-* attributes and standard attributes?

data-* attributes let you store custom data on HTML elements.

Example:

<button data-user-id="123" data-role="admin">
  Edit
</button>

JavaScript can access these values through the element's dataset property, making them useful for storing small pieces of page-specific information without inventing non-standard attributes.


---

Common HTML Interview Tips

Interviewers often ask follow-up questions such as:

Why use semantic HTML instead of many <div> elements?

When would you use id versus class?

Why is accessibility important?

What happens if <!DOCTYPE html> is omitted?

Can multiple elements share the same id? (They should not; id values are intended to be unique within a page.)


Recommended Learning Order

1. HTML Basics


2. Elements and Attributes


3. Headings, Paragraphs, Lists, and Links


4. Images and Multimedia


5. Tables


6. Forms (very commonly asked)


7. Semantic HTML


8. Accessibility (ARIA)


9. HTML5 APIs


10. SEO and Performance


11. Advanced and Scenario-Based Questions



This first part covers the core concepts that form the foundation of most HTML interviews. Subsequent parts can build into intermediate and advanced topics, including forms, semantic HTML, accessibility, HTML5 APIs, and coding exercises.
