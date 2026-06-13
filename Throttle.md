Throttle in JavaScript is a technique used to limit how often a function can run within a specified time interval.

It's commonly used when handling events that fire very frequently, such as:

scroll

resize

mousemove

keydown


Without throttling, these events can trigger hundreds of times per second and hurt performance.


---

Step 1: Understand the Problem

Imagine a user is scrolling a page.

window.addEventListener("scroll", () => {
    console.log("Scrolling...");
});

While scrolling, this callback may execute hundreds of times every second.

This can become expensive if the callback:

Makes API calls

Updates the DOM

Performs calculations



---

Step 2: What Throttling Does

Suppose we throttle a function with a delay of 1000 ms (1 second).

Even if the event fires 100 times during that second, the function will execute only once every second.

Visualization

Without throttle:

Event:   ●●●●●●●●●●●●●●●●●●●●
Function:●●●●●●●●●●●●●●●●●●●●

With throttle (1 second):

Event:   ●●●●●●●●●●●●●●●●●●●●
Function:●---------●---------●


---

Step 3: Basic Throttle Implementation

function throttle(func, delay) {
    let lastCall = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;
            func.apply(this, args);
        }
    };
}


---

Step 4: How It Works

Initial State

lastCall = 0

First Call

now = 1000

Check:

1000 - 0 >= 1000

True ✅

Function executes.

lastCall = 1000


---

Second Call After 300ms

now = 1300

Check:

1300 - 1000 >= 1000

False ❌

Function does not execute.


---

Third Call After 1100ms

now = 2100

Check:

2100 - 1000 >= 1000

True ✅

Function executes again.


---

Step 5: Example Usage

function handleScroll() {
    console.log("Scroll event processed");
}

const throttledScroll = throttle(handleScroll, 1000);

window.addEventListener("scroll", throttledScroll);

Now the handler runs at most once every second.


---

Step 6: Real-World Example

Without Throttle

window.addEventListener("resize", () => {
    console.log(window.innerWidth);
});

Dragging the browser edge fires this continuously.

With Throttle

window.addEventListener(
    "resize",
    throttle(() => {
        console.log(window.innerWidth);
    }, 500)
);

Output updates only twice per second.


---

Step 7: Throttle with Leading Execution

A "leading" throttle executes immediately when the first event occurs.

function throttle(func, delay) {
    let waiting = false;

    return function (...args) {
        if (!waiting) {
            func.apply(this, args);

            waiting = true;

            setTimeout(() => {
                waiting = false;
            }, delay);
        }
    };
}

Behavior:

Event:    ●●●●●●●●●●●●●●
Function: ●-------●-------●

The first call happens instantly.


---

Step 8: Throttle with Trailing Execution

Sometimes you want the last event to run after the delay.

Example:

function throttle(func, delay) {
    let timeout = null;

    return function (...args) {
        if (!timeout) {
            timeout = setTimeout(() => {
                func.apply(this, args);
                timeout = null;
            }, delay);
        }
    };
}

This executes after the delay period ends.


---

Step 9: Throttle vs Debounce

These concepts are often confused.

Throttle

Runs at a fixed rate.

Events:    ●●●●●●●●●●●●●●●
Throttle:  ●----●----●----●

Use for:

Scroll tracking

Mouse movement

Window resize monitoring

Game loops



---

Debounce

Waits until events stop.

Events:    ●●●●●●●●●●●●●●●
Debounce:                ●

Use for:

Search input

Form validation

Auto-save

API requests after typing


Example:

searchBox.addEventListener(
    "input",
    debounce(search, 500)
);

Search runs only after the user stops typing for 500 ms.


---

Step 10: Practical Interview Question

Implement throttle

function throttle(fn, delay) {
    let lastExecution = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastExecution >= delay) {
            lastExecution = now;
            fn.apply(this, args);
        }
    };
}

Usage:

const throttledLog = throttle(() => {
    console.log("Executed");
}, 1000);

setInterval(throttledLog, 100);

Although throttledLog is called every 100 ms, "Executed" appears only once every second.


---

Summary

Throttle ensures a function runs at most once within a specified time interval.

Key points:

1. It improves performance for frequently fired events.


2. Commonly used with scroll, resize, and mousemove.


3. It limits execution frequency rather than preventing execution completely.


4. Unlike debounce, throttle guarantees periodic execution while events continue.


5. A common implementation tracks the last execution time and ignores calls made too soon afterward.



A simple mental model is:

> Throttle = "Run this function at most once every X milliseconds, no matter how many times it is triggered."
