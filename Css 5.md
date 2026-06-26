Great — now we’re getting into one of the most important CSS interview topics ever.

CSS Interview Guide – Part 5 (Flexbox – Deep Dive)

Flexbox is heavily used in real UI layouts and is a favorite in interviews for frontend roles.


---

Q91. What is Flexbox?

Answer

Flexbox (Flexible Box Layout) is a CSS layout system designed to:

Align items easily

Distribute space dynamically

Build responsive layouts without float or positioning hacks



---

Basic idea

Flex Container
    ↓
Flex Items arranged in a row or column


---

Example

.container {
    display: flex;
}


---

Q92. What are the two parts of Flexbox?

1. Flex Container

The parent element:

.container {
    display: flex;
}

2. Flex Items

The children inside the container.


---

Q93. What is Main Axis and Cross Axis?

This is VERY important in interviews.


---

Default direction

row (default)
→ Main Axis (horizontal)
↓ Cross Axis (vertical)


---

If flex-direction: column

column
↓ Main Axis (vertical)
→ Cross Axis (horizontal)


---

Key Idea

👉 Flexbox ALWAYS has:

Main axis (direction of flow)

Cross axis (perpendicular direction)



---

Q94. What is flex-direction?

Controls direction of items.

.container {
    display: flex;
    flex-direction: row;
}


---

Values

Value	Meaning

row	left → right
row-reverse	right → left
column	top → bottom
column-reverse	bottom → top



---

Example

flex-direction: column;

Items stack vertically.


---

Q95. What is justify-content?

Answer

Aligns items along the main axis.


---

Example

.container {
    display: flex;
    justify-content: center;
}


---

Values

Value	Meaning

flex-start	start of axis
flex-end	end of axis
center	center
space-between	equal space between items
space-around	space around items
space-evenly	equal space everywhere



---

Visualization

space-between:

[Item]   [Item]   [Item]


---

Q96. What is align-items?

Answer

Aligns items along the cross axis.


---

Example

.container {
    display: flex;
    align-items: center;
}


---

Values

Value	Meaning

stretch	default
flex-start	top
flex-end	bottom
center	center alignment
baseline	text baseline alignment



---

Q97. Difference Between justify-content and align-items

Property	Axis	Purpose

justify-content	main axis	horizontal alignment (row)
align-items	cross axis	vertical alignment



---

Trick to remember

👉 Justify = main
👉 Align = cross


---

Q98. What is align-self?

Answer

Overrides align-items for a single item.

.item {
    align-self: flex-end;
}


---

Use case

When one item needs special positioning.


---

Q99. What is flex-wrap?

Answer

Controls whether items wrap onto new lines.


---

Example

.container {
    display: flex;
    flex-wrap: wrap;
}


---

Values

Value	Meaning

nowrap	default, single line
wrap	items move to next line
wrap-reverse	reverse wrapping



---

Q100. What is flex-grow?

Answer

Defines how much an item can expand.


---

Example

.item {
    flex-grow: 1;
}


---

Meaning

If space is available:

Items grow proportionally



---

Example scenario

Item1 flex-grow: 1
Item2 flex-grow: 2

Item2 grows twice as much.


---

Q101. What is flex-shrink?

Answer

Defines how items shrink when space is limited.

.item {
    flex-shrink: 1;
}


---

Key idea

👉 Controls compression behavior.


---

Q102. What is flex-basis?

Answer

Defines the initial size of a flex item.

.item {
    flex-basis: 200px;
}


---

Priority order

flex-basis
→ width (if flex-basis not set)


---

Q103. What is flex shorthand?

Answer

Combines:

flex-grow
flex-shrink
flex-basis


---

Example

.item {
    flex: 1 1 200px;
}


---

Common shortcut

flex: 1;

Means:

flex-grow: 1;
flex-shrink: 1;
flex-basis: 0;


---

Q104. How to center a div using Flexbox?

Answer

.container {
    display: flex;
    justify-content: center;
    align-items: center;
}


---

Explanation

Horizontal center → justify-content

Vertical center → align-items



---

Q105. What is gap in Flexbox?

Answer

Defines spacing between flex items.

.container {
    display: flex;
    gap: 20px;
}


---

Advantage

No need for margin hacks

Cleaner layout



---

Q106. What happens without Flexbox?

Before Flexbox:

float layouts

positioning hacks

inline-block spacing issues


Flexbox solves all of these.


---

Q107. Flexbox vs Grid (Interview Favorite)

Flexbox	Grid

One-dimensional	Two-dimensional
Row OR column	Rows AND columns
Best for components	Best for layouts



---

Q108. Common Flexbox Interview Mistakes

1. Confusing axes

justify-content ≠ vertical always

align-items ≠ horizontal always



---

2. Not setting display:flex

Flex properties won’t work.


---

3. Expecting margin:auto behavior in all cases

Flexbox has its own alignment system.


---

4. Forgetting default direction is row


---

Q109. Real UI Use Cases

Flexbox is used for:

Navbar layouts

Card alignment

Centering elements

Button groups

Equal height columns

Responsive layouts



---

Q110. Interview Questions (Flexbox)


---

1. What is Flexbox?

A layout system for aligning items in rows or columns efficiently.


---

2. Difference between justify-content and align-items?

justify-content → main axis

align-items → cross axis



---

3. What is flex-grow?

Controls how much space an item takes when extra space is available.


---

4. What is flex-shrink?

Controls how items shrink when space is limited.


---

5. What is flex-basis?

Initial size of a flex item before distribution.


---

6. Difference between Flexbox and Grid?

Flexbox: 1D layout

Grid: 2D layout



---

7. How do you center a div using Flexbox?

Use justify-content and align-items center.


---

8. What is gap?

Spacing between flex items without using margin.


---

9. What happens if flex-wrap is not set?

Items will overflow in a single line.


---

10. Why is Flexbox preferred?

Because it simplifies alignment and responsive design.


---

Coding Challenge

Create a Centered Card Layout

<div class="container">
    <div class="card">Hello Flexbox</div>
</div>

.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.card {
    padding: 20px;
    background: lightblue;
}


---

What’s Next?

In Part 6, we move to another critical topic:

👉 CSS Grid (Advanced Layout System)

We will cover:

Grid container vs items

grid-template-columns / rows

fr unit

gap

auto-fit vs auto-fill

grid-area

responsive layouts

real-world UI patterns

50+ interview questions + coding problems


Just say “Next” 👍
