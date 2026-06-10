A Promise in JavaScript is an object that represents the eventual result of an asynchronous operation.

Think of it as a placeholder for a value that may be available now, later, or never (if an error occurs).


---

1. Why do we need Promises?

JavaScript often performs tasks that take time:

Fetching data from an API

Reading files

Database queries

Timers


Without promises, handling these operations can become messy.

Example using setTimeout:

console.log("Start");

setTimeout(() => {
  console.log("Data received");
}, 2000);

console.log("End");

Output:

Start
End
Data received

The code doesn't wait for the timeout to finish.

Promises help us manage such asynchronous operations in a structured way.


---

2. What is a Promise?

A promise is an object that eventually settles with either:

A successful value

An error


Example:

const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

Here:

resolve() → operation succeeded

reject() → operation failed



---

3. Promise States

A promise can be in one of three states:

Pending

Initial state.

Pending

The operation is still running.


---

Fulfilled

Operation completed successfully.

Pending → Fulfilled


---

Rejected

Operation failed.

Pending → Rejected


---

Visual representation:

Promise
                |
          ----------------
          |              |
      Fulfilled      Rejected


---

4. Creating a Promise

Syntax:

const promise = new Promise((resolve, reject) => {
  // async work
});

Example:

const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Data loaded");
  } else {
    reject("Something went wrong");
  }
});


---

5. Consuming a Promise

We use:

.then()

.catch()

.finally()


Example:

promise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.log(error);
  });

Output:

Data loaded


---

6. Understanding .then()

.then() runs when the promise is fulfilled.

Example:

const promise = Promise.resolve("Hello");

promise.then(data => {
  console.log(data);
});

Output:

Hello


---

7. Understanding .catch()

.catch() runs when the promise is rejected.

Example:

const promise = Promise.reject("Network Error");

promise.catch(error => {
  console.log(error);
});

Output:

Network Error


---

8. Understanding .finally()

Runs regardless of success or failure.

Example:

fetchData()
  .then(data => console.log(data))
  .catch(err => console.log(err))
  .finally(() => {
    console.log("Finished");
  });

Output:

Data
Finished

or

Error
Finished


---

9. Real Example with setTimeout

const getData = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("User Data");
  }, 2000);
});

getData.then(data => {
  console.log(data);
});

After 2 seconds:

User Data


---

10. Promise Chaining

A .then() can return a value.

Example:

Promise.resolve(10)
  .then(num => num * 2)
  .then(num => num + 5)
  .then(result => {
    console.log(result);
  });

Output:

25

Flow:

10
 ↓
20
 ↓
25


---

11. Returning Another Promise

Promise.resolve(5)
  .then(num => {
    return Promise.resolve(num * 2);
  })
  .then(result => {
    console.log(result);
  });

Output:

10

JavaScript automatically waits for the returned promise.


---

12. Error Handling in Chains

Promise.resolve()
  .then(() => {
    throw new Error("Oops");
  })
  .catch(err => {
    console.log(err.message);
  });

Output:

Oops

Errors automatically travel down the chain until caught.


---

13. Promise vs Callback

Callback Style

getUser(function(user) {
  getOrders(user.id, function(orders) {
    getPayment(orders[0], function(payment) {
      console.log(payment);
    });
  });
});

This becomes:

Callback Hell


---

Promise Style

getUser()
  .then(user => getOrders(user.id))
  .then(orders => getPayment(orders[0]))
  .then(payment => console.log(payment))
  .catch(err => console.log(err));

Much cleaner.


---

14. Promise Static Methods

Promise.resolve()

Creates a resolved promise.

Promise.resolve("Done")
  .then(console.log);

Output:

Done


---

Promise.reject()

Creates a rejected promise.

Promise.reject("Failed")
  .catch(console.log);

Output:

Failed


---

15. Promise.all()

Waits for all promises.

const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then(result => {
    console.log(result);
  });

Output:

[1, 2, 3]

If any promise fails:

