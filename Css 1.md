Excellent choice. Most frontend interviews start with HTML, then move immediately into CSS. We'll cover CSS with the same depth as the HTML series.

Complete CSS Interview Roadmap

We'll cover CSS in 10 parts:

1. CSS Basics (30+ Questions)


2. Selectors & Specificity (30+ Questions)


3. Box Model & Display (40+ Questions)


4. Positioning & Z-index (35+ Questions)


5. Flexbox (50+ Questions)


6. CSS Grid (40+ Questions)


7. Responsive Design & Media Queries (35+ Questions)


8. Animations, Transitions & Transform (40+ Questions)


9. Advanced CSS (Variables, BEM, Performance, Pseudo-elements, etc.)


10. Company Interview Questions, Coding Challenges & Tricky Questions




---

CSS Interview Guide – Part 1 (CSS Basics)


---

Q1. What is CSS?

Answer

CSS stands for Cascading Style Sheets.

It is used to control the presentation of HTML documents, including:

Colors

Fonts

Spacing

Layout

Animations

Responsive design


Think of it this way:

HTML defines the structure.

CSS controls the appearance.

JavaScript adds behavior.



---

Example

HTML

<h1>Hello World</h1>

CSS

h1 {
    color: blue;
}

Output

Hello World (Blue)


---

Step-by-Step Explanation

Step 1: HTML creates the heading.

Step 2: CSS selects the <h1> element.

Step 3: The color property changes the text color to blue.


---

Q2. Why do we use CSS?

Without CSS:

Simple HTML page
↓
Default browser styles
↓
Basic appearance

With CSS:

HTML
↓

CSS Styling

↓

Professional UI

Benefits

Separates content from presentation

Reusable styles

Easier maintenance

Better consistency

Responsive layouts

Improved user experience



---

Q3. What are the different ways to apply CSS?

There are three ways.

1. Inline CSS

<h1 style="color:red;">
Hello
</h1>

Advantages

Quick changes

Useful for testing


Disadvantages

Hard to maintain

Repeats styles

Not recommended for larger projects



---

2. Internal CSS

<style>
h1{
    color:blue;
}
</style>

Placed inside the <head> element.

Useful for small pages or demos.


---

3. External CSS

HTML

<link rel="stylesheet"
href="style.css">

style.css

h1{
    color:green;
}

Advantages

Reusable

Cleaner code

Easier maintenance

Best practice for most projects



---

Interview Question

Which CSS method is best?

Answer:

External CSS, because it promotes reuse, maintainability, and separation of concerns.


---

Q4. What is CSS Syntax?

Basic syntax:

selector {
    property: value;
}

Example:

p{
    color:red;
}

Breakdown

p          → Selector

color      → Property

red        → Value

;          → Ends declaration


---

Q5. What is a Selector?

A selector tells CSS which HTML elements to style.

Example

h1{
    color:blue;
}

Here:

h1

is the selector.


---

Q6. What are CSS Properties?

Properties define what should change.

Examples:

color

background

font-size

margin

padding

width

height

border

display

position


---

Q7. What are CSS Values?

Values specify how a property should be applied.

Example

color: blue;

Property:

color

Value:

blue


---

Q8. What is the Cascade in CSS?

The word Cascading means that when multiple CSS rules target the same element, the browser decides which rule wins based on the cascade.

The browser considers several factors, including:

1. Importance (!important)


2. Origin (browser, user, author styles)


3. Specificity


4. Source order (later rules can win when specificity is equal)



Example

h1{
    color:red;
}

h1{
    color:blue;
}

Output:

Blue

Because both rules have equal specificity, the later one wins.


---

Q9. What is Inheritance?

Some CSS properties are inherited from parent elements by default.

Example

<div>

<p>Hello</p>

</div>

div{
    color:red;
}

Output

Hello (Red)

The <p> inherits the text color.


---

Common Inherited Properties

color

font-family

font-size (unless overridden)

