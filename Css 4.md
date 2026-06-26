Great — now we move into one of the most important (and most asked) CSS interview topics.

CSS Interview Guide – Part 4 (Positioning & Z-Index)

This topic is heavily tested because it directly affects layout behavior, UI layering, and real-world debugging.


---

Q71. What is CSS Positioning?

Answer

The position property defines how an element is placed in a document.

It controls:

Whether the element moves relative to itself or the page

Whether it is removed from normal flow

Whether it can overlap other elements



---

Position Values

static
relative
absolute
fixed
sticky


---

Q72. What is position: static?

Default behavior

Every element is static by default.

div {
    position: static;
}

Key Points

Follows normal document flow

top, left, right, bottom DO NOT work



---

Example

<div>Hello</div>

It appears in normal order.


---

Q73. What is position: relative?

Answer

Element stays in normal flow BUT can be shifted.

div {
    position: relative;
    top: 20px;
    left: 10px;
}


---

Step-by-step

1. Element is placed normally.


2. Then it is visually shifted.


3. Original space is still reserved.




---

Key Idea

👉 “Moves visually but keeps space”


---

Q74. What is position: absolute?

Answer

Element is removed from normal flow and positioned relative to the nearest positioned ancestor.


---

Example

<div class="parent">
    <div class="child">Box</div>
</div>

.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 10px;
    right: 10px;
}


---

Step-by-step

1. .parent becomes reference point.


2. .child is removed from normal flow.


3. .child is positioned inside .parent.




---

Key Idea

👉 “Absolute = taken out of flow + positioned inside nearest positioned parent”


---

Q75. What if no positioned parent exists?

Then it uses the viewport (page) as reference.


---

Q76. What is position: fixed?

Answer

Element is positioned relative to the viewport and does NOT move on scroll.


---

Example

div {
    position: fixed;
    top: 0;
}


---

Use cases

Sticky headers

Chat buttons

Floating navigation



---

Key Idea

👉 “Fixed = stays on screen always”


---

Q77. What is position: sticky?

Answer

Hybrid of relative and fixed.


---

Behavior

Acts like relative initially

Becomes fixed when scrolling reaches a threshold



---

Example

header {
    position: sticky;
    top: 0;
}


---

Use case

Sticky navbar

Table headers

Section titles



---

Key Idea

👉 “Sticky = relative until scroll threshold, then fixed”


---

Q78. Difference Between All Position Values

Position	Flow	Moves with scroll	Reference

static	normal	yes	none
relative	normal	yes	itself
absolute	removed	no	nearest positioned parent
fixed	removed	no	viewport
sticky	normal → fixed	partial	scroll container



---

Q79. What is Z-index?

Answer

z-index controls stacking order (depth) of elements.

Higher value = appears on top.


---

Example

.box1 {
    position: absolute;
    z-index: 1;
}

.box2 {
    position: absolute;
    z-index: 2;
}

Box2 appears above Box1.


---

Q80. Important Rule About Z-index

👉 z-index only works on positioned elements:

position must be:
relative / absolute / fixed / sticky


---

Q81. What is Stacking Context?

A stacking context is a layer system created by certain CSS properties.


---

It is created by:

position + z-index

opacity < 1

transform

flex / grid container

isolation: isolate



---

Example

.parent {
    position: relative;
    z-index: 1;
}

.child {
    position: relative;
    z-index: 9999;
}

If parent creates stacking context, child cannot escape it.


---

Key Idea

👉 “Z-index works inside a context, not globally”


---

Q82. Why z-index sometimes does NOT work?

Common reasons:

1. Element is not positioned


2. Parent has stacking context


3. Overflow clipping


4. Opacity or transform creates new context




---

Q83. Difference Between relative and absolute

Relative	Absolute

Stays in flow	Removed from flow
Space preserved	No space reserved
Moves from original position	Positioned independently



---

Q84. Difference Between fixed and sticky

Fixed	Sticky

Always fixed on screen	Activates on scroll
Relative to viewport	Relative to scroll container
Always visible	Conditional



---

Q85. How does top, left, right, bottom work?

They only work when:

position ≠ static


---

Example

div {
    position: absolute;
    top: 50px;
    left: 20px;
}


---

Q86. How to center a div using position?

Method 1 (absolute + transform)

div {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}


---

Why transform?

Because top/left move from corner, not center.


---

Q87. What is transform in positioning context?

It adjusts element visually without affecting layout.

Example:

transform: translate(-50%, -50%);

Used for centering and animations.


---

Q88. What happens when two elements overlap?

Browser uses:

1. z-index


2. stacking context


3. DOM order (if equal)




---

Q89. What is default stacking order?

background
↓
border
↓
content
↓
positioned elements
↓
z-index order


---

Q90. Common Positioning Interview Questions


---

1. Difference between relative and absolute?

Relative keeps space

Absolute removes from flow



---

2. Why is absolute positioned relative to parent?

Because the nearest positioned ancestor becomes reference.


---

3. Why is z-index not working?

Because:

No positioning

Parent stacking context

Overflow hidden

Transform applied



---

4. Difference between fixed and sticky?

Fixed always stays

Sticky activates on scroll



---

5. Can z-index be negative?

Yes.

It places element behind others.


---

6. What creates stacking context?

Opacity, transform, position + z-index, etc.


---

7. Why is sticky not working?

Common reasons:

Missing top

Parent overflow hidden

Incorrect container



---

Coding Challenge

Sticky Navbar

<nav class="navbar">Navbar</nav>

<div class="content">Scroll Content</div>

.navbar {
    position: sticky;
    top: 0;
    background: black;
    color: white;
    padding: 10px;
}


---

Interview Insight

Interviewers often ask:

“Why is my element overlapping incorrectly?”

“Why is z-index not working?”

“Explain stacking context with real example”

“Difference between fixed and sticky in UI scenarios”



---

What’s Next?

In Part 5, we move to one of the MOST IMPORTANT topics in CSS interviews:

👉 Flexbox (Deep Dive)

We will cover:

Flex container vs flex items

main axis vs cross axis

justify-content vs align-items

flex-grow, shrink, basis

flex shorthand

centering techniques

real UI layouts

50+ interview questions + coding challenges


Just say “Next” 👍