Promise.all([
  Promise.resolve(1),
  Promise.reject("Error"),
  Promise.resolve(3)
]);

Result:

Rejected immediately


---

16. Promise.allSettled()

Waits for every promise.

Promise.allSettled([
  Promise.resolve("A"),
  Promise.reject("B")
]).then(result => {
  console.log(result);
});

Output:

[
  { status: "fulfilled", value: "A" },
  { status: "rejected", reason: "B" }
]


---

17. Promise.race()

Returns the first settled promise.

Promise.race([
  new Promise(resolve =>
    setTimeout(() => resolve("Fast"), 1000)
  ),
  new Promise(resolve =>
    setTimeout(() => resolve("Slow"), 3000)
  )
]).then(console.log);

Output:

Fast


---

18. Promise.any()

Returns the first successful promise.

Promise.any([
  Promise.reject("Error"),
  Promise.resolve("Success")
]).then(console.log);

Output:

Success


---

19. Async/Await and Promises

async/await is built on top of promises.

Promise version:

getData()
  .then(data => {
    console.log(data);
  })
  .catch(err => {
    console.log(err);
  });

Async/Await version:

async function loadData() {
  try {
    const data = await getData();
    console.log(data);
  } catch (err) {
    console.log(err);
  }
}

Cleaner syntax, same underlying promise mechanism.


---

20. How the Event Loop Handles Promises

Promise callbacks (then, catch) go into the Microtask Queue.

Example:

console.log("A");

Promise.resolve().then(() => {
  console.log("B");
});

console.log("C");

Output:

A
C
B

Execution order:

Call Stack
   ↓
Promise Microtasks
   ↓
Macrotasks (setTimeout, etc.)


---

21. Practical API Example

fetch("https://jsonplaceholder.typicode.com/users/1")
  .then(response => response.json())
  .then(user => {
    console.log(user.name);
  })
  .catch(error => {
    console.error(error);
  });

Flow:

Request Sent
     ↓
Response Received
     ↓
Convert JSON
     ↓
Use Data
     ↓
Handle Errors
-----
response.json() is a method used with the Fetch API to read the response body and convert JSON text into a JavaScript object.

Example:

fetch("https://jsonplaceholder.typicode.com/users/1")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  });

Suppose the server returns:

{
  "id": 1,
  "name": "Leanne Graham"
}

Here's what happens:

Step 1: Fetch request

fetch(url)

Returns a Promise that resolves to a Response object.

Step 2: Get the response

.then(response => response.json())

The response contains metadata and the raw body.

console.log(response);

Might show:

Response {
  status: 200,
  ok: true,
  body: ReadableStream
}

The body is still raw data.

Step 3: Parse JSON

response.json()

Reads the body and converts:

{"id":1,"name":"Leanne Graham"}

into:

{
  id: 1,
  name: "Leanne Graham"
}

Step 4: Use the JavaScript object

.then(data => {
  console.log(data.name);
});

Output:

Leanne Graham

Important

response.json() itself returns a Promise because reading and parsing the response takes time.

That's why we write:

response.json().then(data => {
  console.log(data);
});

or with async/await:

const response = await fetch(url);
const data = await response.json();

console.log(data);

Simple analogy

Imagine the server sends a package:

Server
  ↓
'{"name":"John","age":25}'   (JSON text)

response.json() opens the package and converts it into:

{
  name: "John",
  age: 25
}

which JavaScript can work with directly.
---

Summary

A Promise is a JavaScript object that represents the future result of an asynchronous operation.

Key concepts:

1. Promise has 3 states:

Pending

Fulfilled

Rejected



2. Main methods:

.then()

.catch()

.finally()



3. Promise utilities:

Promise.resolve()

Promise.reject()

Promise.all()

Promise.allSettled()

Promise.race()

Promise.any()



4. async/await is syntactic sugar over promises.


5. Promise callbacks run in the microtask queue, which is why they execute before setTimeout callbacks.



A good next step is to learn Promises with real API calls (fetch), then move on to async/await, since that's how modern JavaScript applications are typically written.
