Excellent. Now we'll cover one of the most important interview topics: Semantic HTML, Accessibility, and SEO. These are asked frequently in interviews for companies ranging from startups to large tech firms because they reflect how well you build maintainable, accessible, and search-friendly web pages.

HTML Interview Guide – Part 3 (Semantic HTML, Accessibility & SEO)


---

Q41. What is Semantic HTML?

Answer

Semantic HTML means using HTML elements that clearly describe the purpose of their content, rather than just how it looks.

Instead of using generic containers everywhere:

<div>
    Header
</div>

Use semantic elements:

<header>
    Header
</header>

The element name itself communicates its role.


---

Why is Semantic HTML Important?

1. Improves readability.


2. Helps search engines understand page structure.


3. Improves accessibility.


4. Makes code easier to maintain.


5. Helps assistive technologies such as screen readers.




---

Example

Non-semantic

<div id="header"></div>

<div id="menu"></div>

<div id="content"></div>

<div id="footer"></div>


---

Semantic

<header></header>

<nav></nav>

<main></main>

<footer></footer>

The second version is easier for both developers and assistive technologies to understand.


---

Q42. Explain the <header> element.

The <header> element contains introductory content for a page or a section.

It often includes:

Logo

Website title

Search bar

Navigation (though navigation can also be in a separate <nav>)


Example

<header>

<h1>My Website</h1>

</header>


---

Interview Tip

A page can have more than one <header>. For example, an <article> can have its own header.


---

Q43. Explain the <nav> element.

The <nav> element contains major navigation links.

Example

<nav>

<a href="/">Home</a>

<a href="/about">About</a>

<a href="/contact">Contact</a>

</nav>


---

Why use <nav>?

Search engines and screen readers recognize it as a navigation area.


---

Q44. Explain the <main> element.

The <main> element contains the primary content of the document.

Example

<main>

<h2>Products</h2>

<p>Our latest products...</p>

</main>


---

Rules

Only one <main> element should exist per page.

It should contain the central content unique to that page.



---

Q45. Explain the <section> element.

A <section> groups related content around a theme.

Example

<section>

<h2>Services</h2>

<p>Web Development</p>

</section>


---

Use <section> when

The content has a clear topic.

It typically has a heading.


Examples:

About Us

Features

Pricing

Contact



---

Q46. Explain the <article> element.

An <article> represents a self-contained piece of content that could stand on its own.

Examples:

Blog post

News article

Forum post

Product review


Example

<article>

<h2>HTML Tutorial</h2>

<p>HTML is a markup language...</p>

</article>


---

Difference Between <article> and <section>

<article>	<section>

Self-contained	Groups related content
Can often be reused or syndicated independently	Usually part of a larger page
Example: Blog post	Example: Features section



---

Q47. Explain the <aside> element.

<aside> contains content related to, but separate from, the main content.

Examples:

Sidebar

Advertisements

Related posts

Author information


Example

<aside>

<h3>Related Articles</h3>

</aside>


---

Q48. Explain the <footer> element.

Contains closing information for a page or section.

Common content:

Copyright

Contact information

Privacy policy

Social media links


Example

<footer>

<p>© 2026 My Website</p>

</footer>


---

Q49. Difference Between <div> and Semantic Elements

<div>

Generic container.

<div>
Content
</div>

No meaning is conveyed.


---

Semantic Element

<section>
Content
</section>

Conveys purpose.


---

Comparison

<div>	Semantic element

Generic	Meaningful
No inherent role	Describes content
Often used for layout	Used for document structure



---

Q50. Explain <figure> and <figcaption>.

Used for images, diagrams, code samples, or charts with captions.

Example

<figure>

<img src="cat.jpg" alt="A cat">

<figcaption>
Sleeping Cat
</figcaption>

</figure>


---

Benefits

Better semantics.

Clear association between media and caption.



---

Q51. Explain <details> and <summary>.

Creates expandable content without JavaScript.

Example

<details>

<summary>Read More</summary>

<p>Extra information...</p>

</details>


---

Output

▶ Read More

(click)

▼ Read More

Extra information...


---

Q52. What is Accessibility?

Accessibility means designing websites so people with disabilities can use them.

Examples include supporting users who:

Use screen readers

Cannot use a mouse

