A closure in JavaScript is one of the most important concepts to understand because it explains how functions can "remember" variables from their surrounding scope even after that outer function has finished executing.

Let's build the concept step by step.

Step 1: Understand Scope

A variable's scope determines where it can be accessed.

let globalVar = "I'm global";

function test() {
  let localVar = "I'm local";
  console.log(globalVar); // Accessible
  console.log(localVar);  // Accessible
}

test();

console.log(globalVar); // Accessible
// console.log(localVar); // Error

Here:

globalVar is accessible everywhere.

localVar exists only inside test().



---

Step 2: Functions Can Access Outer Variables

JavaScript uses lexical scope.

function outer() {
  let message = "Hello";

  function inner() {
    console.log(message);
  }

  inner();
}

outer();

Output:

Hello

inner() can access message because it was defined inside outer().


---

Step 3: Returning a Function

Now let's return the inner function.

function outer() {
  let message = "Hello";

  function inner() {
    console.log(message);
  }

  return inner;
}

const fn = outer();
fn();

Output:

Hello

At first this seems strange.

After outer() finishes, you might expect message to disappear.

Yet fn() still prints "Hello".

Why?

This is where closures come in.


---

Step 4: What Exactly Is a Closure?

A closure is:

> A function bundled together with references to the variables from its surrounding lexical scope.



In simple words:

> The function remembers the variables that existed when it was created.



In the previous example:

const fn = outer();

fn doesn't just contain code.

It also remembers:

message = "Hello"

This remembered environment is the closure.


---

Step 5: Visualizing the Closure

When outer() runs:

outer()

Memory looks like:

outer scope
 └── message = "Hello"

When inner is returned:

return inner;

JavaScript keeps message alive because inner still needs it.

fn
 ├── function code
 └── remembers:
      message = "Hello"

Even though outer() has completed.


---

Step 6: Real Example – Counter

Closures are commonly used to maintain private state.

function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter());
console.log(counter());
console.log(counter());

Output:

1
2
3

What happens?

First call:

count = 0
count++

Returns:

1

Second call:

count = 1
count++

Returns:

2

The variable count stays alive because of the closure.


---

Step 7: Independent Closures

Each call creates a separate closure.

function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counterA = createCounter();
const counterB = createCounter();

console.log(counterA());
console.log(counterA());

console.log(counterB());
console.log(counterB());

Output:

1
2
1
2

Each counter has its own private count.


---

Step 8: Closures with Parameters

function multiplyBy(multiplier) {
  return function (num) {
    return num * multiplier;
  };
}

const double = multiplyBy(2);
const triple = multiplyBy(3);

console.log(double(5));
console.log(triple(5));

Output:

10
15

double remembers:

multiplier = 2

triple remembers:

multiplier = 3


---

Step 9: Data Privacy Using Closures

Before JavaScript had private class fields, closures were commonly used for encapsulation.

function createBankAccount() {
  let balance = 1000;

  return {
    deposit(amount) {
      balance += amount;
    },

    getBalance() {
      return balance;
    }
  };
}

const account = createBankAccount();

account.deposit(500);

console.log(account.getBalance());

Output:

1500

Trying:

console.log(account.balance);

Returns:

undefined

The variable balance is private.


---

Step 10: Closures in Event Handlers

function setupButton() {
  let clicks = 0;

  document
    .getElementById("btn")
    .addEventListener("click", function () {
      clicks++;
      console.log(clicks);
    });
}

Every click remembers and updates the same clicks variable.

This is a very common real-world use of closures.


---

Step 11: Common Interview Example

Consider:

for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}

Output:

4
4
4

Why?

Because:

var is function-scoped.

All callbacks share the same i.

By the time callbacks execute:


i = 4

So each callback prints 4.


---

Fix using let

for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}

Output:

1
2
3

let creates a new binding for each iteration.

Each callback closes over its own i.


---

Step 12: Closure Lifecycle

function outer() {
  let x = 10;

  return function () {
    console.log(x);
  };
}

const fn = outer();

Normally:

outer finishes
x should be destroyed

But because fn references x:

x remains in memory

Once:

fn = null;

and no references remain, JavaScript can garbage collect the closure.


---

Step 13: Advantages of Closures

1. Data Hiding

private variables

2. State Preservation

counters
timers
caches

3. Function Factories

double()
triple()

4. Event Handling

button clicks
DOM interactions

5. Memoization

Store previous results for faster execution.


---

Step 14: One-Line Definition for Interviews

> A closure is a function that remembers and can access variables from its lexical scope even after the outer function has finished executing.



Example:

function outer() {
  let name = "John";

  return function () {
    console.log(name);
  };
}

const fn = outer();
fn();

fn() can still access name because of the closure.


---

Mental Model

Think of a closure as:

Function
+
Its remembered variables

Closure
=
Function Code
+
Lexical Environment

Whenever you see a function being returned, passed as a callback, or stored for later execution, ask:

> "What variables is this function remembering from where it was created?"



Those remembered variables form the closure.
