Great — now we’re moving into the most powerful CSS layout system: CSS Grid. If Flexbox is for components, Grid is for entire page layouts.


---

CSS Interview Guide – Part 6 (CSS Grid – Deep Dive)


---

Q111. What is CSS Grid?

Answer

CSS Grid is a 2-dimensional layout system used to design web layouts in:

Rows

Columns


Unlike Flexbox (1D), Grid handles both directions at the same time.


---

Basic Example

.container {
    display: grid;
}


---

Key Idea

Flexbox → 1D (row OR column)
Grid    → 2D (row AND column)


---

Q112. What are Grid Container and Grid Items?

Grid Container

The parent element:

.container {
    display: grid;
}

Grid Items

Direct children of the container.


---

Q113. What is grid-template-columns?

Defines number and size of columns.


---

Example

.container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
}


---

Result

| 200px | 200px | 200px |


---

Q114. What is grid-template-rows?

Defines row structure.

.container {
    grid-template-rows: 100px 100px;
}


---

Q115. What is the fr unit?

Answer

fr = fraction of available space.


---

Example

grid-template-columns: 1fr 2fr;


---

Meaning

Total space = 3 parts

1fr = 1 part
2fr = 2 parts

So second column is twice as wide.


---

Q116. Why is Grid better than Flexbox for layouts?

Feature	Grid	Flexbox

Direction	2D	1D
Layout control	Rows + Columns	Row OR Column
Page layout	Best	Not ideal
Component layout	OK	Best



---

Q117. What is gap in Grid?

Adds spacing between rows and columns.

.container {
    display: grid;
    gap: 20px;
}


---

Advantage

No need for margin hacks

Cleaner layout spacing



---

Q118. What is grid-column?

Used to control horizontal span.


---

Example

.item {
    grid-column: 1 / 3;
}


---

Meaning

Start at column 1 → end at column 3


---

Q119. What is grid-row?

Controls vertical span.

.item {
    grid-row: 1 / 3;
}


---

Q120. What is grid-area?

Shorthand for row + column placement.

.item {
    grid-area: 1 / 1 / 3 / 3;
}


---

Order

row-start / column-start / row-end / column-end


---

Q121. What is repeat() in Grid?

Used to avoid repetition.


---

Example

grid-template-columns: repeat(3, 1fr);


---

Equivalent to:

1fr 1fr 1fr


---

Q122. What is minmax()?

Defines minimum and maximum size.


---

Example

grid-template-columns: minmax(200px, 1fr);


---

Meaning

Minimum: 200px

Maximum: flexible (1fr)



---

Q123. What is auto-fit vs auto-fill?

This is a very common interview question.


---

auto-fill

Fills the row with as many columns as possible, even if empty.

grid-template-columns: repeat(auto-fill, 200px);


---

auto-fit

Collapses empty tracks and expands items.

grid-template-columns: repeat(auto-fit, 200px);


---

Key Difference

auto-fill	auto-fit

Keeps empty spaces	Removes empty spaces
Fixed layout	Flexible layout



---

Q124. What is grid-auto-rows?

Defines default row height.

grid-auto-rows: 150px;


---

Q125. What is grid-auto-columns?

Defines default column size for implicit grids.


---

Q126. What is implicit vs explicit grid?

Explicit Grid

Defined manually:

grid-template-columns: 1fr 1fr;


---

Implicit Grid

Created automatically when items overflow.


---

Q127. What is justify-items?

Aligns items horizontally inside their cell.

justify-items: center;


---

Q128. What is align-items in Grid?

Aligns items vertically inside grid cells.

align-items: center;


---

Q129. Difference between justify-content and justify-items

Property	Meaning

justify-content	Aligns whole grid
justify-items	Aligns items inside cells



---

Q130. What is place-items?

Shortcut for:

align-items + justify-items

Example:

place-items: center;


---

Q131. What is place-content?

Controls alignment of the entire grid.


---

Q132. What is grid-template-areas?

Allows naming layout regions.


---

Example

.container {
    display: grid;
    grid-template-areas:
        "header header"
        "sidebar main"
        "footer footer";
}


---

Assign areas

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }


---

Q133. Why is grid-template-areas useful?

Easy visualization

Cleaner layout structure

Better readability



---

Q134. How to center a div using Grid?

.container {
    display: grid;
    place-items: center;
    height: 100vh;
}


---

Q135. Grid vs Flexbox (Interview Favorite)

Feature	Grid	Flexbox

Direction	2D	1D
Layout type	Page layout	Component layout
Control	Rows + columns	Single axis
Complexity	High	Low



---

Q136. Common Grid Interview Mistakes

1. Using Grid for everything

Grid is not always needed for simple components.


---

2. Confusing auto-fit vs auto-fill

Very frequently asked.


---

3. Not understanding implicit grid

Extra items create unexpected rows/columns.


---

4. Misusing fr unit

fr is not fixed size — it's flexible space.


---

Q137. Real-world Grid Use Cases

Dashboard layouts

Image galleries

Product listings

Page structure (header/sidebar/footer)

Complex UI layouts



---

Q138. Interview Questions (CSS Grid)


---

1. What is CSS Grid?

A 2D layout system for rows and columns.


---

2. Difference between Grid and Flexbox?

Grid = 2D, Flexbox = 1D.


---

3. What is fr unit?

Fraction of available space.


---

4. What is auto-fit?

Removes empty grid tracks.


---

5. What is minmax()?

Defines min and max size of a grid track.


---

6. What is grid-template-areas?

Named layout system for grids.


---

7. What is implicit grid?

Automatically created rows/columns when content overflows.


---

8. What is gap?

Spacing between grid items.


---

9. How to center using Grid?

Use place-items: center.


---

10. When should you use Grid?

When designing full page layouts or complex 2D structures.


---

Coding Challenge

Responsive Grid Layout

<div class="grid">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</div>

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 20px;
}


---

Why this is powerful

Responsive

No media queries needed

Automatically adjusts layout



---

What’s Next?

In Part 7, we’ll cover:

👉 Responsive Design & Media Queries

We will go deep into:

Media queries

Mobile-first vs desktop-first

Breakpoints

Responsive units (vw, vh, rem, %)

Responsive images

Fluid layouts

Container queries

Real interview problems + UI challenges


Just say “Next” 👍
