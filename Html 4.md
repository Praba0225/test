HTML Interview Guide – Part 4 (Tables, Lists, Multimedia, Iframes, Canvas, SVG & HTML5 APIs)

This section covers intermediate to advanced HTML interview topics that are frequently asked in frontend interviews.


---

Q61. What are HTML Lists?

Answer

Lists are used to display related items in an organized way.

HTML provides three types of lists:

Ordered List (<ol>)

Unordered List (<ul>)

Description List (<dl>)



---

Q62. What is an Ordered List (<ol>)?

An ordered list displays items in a numbered sequence.

Example

<ol>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ol>

Output

1. HTML
2. CSS
3. JavaScript

Step-by-Step

<ol>  → Ordered List

<li>  → List Item

</ol> → End List


---

Interview Question

When should you use <ol>?

Use it when order matters, such as:

Recipe steps

Installation instructions

Rankings

Algorithms



---

Q63. What is an Unordered List (<ul>)?

Displays items with bullets.

Example

<ul>
    <li>Apple</li>
    <li>Mango</li>
    <li>Orange</li>
</ul>

Output

• Apple

• Mango

• Orange


---

When to use?

Whenever sequence doesn't matter.

Examples

Menu

Features

Shopping list



---

Q64. What is a Description List (<dl>)?

Used for terms and descriptions.

Example

<dl>

<dt>HTML</dt>

<dd>Markup Language</dd>

<dt>CSS</dt>

<dd>Styling Language</dd>

</dl>

Output

HTML
   Markup Language

CSS
   Styling Language


---

Q65. What are HTML Tables?

Tables display data in rows and columns.

Example

<table>

<tr>

<th>Name</th>

<th>Age</th>

</tr>

<tr>

<td>John</td>

<td>22</td>

</tr>

</table>

Output

-------------------

Name     Age

John      22

-------------------


---

Table Structure

table

│

├── tr

│     ├── th

│     └── th

│

└── tr

      ├── td

      └── td


---

Q66. Explain Table Tags

Tag	Purpose

<table>	Creates table
<tr>	Table row
<th>	Header cell
<td>	Data cell
<caption>	Table title
<thead>	Header section
<tbody>	Body section
<tfoot>	Footer section



---

Complete Example

<table>

<caption>
Student Marks
</caption>

<thead>

<tr>

<th>Name</th>

<th>Marks</th>

</tr>

</thead>

<tbody>

<tr>

<td>Rahul</td>

<td>95</td>

</tr>

</tbody>

</table>


---

Why use <thead>, <tbody>, <tfoot>?

Benefits:

Better readability

Better accessibility

Easier styling

Clear document structure



---

Q67. Difference Between <th> and <td>

<th>	<td>

Header cell	Data cell
Bold by default	Normal text by default
Typically centered by default	Typically left-aligned by default (browser defaults vary)



---

Q68. What are rowspan and colspan?

rowspan

Merges rows.

Example

<td rowspan="2">
A
</td>

Output

A | B

  | C


---

colspan

Merges columns.

<td colspan="2">
Total
</td>

Output

Total

A     B


---

Q69. What is an HTML iframe?

An iframe embeds another webpage within the current webpage.

Example

<iframe
src="https://example.com"
width="500"
height="300">
</iframe>


---

Uses

Google Maps

YouTube videos

Documents

External pages



---

Interview Question

Can we embed every website inside an iframe?

No.

Many websites prevent embedding using HTTP headers such as X-Frame-Options or the Content-Security-Policy frame-ancestors directive.


---

Q70. Explain HTML Audio

Example

<audio controls>

<source
src="song.mp3"
type="audio/mpeg">

</audio>


---

Controls

▶ Play

⏸ Pause

🔊 Volume


---

Attributes

Attribute	Purpose

controls	Shows audio controls
autoplay	Starts automatically (subject to browser policies)
loop	Repeats playback
muted	Starts muted
preload	Hints how much media to preload



---

Q71. Explain HTML Video

Example

<video
width="400"
controls>

<source
src="movie.mp4"
type="video/mp4">

</video>


---

Attributes

controls

autoplay

loop

muted

poster

preload


---

Interview Tip

Modern browsers often block autoplay with sound. Autoplay is more likely to work when the video is muted.


---

Q72. Difference Between Audio and Video Tags

Audio	Video

Plays sound	Plays sound and video
No visuals	Displays visuals
<audio>	<video>



---

