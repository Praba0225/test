Excellent. CSS Selectors and Specificity are among the most frequently asked topics in frontend interviews because they test whether you understand how CSS targets elements and resolves conflicts.

CSS Interview Guide – Part 2 (Selectors, Combinators & Specificity)


---

Q21. What is a CSS Selector?

Answer

A CSS selector is used to target HTML elements so that styles can be applied.

Example:

<h1>Welcome</h1>

h1 {
    color: blue;
}

Step-by-Step

1. Browser reads the HTML.


2. Browser reads the CSS.


3. Selector h1 matches every <h1> element.


4. The color property is applied.




---

Q22. What are the Different Types of CSS Selectors?

The most common selectors are:

Selector	Example	Purpose

Element	p	Selects all <p> elements
Class	.box	Selects elements with a class
ID	#header	Selects an element with a specific ID
Universal	*	Selects all elements
Group	h1, p	Selects multiple selectors
Attribute	[type="text"]	Selects based on attributes
Descendant	div p	Selects nested elements
Child	div > p	Selects direct children
Adjacent Sibling	h1 + p	Selects the next sibling
General Sibling	h1 ~ p	Selects following siblings



---

Q23. Element Selector

Targets all elements of a specific type.

Example

p {
    color: red;
}

HTML

<p>One</p>

<p>Two</p>

Both paragraphs become red.


---

Q24. Class Selector

Targets elements with a class.

HTML

<p class="note">
Hello
</p>

CSS

.note {
    color: blue;
}


---

Why use classes?

Because they can be reused across many elements.

Example

<div class="box"></div>

<p class="box"></p>

<button class="box">

All three can share the same styles.


---

Q25. ID Selector

Targets one unique element.

HTML

<h1 id="title">
Hello
</h1>

CSS

#title {
    color: green;
}


---

Interview Tip

Use id for unique elements.

Use class for reusable styling.


---

Q26. Universal Selector

Selects every element.

* {
    margin: 0;
    padding: 0;
}

Commonly used as part of a CSS reset or normalization strategy.


---

Q27. Group Selector

Styles multiple selectors together.

Instead of

h1 {
    color: blue;
}

h2 {
    color: blue;
}

h3 {
    color: blue;
}

Use

h1,
h2,
h3 {
    color: blue;
}

Less repetition.


---

Q28. Attribute Selector

Targets elements based on their attributes.

Example

input[type="text"] {
    border: 1px solid blue;
}

HTML

<input type="text">

<input type="password">

Only the text input is selected.


---

More Examples

Starts with

a[href^="https"] {
    color: green;
}

Ends with

img[src$=".png"] {
    border: 1px solid red;
}

Contains

a[href*="google"] {
    color: blue;
}


---

Q29. Descendant Selector

Selects elements inside another element, no matter how deeply nested.

HTML

<div>

<p>Hello</p>

</div>

CSS

div p {
    color: red;
}

Every <p> inside a <div> matches.


---

Q30. Child Selector

Selects only direct children.

HTML

<div>

<p>One</p>

<section>

<p>Two</p>

</section>

</div>

CSS

div > p {
    color: blue;
}

Only One becomes blue.


---

Difference

Descendant

div p

Matches

All nested paragraphs

Child

div > p

Matches

Direct child only


---

Q31. Adjacent Sibling Selector (+)

Selects the next sibling only.

HTML

<h1>Heading</h1>

<p>First</p>

<p>Second</p>

CSS

h1 + p {
    color: red;
}

Only First becomes red.


---

Q32. General Sibling Selector (~)

Selects all following siblings.

HTML

<h1></h1>

<p>One</p>

<p>Two</p>

<p>Three</p>

CSS

h1 ~ p {
    color: blue;
}

All three paragraphs become blue.


---

Q33. Pseudo-Class Selectors

Pseudo-classes style elements in a specific state.

Examples:

:hover

:focus

:active

:visited

:first-child

:last-child

:nth-child()

:not()


---

Q34. :hover

Applies styles when the mouse pointer is over an element.

button:hover {
    background: blue;
}


---

Q35. :focus

Styles an element when it receives keyboard or other focus.

input:focus {
    border: 2px solid blue;
}

Important for accessibility and keyboard users.


---

Q36. :active

Applies while an element is being activated (for example, while a mouse button is pressed).

button:active {
    background: red;
}


---

Q37. :first-child

