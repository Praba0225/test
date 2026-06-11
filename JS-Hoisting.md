Hoisting is a JavaScript behavior where declarations are processed before the code is executed. It often looks like variables and functions are "moved" to the top of their scope, although JavaScript doesn't literally move the code.

Let's build the concept step by step.


---

Step 1: What Happens Before Execution?

When JavaScript runs a file, it generally goes through two phases:

1. Creation Phase

Memory is allocated for variables and functions.

Function declarations are stored completely.

Variables are initialized depending on how they are declared.



2. Execution Phase

Code runs line by line.

Variables get assigned their actual values.




Example:

console.log(a);
var a = 10;

JavaScript treats it roughly like:

var a;       // Creation phase

console.log(a); // undefined
a = 10;         // Execution phase

Output:

undefined

This behavior is called hoisting.


---

Step 2: Hoisting with var

Variables declared using var are hoisted and initialized with undefined.

Example:

console.log(city);

var city = "Chennai";

Output:

undefined

Internal view:

var city;

console.log(city); // undefined

city = "Chennai";


---

Step 3: Hoisting with Function Declarations

Function declarations are fully hoisted.

Example:

greet();

function greet() {
    console.log("Hello");
}

Output:

Hello

Why?

During the creation phase, JavaScript stores the entire function:

function greet() {
    console.log("Hello");
}

greet();

So you can call the function before its declaration.


---

Step 4: Hoisting with Function Expressions

Function expressions behave differently.

Example:

sayHi();

var sayHi = function() {
    console.log("Hi");
};

Output:

TypeError: sayHi is not a function

What happens?

var sayHi;       // hoisted as undefined

sayHi();         // undefined()

sayHi = function() {
    console.log("Hi");
};

Since sayHi is undefined at the time of the call, JavaScript throws an error.


---

Step 5: Hoisting with let

Variables declared with let are hoisted, but they are not initialized.

Example:

console.log(age);

let age = 25;

Output:

ReferenceError

This surprises many beginners because let is hoisted, but you cannot access it before its declaration.


---

Step 6: Temporal Dead Zone (TDZ)

The period between entering a scope and the declaration of a let or const variable is called the Temporal Dead Zone (TDZ).

Example:

{
    console.log(score);

    let score = 100;
}

Output:

ReferenceError

Visualization:

{
   // TDZ starts

   console.log(score); // Error

   let score = 100;

   // TDZ ends
}

The variable exists in memory but cannot be used yet.


---

Step 7: Hoisting with const

const behaves similarly to let.

Example:

console.log(PI);

const PI = 3.14;

Output:

ReferenceError

Reason:

Hoisted

Not initialized

Lives in the TDZ until declaration



---

Step 8: Compare var, let, and const

Declaration	Hoisted	Initial Value	Access Before Declaration

var	Yes	undefined	Allowed
let	Yes	Uninitialized	ReferenceError
const	Yes	Uninitialized	ReferenceError


Example:

console.log(a); // undefined
console.log(b); // ReferenceError
console.log(c); // ReferenceError

var a = 1;
let b = 2;
const c = 3;


---

Step 9: Function Declaration vs Function Expression

Function Declaration

hello();

function hello() {
    console.log("Hello");
}

✅ Works


---

Function Expression

hello();

var hello = function() {
    console.log("Hello");
};

❌ TypeError


---

Arrow Function

hello();

const hello = () => {
    console.log("Hello");
};

❌ ReferenceError


---

Step 10: Interview Example

Question:

var x = 1;

function test() {
    console.log(x);

    var x = 2;

    console.log(x);
}

test();

Output:

undefined
2

Explanation:

Inside test():

function test() {

    var x;           // hoisted

    console.log(x);  // undefined

    x = 2;

    console.log(x);  // 2
}

The local x shadows the global x.


---

Step 11: Another Common Interview Question

function foo() {
    console.log(a);
    let a = 10;
}

foo();

Output:

ReferenceError

Reason:

a is in the Temporal Dead Zone until the let declaration executes.


---

Step 12: Mental Model for Hoisting

Think of JavaScript as doing this:

First Pass (Creation Phase)

var a = undefined;

function greet() {
   ...
}

Second Pass (Execution Phase)

a = 10;
greet();

This explains most hoisting-related behavior.


---

Quick Summary

Hoisting is JavaScript's behavior of processing declarations before execution.

var is hoisted and initialized with undefined.

Function declarations are fully hoisted.

Function expressions are not fully hoisted.

let and const are hoisted but remain in the Temporal Dead Zone (TDZ) until their declaration is reached.

Accessing let or const before declaration causes a ReferenceError.

Hoisting is tied to JavaScript's creation phase and execution phase.


A useful interview definition:

> Hoisting is JavaScript's mechanism of allocating memory for declarations before code execution. Function declarations are fully initialized, var variables are initialized to undefined, and let/const remain uninitialized in the Temporal Dead Zone until their declaration is executed.
