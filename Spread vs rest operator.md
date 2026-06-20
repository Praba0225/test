In modern JavaScript (and therefore React), the spread operator (...) and rest operator (...) use the same syntax but serve different purposes.

A simple way to remember:

Spread = expands elements.

Rest = collects elements.



---

spread and rest operators follow shallow copy. shallow copy 
updates only top level properties in an array or object. nested objects still share the same memory/ref

1. Spread Operator (...)

The spread operator takes an iterable (array, object, string, etc.) and spreads its contents out.

A. Spread with Arrays

Example

const fruits = ["Apple", "Banana"];
const moreFruits = [...fruits, "Orange"];

console.log(moreFruits);

Output:

["Apple", "Banana", "Orange"]

Without Spread

const fruits = ["Apple", "Banana"];

const moreFruits = [fruits, "Orange"];

console.log(moreFruits);

Output:

[["Apple", "Banana"], "Orange"]

Spread expands the array elements individually.


---

B. Copying Arrays

Example

const numbers = [1, 2, 3];

const copy = [...numbers];

console.log(copy);

Output:

[1, 2, 3]

Why useful in React?

React state should not be mutated directly.

❌ Wrong

numbers.push(4);

✅ Correct

const updatedNumbers = [...numbers, 4];


---

C. Merging Arrays

const arr1 = [1, 2];
const arr2 = [3, 4];

const merged = [...arr1, ...arr2];

console.log(merged);

Output:

[1, 2, 3, 4]


---

D. Spread with Objects

Copying Objects

const user = {
  name: "John",
  age: 25
};

const copyUser = {
  ...user
};

console.log(copyUser);

Output:

{
  name: "John",
  age: 25
}


---

Updating Object Properties

Very common in React state updates.

const user = {
  name: "John",
  age: 25
};

const updatedUser = {
  ...user,
  age: 26
};

console.log(updatedUser);

Output:

{
  name: "John",
  age: 26
}

The old object remains unchanged.


---

React Example: Updating State

import { useState } from "react";

function App() {
  const [user, setUser] = useState({
    name: "John",
    age: 25
  });

  const increaseAge = () => {
    setUser({
      ...user,
      age: user.age + 1
    });
  };

  return (
    <>
      <h2>{user.name}</h2>
      <h3>{user.age}</h3>

      <button onClick={increaseAge}>
        Increase Age
      </button>
    </>
  );
}

Here:

...user

copies all existing properties and only updates age.


---

E. Passing Props in React

Parent

const user = {
  name: "John",
  age: 25,
  city: "Mumbai"
};

<UserCard {...user} />

Child

function UserCard(props) {
  return (
    <>
      <h2>{props.name}</h2>
      <p>{props.age}</p>
      <p>{props.city}</p>
    </>
  );
}

Equivalent to:

<UserCard
  name="John"
  age={25}
  city="Mumbai"
/>

Spread converts object properties into individual props.


---

2. Rest Operator (...)

The rest operator collects multiple values into a single array or object.


---

A. Rest in Function Parameters

function sum(...numbers) {
  return numbers.reduce(
    (total, num) => total + num,
    0
  );
}

console.log(sum(10, 20, 30));

Output:

60

Here:

...numbers

collects all arguments into an array.

numbers = [10, 20, 30]


---

B. Rest with Array Destructuring

const colors = ["Red", "Blue", "Green", "Yellow"];

const [first, second, ...remaining] = colors;

console.log(first);
console.log(second);
console.log(remaining);

Output:

Red
Blue
["Green", "Yellow"]


---

C. Rest with Object Destructuring

const user = {
  name: "John",
  age: 25,
  city: "Mumbai"
};

const { name, ...otherDetails } = user;

console.log(name);
console.log(otherDetails);

Output:

John

{
  age: 25,
  city: "Mumbai"
}

Everything except name is collected into otherDetails.


---

React Example: Handling Remaining Props

A common React pattern.

function Button({ children, ...props }) {
  return (
    <button {...props}>
      {children}
    </button>
  );
}

Usage:

<Button
  type="button"
  className="primary"
  onClick={() => alert("Clicked")}
>
  Save
</Button>

Inside the component:

children = "Save"

props = {
  type: "button",
  className: "primary",
  onClick: ...
}

Then:

<button {...props}>

spreads those props onto the button element.

This pattern is widely used in reusable React components.


---

Spread vs Rest Comparison

Spread (Expands)

const arr = [1, 2, 3];

console.log(...arr);

Output:

1 2 3

Array elements are expanded.


---

Rest (Collects)

function test(...arr) {
  console.log(arr);
}

test(1, 2, 3);

Output:

[1, 2, 3]

Values are collected.


---

Real React Interview Examples

Updating Array State

const [todos, setTodos] = useState([]);

const addTodo = () => {
  setTodos([
    ...todos,
    "Learn React"
  ]);
};


---

Removing Item from Array

const removeTodo = (index) => {
  setTodos(
    todos.filter((_, i) => i !== index)
  );
};

Alternative with spread:

setTodos([
  ...todos.slice(0, index),
  ...todos.slice(index + 1)
]);


---

Updating One Object in State

const [profile, setProfile] = useState({
  name: "John",
  age: 25
});

setProfile({
  ...profile,
  age: 26
});


---

Combining Multiple State Objects

const personal = {
  name: "John"
};

const address = {
  city: "Mumbai"
};

const user = {
  ...personal,
  ...address
};

console.log(user);

Output:

{
  name: "John",
  city: "Mumbai"
}


---

Key Takeaways

Spread Operator	Rest Operator

Expands values	Collects values
Used while creating arrays/objects	Used while destructuring or receiving arguments
const arr2 = [...arr1]	function fn(...args)
const obj2 = {...obj1}	const {name, ...rest} = obj
Common for React state updates	Common for reusable React components


Quick Memory Trick

// Spread → Expand
const newArr = [...oldArr];

// Rest → Collect
function demo(...args) {}

Spread = unpack/open a box.
Rest = pack remaining items into a box.