Q73. What is SVG?

SVG stands for Scalable Vector Graphics.

SVG is an XML-based format for vector graphics.

Example

<svg
width="200"
height="100">

<circle
cx="50"
cy="50"
r="40"
fill="red"/>

</svg>


---

Benefits

Scales without losing quality

Small file size for simple graphics

Can be styled with CSS

Can be manipulated using JavaScript



---

SVG vs Image

SVG	PNG/JPG

Vector	Raster
Scalable	May lose quality when enlarged
Editable	Not easily editable
Great for icons and logos	Better for photographs



---

Q74. What is Canvas?

Canvas provides a drawing surface for graphics using JavaScript.

Example

<canvas
id="myCanvas"
width="200"
height="100">
</canvas>

JavaScript is then used to draw on it.


---

Uses

Games

Charts

Drawing applications

Animations



---

Q75. Difference Between SVG and Canvas

SVG	Canvas

Vector graphics	Pixel-based drawing
Elements remain part of the DOM	Drawn pixels are not individual DOM elements
Easier to manipulate individual shapes	Better for many rapidly changing graphics
Better for icons	Better for games and complex animations



---

Q76. What are HTML Entities?

Special character codes.

Example

&lt;

Output

<

More examples

&amp;

&nbsp;

&gt;

&copy;

&quot;


---

Q77. What is Local Storage?

Stores data in the browser.

JavaScript example:

localStorage.setItem("name","John");

Retrieve:

localStorage.getItem("name");


---

Features

Persists until cleared

Around 5–10 MB depending on the browser

Same-origin access

Not sent with HTTP requests



---

Q78. What is Session Storage?

Similar to Local Storage.

Difference:

Data exists only while the browser tab remains open.


---

Q79. Difference Between Local Storage and Session Storage

Local Storage	Session Storage

Persists until cleared	Cleared when the tab/session ends
Shared across tabs of the same origin (browser behavior)	Limited to a single tab/session
Same-origin	Same-origin



---

Q80. Difference Between Cookies, Local Storage and Session Storage

Cookies	Local Storage	Session Storage

Small storage (around 4 KB per cookie)	Larger storage	Larger storage
Can be sent with HTTP requests	Not sent automatically	Not sent automatically
Can have expiration dates	No built-in expiration	Ends with the tab/session
Commonly used for sessions and preferences	Persistent client-side data	Temporary client-side data



---

Frequently Asked Interview Questions

1. Difference between SVG and Canvas?

Answer:

SVG is vector-based and ideal for icons, logos, and diagrams.

Canvas is pixel-based and better for games and complex animations.


---

2. When should you use Tables?

Only for tabular data, such as reports, schedules, or financial records—not for page layout.


---

3. Difference between <thead> and <tbody>?

<thead> contains header rows.

<tbody> contains the main table data.


---

4. Can every website be embedded in an iframe?

No. Many websites explicitly block embedding for security reasons.


---

5. Difference between Local Storage and Cookies?

Local Storage:

More storage

Not sent with requests

Good for client-side data


Cookies:

Smaller

Can be sent with every request to the matching domain/path

Often used for authentication and session management



---

6. Can JavaScript access Local Storage?

Yes, through the localStorage API.


---

7. Which is better for a company logo—SVG or PNG?

SVG, because it scales cleanly without losing quality.


---

8. Why shouldn't tables be used for page layout?

Because semantic layout elements and CSS provide more accessible, maintainable, and responsive layouts. Tables should represent tabular data only.


---

Interview Coding Challenge

Question: Create a student marks table with a header, body, and footer.

Answer:

<table border="1">
    <caption>Student Marks</caption>

    <thead>
        <tr>
            <th>Name</th>
            <th>Marks</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>Alice</td>
            <td>92</td>
        </tr>
        <tr>
            <td>Bob</td>
            <td>88</td>
        </tr>
    </tbody>

    <tfoot>
        <tr>
            <td>Average</td>
            <td>90</td>
        </tr>
    </tfoot>
</table>


---

What's Next?

Part 5 will cover Advanced HTML Interview Questions, including:

HTML5 APIs (Geolocation, Drag & Drop, Web Workers)

Web Components

Progressive enhancement

Performance optimization

Browser rendering basics

DOM concepts

Advanced scenario-based questions

Tricky interview questions asked in companies like TCS, Infosys, Accenture, Capgemini, Cognizant, IBM, Amazon, Microsoft, and Google.