Have low vision

Have color vision deficiencies

Rely on keyboard navigation



---

Why Accessibility Matters

Improves usability.

Supports more users.

May be required by organizational or legal standards.

Often improves overall code quality.



---

Q53. What is ARIA?

ARIA stands for Accessible Rich Internet Applications.

ARIA attributes provide additional information to assistive technologies, especially when native HTML semantics are insufficient.

Example

<button
aria-label="Close">
X
</button>

A screen reader announces:

Close button


---

Common ARIA Attributes

Attribute	Purpose

aria-label	Gives an accessible name
aria-hidden	Hides content from assistive technologies
aria-expanded	Indicates whether content is expanded
aria-controls	Identifies the controlled element
aria-describedby	References descriptive text



---

Interview Tip

Prefer native HTML elements first. Use ARIA only when native semantics cannot provide the required accessibility.


---

Q54. Why is the alt attribute important?

Example

<img
src="dog.jpg"
alt="Golden Retriever">

Benefits:

Screen readers announce the description.

Displays text if the image cannot load.

Improves accessibility.

Can help search engines understand the image.


For decorative images, an empty alt="" is often appropriate so screen readers skip them.


---

Q55. What are Meta Tags?

Meta tags provide information about the page.

Example

<meta charset="UTF-8">

<meta
name="viewport"
content="width=device-width, initial-scale=1.0">

<meta
name="description"
content="HTML Tutorial">

Meta tags belong inside the <head> element.


---

Q56. Explain the Viewport Meta Tag.

<meta
name="viewport"
content="width=device-width, initial-scale=1.0">

This helps pages display correctly on mobile devices.

Without it, pages may appear zoomed out or not adapt to the device width.


---

Q57. What is SEO?

SEO stands for Search Engine Optimization.

It is the practice of improving a website so search engines can better understand and rank its content.


---

HTML's Role in SEO

Use:

Semantic HTML

Descriptive page titles

Meta descriptions

Heading hierarchy

Descriptive alt text

Meaningful link text



---

Q58. Why is the <title> tag important?

Example

<title>

Learn HTML

</title>

It:

Appears in browser tabs.

Is commonly shown in search engine results.

Helps users identify the page.



---

Q59. Explain Heading Tags.

Available heading levels:

<h1>

<h2>

<h3>

<h4>

<h5>

<h6>


---

Best Practices

Use one primary <h1> to represent the main topic of the page (while HTML allows more than one in some contexts, a single clear main heading is a common best practice).

Use headings in order where it makes sense (<h2> under <h1>, <h3> under <h2>, etc.).

Don't choose heading levels based on appearance—use CSS for styling.



---

Q60. Common Semantic HTML Interview Questions

1. Why should we use Semantic HTML?

Answer: It improves readability, accessibility, SEO, and maintainability.


---

2. Difference between <section> and <div>?

<section> groups related content around a theme, often with a heading. <div> is a generic container.


---

3. Difference between <section> and <article>?

An <article> is self-contained and can stand alone. A <section> organizes related content within a page.


---

4. What is ARIA?

A set of accessibility attributes that supplement HTML semantics when necessary.


---

5. What is the purpose of the viewport meta tag?

It helps ensure pages render properly on different screen sizes, especially mobile devices.


---

6. Why are meta tags important?

They provide metadata used by browsers, search engines, and other tools.


---

7. What is the difference between alt and title?

alt describes images for accessibility and when images fail to load.

title typically provides additional information as a tooltip in supporting browsers.



---

8. Why should images have alt text?

To improve accessibility and provide a text alternative when images cannot be seen.


---

9. Why should headings be used in order?

A logical heading structure helps users, screen readers, and search engines understand the page organization.


---

10. Why is <main> important?

It identifies the primary content of the page, making navigation easier for assistive technologies and clarifying document structure.


---

Interviewer Challenge Question

Question: Can we build an entire website using only <div> elements?

Answer: Yes, browsers can render it, but it's not recommended. Using semantic elements makes the document easier to understand, improves accessibility, and generally benefits SEO and long-term maintenance.


---

In Part 4, we'll cover HTML Tables, Lists, Multimedia (Audio/Video), Iframes, Canvas, SVG, and HTML5 APIs, followed by advanced and scenario-based interview questions.
