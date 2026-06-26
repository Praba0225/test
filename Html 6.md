HTML Interview Guide – Part 6 (Company Interview Questions, Tricky Questions, Coding Challenges & Rapid Fire)

This section is designed as a mock interview. It includes the kinds of HTML questions that commonly appear in technical interviews across startups and larger companies. The exact questions vary by interviewer and role, but these are representative of the concepts that are frequently assessed.


---

Beginner Level Questions

Q101. What is HTML?

Answer

HTML (HyperText Markup Language) is the standard markup language used to structure web pages.

It defines the page structure using elements such as headings, paragraphs, forms, tables, and images.


---

Q102. Why do we use HTML?

HTML is used to:

Create web pages

Structure content

Display text, images, videos, and forms

Connect pages using hyperlinks



---

Q103. Is HTML case-sensitive?

Answer

No.

HTML element and attribute names are case-insensitive, but the convention is to write them in lowercase.

Recommended:

<p>Hello</p>

Avoid:

<P>Hello</P>


---

Q104. What happens if closing tags are missing?

Some elements may be automatically closed by the browser, but relying on this can lead to unexpected behavior.

Example:

<p>Hello

<p>World

Browsers attempt to correct the markup, but you should always write valid HTML.


---

Q105. Can multiple elements have the same id?

Answer

No.

An id should be unique within a page.

Incorrect:

<div id="box"></div>

<div id="box"></div>

Correct:

<div id="box1"></div>

<div id="box2"></div>

Use class when multiple elements need the same styling or behavior.


---

Intermediate Questions

Q106. Difference between id and class

id	class

Unique	Reusable
Selected with #	Selected with .
One element per page	Multiple elements



---

Q107. Why use Semantic HTML?

Benefits:

Better SEO

Better accessibility

Easier maintenance

Cleaner code

More meaningful structure



---

Q108. Difference between <section> and <article>

<article>

Independent content.

Example:

News article

Blog post

Product review


<section>

Groups related content within a page.


---

Q109. Difference between <strong> and <b>

<b>

Visual bold text


<strong>

Indicates strong importance

Usually displayed bold by default



---

Q110. Difference between <em> and <i>

<i>

Stylistic italics


<em>

Adds emphasis with semantic meaning



---

Advanced Questions

Q111. Explain the Browser Rendering Process

Answer

HTML
↓

DOM

↓

CSS

↓

CSSOM

↓

Render Tree

↓

Layout

↓

Paint

↓

Screen

This is one of the most common advanced HTML interview questions.


---

Q112. What is the DOM?

DOM = Document Object Model

JavaScript uses the DOM to:

Add elements

Remove elements

Update elements

Handle events



---

Q113. Difference between HTML and DOM

HTML	DOM

Source document	Browser representation
Static markup	Dynamic object model



---

Q114. Difference between Local Storage and Cookies

Local Storage	Cookies

Larger capacity	Smaller capacity
Not sent with every HTTP request	Can be sent with HTTP requests
Good for client-side data	Often used for sessions



---

Q115. Difference between SVG and Canvas

SVG	Canvas

Vector	Pixel
DOM elements	Pixel drawing
Best for icons	Best for games



---

Tricky HTML Questions

Q116. Can a webpage have multiple <header> elements?

Answer

Yes.

Each section or article may have its own <header>.

Example:

<header>
Website Header
</header>

<article>

<header>
Article Header
</header>

</article>


---

Q117. Can a webpage have multiple <main> elements?

Answer

No.

A page should contain only one <main> element representing its primary content.


---

Q118. Does required replace server-side validation?

Answer

No.

Browser validation improves the user experience, but the server must still validate all submitted data because client-side checks can be bypassed.


---

Q119. Can JavaScript change HTML?

Yes.

Example:

document.querySelector("h1").textContent = "Welcome";


---

Q120. Can CSS work without HTML?

No.

CSS styles HTML (or other document languages). Without a document to style, CSS has nothing to apply to.


---

Coding Questions

Q121. Create a Login Form

<form>

<label>Email</label>

<input
type="email"
required>

<label>Password</label>

<input
type="password"
required>

<button>
Login
</button>

</form>


---

Q122. Create a Table

<table border="1">

<tr>

<th>Name</th>

<th>Age</th>

</tr>

<tr>

<td>John</td>