line-height

text-align



---

Non-Inherited Properties

margin

padding

border

width

height



---

Q10. What is the Difference Between HTML Attributes and CSS Properties?

HTML

<img
src="cat.jpg"
alt="Cat">

Attributes:

src

alt

CSS

img{
    width:200px;
}

Property:

width


---

Comparison

HTML Attribute	CSS Property

Defines element information	Defines presentation
Written in HTML	Written in CSS
Example: src, href, alt	Example: color, margin, padding



---

Q11. What are CSS Comments?

Single-line or multi-line comments:

/* This is a comment */

h1{
    color:red;
}

Comments are ignored by the browser.


---

Q12. What is the Difference Between CSS2 and CSS3?

CSS2	CSS3

Monolithic specification	Modular specifications
Limited visual effects	Animations, transitions, transforms
No Flexbox/Grid	Modern layout systems
Limited selectors	More powerful selectors



---

Q13. What are CSS Units?

Absolute Units

px

cm

mm

in

pt

Example

font-size:16px;


---

Relative Units

%

em

rem

vw

vh

vmin

vmax

Example

width:50%;


---

Interview Tip

For responsive design, relative units are often preferred over fixed units where appropriate.


---

Q14. Difference Between em and rem

em

Relative to the font size of the current element (or inherited font size).

font-size:2em;


---

rem

Relative to the root (<html>) font size.

font-size:2rem;


---

Example

html{
    font-size:16px;
}

Then:

2rem = 32px


---

Comparison

em	rem

Relative to current context	Relative to root element
Can compound in nested elements	More predictable



---

Q15. Difference Between px and %

px

Fixed unit.

width:200px;


---

%

Relative to the containing element.

width:50%;


---

Comparison

px	%

Fixed	Relative
Predictable	Flexible



---

Q16. What is the color Property?

Changes text color.

h1{
    color:red;
}


---

Q17. What is the background-color Property?

Changes background color.

body{
    background-color:lightblue;
}


---

Q18. What is the Difference Between color and background-color?

color:red;

Changes text.

background-color:yellow;

Changes the background.


---

Q19. How Can Colors Be Specified in CSS?

Color Name

color:red;


---

Hex

color:#ff0000;


---

RGB

color:rgb(255,0,0);


---

RGBA

color:rgba(255,0,0,0.5);

The last value controls opacity.


---

HSL

color:hsl(0,100%,50%);


---

HSLA

color:hsla(0,100%,50%,0.5);


---

Q20. Frequently Asked CSS Basics Questions

1. What does CSS stand for?

Cascading Style Sheets


---

2. Why do we use CSS?

To control the presentation and layout of HTML documents.


---

3. Which CSS method is best?

External CSS.


---

4. What is a selector?

A pattern used to target HTML elements.


---

5. What is a property?

The aspect of the element you want to style.


---

6. What is a value?

The setting assigned to a property.


---

7. What is inheritance?

Some properties automatically inherit values from their parent elements.


---

8. What is the cascade?

The process the browser uses to resolve conflicting CSS rules.


---

9. Difference between em and rem?

em: relative to the current element's font size.

rem: relative to the root element's font size.



---

10. Difference between px and %?

px: fixed unit.

%: relative unit.



---

Interview Tips for CSS Basics

Interviewers often ask follow-up questions like:

Why is external CSS preferred?

What is the difference between inheritance and the cascade?

When would you choose rem instead of em?

Why are relative units useful in responsive design?

Which CSS properties inherit by default?



---

What's Next?

In Part 2, we'll cover one of the most important interview topics:

CSS Selectors (Element, Class, ID, Universal, Grouping)

Attribute Selectors

Combinators

Pseudo-classes (:hover, :focus, :nth-child, etc.)

Pseudo-elements (::before, ::after)

CSS Specificity (a favorite interview topic)

The Cascade in depth

!important and when to avoid it

50+ selector-based interview questions with detailed explanations.