Targets the first child element.

HTML

<ul>

<li>A</li>

<li>B</li>

<li>C</li>

</ul>

CSS

li:first-child {
    color: red;
}

Only A becomes red.


---

Q38. :last-child

li:last-child {
    color: green;
}

Only C becomes green.


---

Q39. :nth-child()

Selects elements based on position.

Example

li:nth-child(2) {
    color: blue;
}

Second item only.


---

Odd items

li:nth-child(odd)

Even items

li:nth-child(even)

Every third item

li:nth-child(3n)


---

Q40. :not()

Excludes matching elements.

Example

p:not(.note) {
    color: red;
}

All paragraphs except those with the note class become red.


---

Q41. Pseudo-Elements

Pseudo-elements style part of an element or generate content.

Examples

::before

::after

::first-letter

::first-line

::selection


---

Q42. ::before

Adds generated content before an element's content.

p::before {
    content: "★ ";
}

Output

★ Hello


---

Q43. ::after

p::after {
    content: " ✔";
}

Output

Hello ✔


---

Q44. ::first-letter

p::first-letter {
    font-size: 40px;
}

Commonly used for decorative drop caps.


---

Q45. ::first-line

p::first-line {
    color: red;
}

Only the first rendered line is styled.


---

Q46. What is CSS Specificity?

Specificity is the algorithm browsers use to decide which CSS rule wins when multiple rules target the same element.

Example

p {
    color: blue;
}

.text {
    color: red;
}

HTML

<p class="text">
Hello
</p>

Output

Red

The class selector is more specific than the element selector.


---

Q47. Specificity Order

From highest to lowest (ignoring !important):

Inline styles

↓

ID selectors

↓

Class, attribute selectors, pseudo-classes

↓

Element selectors, pseudo-elements

↓

Universal selector (*)


---

Q48. Specificity Example

#title {
    color: blue;
}

.heading {
    color: red;
}

h1 {
    color: green;
}

HTML

<h1
id="title"
class="heading">
Hello
</h1>

Final color:

Blue

Because the ID selector has higher specificity.


---

Q49. What is !important?

Example

p {
    color: red !important;
}

!important increases the priority of a declaration within the cascade.


---

Should You Use It?

Generally avoid it unless there is a specific reason, because it makes styles harder to override and maintain.


---

Q50. Frequently Asked Selector Interview Questions

1. Difference between id and class selectors?

id is intended to be unique.

class is reusable.



---

2. Difference between div p and div > p?

div p selects all descendant paragraphs.

div > p selects only direct child paragraphs.



---

3. Difference between + and ~?

+ selects the next adjacent sibling.

~ selects all following siblings.



---

4. Difference between pseudo-class and pseudo-element?

Pseudo-class	Pseudo-element

Styles an element's state	Styles part of an element or generated content
:hover	::before
:focus	::after
:nth-child()	::first-letter



---

5. What is specificity?

The algorithm that determines which CSS rule is applied when multiple rules match the same element.


---

6. Which is stronger: class or ID?

An ID selector has higher specificity than a class selector.


---

7. Is !important stronger than an ID selector?

Yes. Within the normal cascade, a declaration marked with !important takes precedence over non-!important declarations, regardless of selector specificity. If multiple competing declarations are all marked !important, specificity is then used to break the tie.


---

8. Why should !important be avoided?

Because it makes stylesheets harder to understand, override, and maintain.


---

9. What is the universal selector?

*

It matches every element.


---

10. What is the difference between :first-child and :first-of-type?

:first-child matches an element only if it is the first child of its parent.

:first-of-type matches the first element of its type among its siblings.


Example:

<div>
  <h2>Title</h2>
  <p>First paragraph</p>
  <p>Second paragraph</p>
</div>

p:first-child {
  color: red;      /* Doesn't match because <h2> is first */
}

p:first-of-type {
  color: blue;     /* Matches the first <p> */
}


---

Interview Coding Challenge

Question: Style every even row of a table with a light gray background.

tr:nth-child(even) {
    background-color: #f2f2f2;
}

This technique is commonly called zebra striping and improves readability.


---

What's Next?

In Part 3, we'll cover one of the most important CSS interview topics:

CSS Box Model

margin, padding, border, outline

box-sizing

display (block, inline, inline-block, none)

visibility

overflow

Width, height, min-width, max-width

Real interview scenarios and coding questions based on the Box Model.