<td>25</td>

</tr>

</table>


---

Q123. Create Nested Lists

<ul>

<li>Frontend

<ul>

<li>HTML</li>

<li>CSS</li>

</ul>

</li>

</ul>


---

Q124. Create Navigation

<nav>

<a href="#">Home</a>

<a href="#">About</a>

<a href="#">Services</a>

<a href="#">Contact</a>

</nav>


---

Q125. Embed a Video

<video controls>

<source
src="video.mp4"
type="video/mp4">

</video>


---

Scenario-Based Questions

Q126. Why is your website not SEO-friendly?

Possible reasons:

Missing semantic HTML

Poor heading hierarchy

Missing <title>

Missing meta description

Images without alt

Generic link text (for example, many "Click here" links)



---

Q127. Why is Accessibility Poor?

Possible causes:

Missing labels

Missing alt

Incorrect heading order

Poor keyboard support

Low color contrast (often addressed with CSS/design)



---

Q128. Users cannot submit the form.

Check:

Required fields

Form action

Form method

JavaScript errors (if applicable)

Server-side handling



---

Q129. Images are not showing.

Possible causes:

Wrong file path

Missing file

Incorrect file extension

Server configuration issues



---

Q130. Website loads slowly.

Possible improvements:

Compress images

Reduce unnecessary HTML

Minify CSS and JavaScript

Lazy load images

Optimize server responses



---

Rapid Fire Questions

What tag creates a paragraph?

<p>


---

What tag creates a heading?

<h1>


---

Largest heading?

<h1>


---

Smallest heading?

<h6>


---

Image tag?

<img>


---

Link tag?

<a>


---

Form tag?

<form>


---

Table tag?

<table>


---

Ordered list?

<ol>


---

Unordered list?

<ul>


---

List item?

<li>


---

Line break?

<br>


---

Horizontal line?

<hr>


---

Bold semantic tag?

<strong>


---

Italic semantic tag?

<em>


---

Page title?

<title>


---

Metadata?

<meta>


---

External CSS?

<link>


---

External JavaScript?

<script>


---

Main content?

<main>


---

Navigation?

<nav>


---

Footer?

<footer>


---

Header?

<header>


---

Frequently Asked Interview Questions

1. What is HTML?

The standard markup language for structuring web pages.


---

2. Difference between HTML and HTML5?

HTML5 introduced semantic elements, multimedia support, improved forms, and browser APIs.


---

3. Difference between id and class?

id is unique; class is reusable.


---

4. Difference between GET and POST?

GET appends data to the URL and is typically used for retrieval. POST sends data in the request body and is commonly used for creating or updating data.


---

5. Difference between div and span?

div is a block-level container; span is an inline container.


---

6. Difference between section and article?

section groups related content; article represents self-contained content.


---

7. Difference between strong and b?

strong adds semantic importance; b is primarily presentational.


---

8. Difference between SVG and Canvas?

SVG is vector-based; Canvas is pixel-based.


---

9. Difference between Local Storage and Session Storage?

Local Storage persists until cleared; Session Storage lasts for the current browser tab/session.


---

10. What are semantic tags?

Elements that describe the meaning and role of their content, such as <header>, <nav>, <main>, <article>, and <footer>.


---

Final Interview Tips

For Freshers (0–2 years)

Focus on:

HTML structure

Forms

Tables

Lists

Semantic HTML

Accessibility basics

HTML5 features


For Experienced Developers (2+ years)

Be prepared to discuss:

Semantic HTML and accessibility

SEO considerations

Browser rendering process

Performance optimization

Progressive enhancement

Advanced HTML5 APIs

Real-world implementation decisions



---

Complete HTML Learning Roadmap

1. HTML Basics


2. Elements & Attributes


3. Text Formatting


4. Links & Images


5. Lists


6. Tables


7. Forms


8. Semantic HTML


9. Multimedia


10. Iframes


11. SVG & Canvas


12. HTML5 APIs


13. Accessibility


14. SEO


15. Browser Rendering


16. Performance


17. Storage (Cookies, Local Storage, Session Storage)


18. Scenario-Based Questions


19. Coding Challenges


20. Mock Interviews



If you can confidently explain and implement the topics across these six parts, you'll have a strong foundation for HTML interviews ranging from entry-level frontend roles to many intermediate frontend positions.
