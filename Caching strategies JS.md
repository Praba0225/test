In-Memory Caching in Detail

In-memory caching is the simplest and fastest caching strategy. Data is stored directly in the application's memory (RAM) so that future requests can reuse it without performing expensive operations such as API calls, database queries, or complex calculations.

Think of it as a temporary "shortcut" inside your running application.


---

Why Do We Need In-Memory Caching?

Suppose your application repeatedly requests the same user data:

User opens profile
↓
API Call
↓
Database Query
↓
Return Data

If another component requests the same data immediately afterward:

User opens settings
↓
API Call
↓
Database Query Again
↓
Return Same Data

This creates unnecessary work.

With in-memory caching:

First Request
↓
API Call
↓
Store Result in Memory

Second Request
↓
Read from Memory
↓
No API Call

Response time becomes almost instantaneous.


---

How In-Memory Cache Works

A cache usually consists of:

const cache = {};

or

const cache = new Map();

The cache stores:

Key → Value

Example:

{
  "user_1": {
    id: 1,
    name: "John"
  }
}


---

Step-by-Step Example

Without Cache

async function getUser(id) {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}

Flow:

getUser(1)
↓
API Request
↓
Server Response

getUser(1)
↓
API Request Again
↓
Server Response

Every call hits the server.


---

With Cache

const cache = {};

async function getUser(id) {
  if (cache[id]) {
    return cache[id];
  }

  const response = await fetch(`/api/users/${id}`);
  const user = await response.json();

  cache[id] = user;

  return user;
}

Flow:

First Call

getUser(1)
↓
Check Cache
↓
Not Found
↓
API Request
↓
Store in Cache
↓
Return Data

Second Call

getUser(1)
↓
Check Cache
↓
Found
↓
Return Cached Data

No network request.


---

Cache Hit vs Cache Miss

These are important terms.

Cache Hit

Data exists in cache.

Request
↓
Cache
↓
Found
↓
Return Data

Time:

~1 ms


---

Cache Miss

Data doesn't exist.

Request
↓
Cache
↓
Not Found
↓
API Call
↓
Store Result

Time:

100-500 ms

depending on network speed.


---

Using Object vs Map

Object

const cache = {};
cache["user1"] = data;

Works fine for small caches.


---

Map

Recommended for larger caches.

const cache = new Map();

cache.set("user1", data);

cache.get("user1");

Advantages:

Better performance

Any key type supported

Useful methods


cache.has(key);
cache.delete(key);
cache.clear();


---

Cache Expiration (TTL)

One problem:

Data changes on server
↓
Cache still has old data
↓
User sees outdated information

Solution:

Time To Live (TTL)


---

Example:

const cache = new Map();
const TTL = 60000;

Store:

cache.set(id, {
  data: user,
  timestamp: Date.now()
});

Read:

const item = cache.get(id);

if (
  item &&
  Date.now() - item.timestamp < TTL
) {
  return item.data;
}


---

Flow:

Request
↓
Check Cache

Is Data Younger Than 60 sec?
↓
Yes → Return Cache
No → Fetch Again


---

Cache Eviction

Memory is limited.

If cache keeps growing:

100 records
1000 records
10000 records
100000 records

RAM usage increases.

Old entries must be removed.


---

Manual Eviction

cache.delete("user1");

or

cache.clear();


---

LRU (Least Recently Used)

Most popular eviction strategy.

Rule:

Remove oldest unused item first

Example:

Cache size = 3

A
B
C

User accesses:

A

Order becomes:

B
C
A

Insert D:

B removed

Result:

C
A
D


---

Request Deduplication

A common issue:

Two components request the same data simultaneously.

Without protection:

Component A
↓
API Request

Component B
↓
API Request

Two identical calls.


---

Solution:

Cache the Promise.

const cache = new Map();

function getUser(id) {
  if (cache.has(id)) {
    return cache.get(id);
  }

  const promise = fetch(`/api/users/${id}`)
    .then(res => res.json());

  cache.set(id, promise);

  return promise;
}


---

Flow:

Component A
↓
Creates Promise

Component B
↓
Uses Same Promise

Only One Network Request

This is how libraries like React Query work internally.


---

Memory Cache for Computation

Caching is not only for APIs.

Example:

function fibonacci(n) {
  if (n <= 1) return n;

  return fibonacci(n - 1) +
         fibonacci(n - 2);
}

Very slow for large numbers.


---

Memoized version:

const cache = {};

function fibonacci(n) {
  if (cache[n]) {
    return cache[n];
  }

  if (n <= 1) {
    return n;
  }

  cache[n] =
    fibonacci(n - 1) +
    fibonacci(n - 2);

  return cache[n];
}


---

Flow:

fib(50)
↓
Calculate Once
↓
Store Results
↓
Future Calls Reuse Values

Huge performance gain.


---

React Example

Suppose multiple components need user data.

Service Layer Cache

const userCache = new Map();

export async function getUser(id) {
  if (userCache.has(id)) {
    return userCache.get(id);
  }

  const data =
    await fetch(`/api/users/${id}`)
      .then(r => r.json());

  userCache.set(id, data);

  return data;
}

Components reuse the cached data.


---

Angular Example

Service singleton acts as memory cache.

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private cache = new Map();

  getUser(id: number) {
    return this.cache.get(id);
  }
}

Since Angular services are often singletons, the cache survives while the application is running.


---

Advantages of In-Memory Caching

Extremely Fast

RAM access
≈ nanoseconds to microseconds

Much faster than network or disk.


---

Reduces API Calls

100 requests
↓
10 actual API calls

Lower server load.


---

Better User Experience

Instant responses

No loading spinners for repeated data.


---

Simple Implementation

Only a few lines of code are needed.


---

Limitations of In-Memory Caching

Lost on Refresh

Page Refresh
↓
Memory Cleared
↓
Cache Lost

Unlike localStorage or IndexedDB.


---

Consumes RAM

Large caches can cause:

High memory usage
Slow application
Browser crashes


---

Stale Data

Server Updated
↓
Cache Not Updated
↓
User Sees Old Data

Requires TTL or invalidation strategies.


---

Not Shared Across Tabs

Tab A Cache
≠
Tab B Cache

Each browser tab has its own memory.


---

Common Invalidation Strategies

The hardest part of caching is knowing when to remove cached data.

Typical approaches:

Time-Based

Cache expires after 5 minutes

Event-Based

User updates profile
↓
Delete cached profile

Version-Based

Server sends version number
↓
Version changed
↓
Refresh cache


---

Real-World Architecture

A typical frontend memory cache looks like:

UI Component
     ↓
Memory Cache
     ↓ (miss)
API Request
     ↓
Server
     ↓
Store Result In Cache
     ↓
Return Data

Subsequent requests become:

UI Component
     ↓
Memory Cache
     ↓
Return Data

No network traffic.


---

Key Principle

In-memory caching is best when:

Data is accessed frequently.

Data changes relatively infrequently.

Fast response time is important.

Losing the cache on page refresh is acceptable.


It is often the first layer of caching in modern React, Angular, and JavaScript applications, with additional layers such as browser cache, service worker cache, and server-side caches built on top of it.



I think you mean memoization (a caching technique in programming), not memorization (remembering information).

What is Memoization?

Memoization is an optimization technique where the result of a function call is stored (cached) so that if the same inputs are provided again, the cached result is returned instead of recalculating it.

Simple Idea

Without memoization:

square(5) → calculate → 25
square(5) → calculate again → 25
square(5) → calculate again → 25

With memoization:

square(5) → calculate → cache 25
square(5) → return cached 25
square(5) → return cached 25

The computation happens only once.


---

Why Do We Need Memoization?

Some operations are expensive:

Complex mathematical calculations

Recursive algorithms

Large array filtering/sorting

Data transformations

React component computations


Instead of repeating the same work, we store the result and reuse it.


---

How Memoization Works

The process is:

Function Call
      ↓
Check Cache
      ↓
Result Exists?
   ↙        ↘
 Yes         No
 ↓            ↓
Return     Calculate
Cache         ↓
             Store
               ↓
           Return


---

Example 1: Basic Memoization

Normal function:

function square(n) {
  console.log("Calculating...");
  return n * n;
}

square(5);
square(5);

Output:

Calculating...
Calculating...

The calculation runs twice.


---

Memoized version:

function memoizedSquare() {
  const cache = {};

  return function(n) {
    if (cache[n]) {
      console.log("From cache");
      return cache[n];
    }

    console.log("Calculating");

    const result = n * n;

    cache[n] = result;

    return result;
  };
}

const square = memoizedSquare();

square(5);
square(5);

Output:

Calculating
From cache

The second call avoids recalculation.


---

Example 2: Fibonacci (Classic Example)

Fibonacci:

fib(5)
=
fib(4) + fib(3)

Without memoization:

function fib(n) {
  if (n <= 1) return n;

  return fib(n - 1) + fib(n - 2);
}

Calling:

fib(40);

can be very slow because many values are recomputed repeatedly.


---

Visualization:

fib(5)
├─ fib(4)
│  ├─ fib(3)
│  │  ├─ fib(2)
│  │  └─ fib(1)
│  └─ fib(2)
└─ fib(3)
   ├─ fib(2)
   └─ fib(1)

Notice:

fib(3) repeated
fib(2) repeated

The same calculations happen many times.


---

Memoized Fibonacci:

const cache = {};

function fib(n) {
  if (n in cache) {
    return cache[n];
  }

  if (n <= 1) {
    return n;
  }

  cache[n] =
    fib(n - 1) +
    fib(n - 2);

  return cache[n];
}

Now:

fib(40)

becomes dramatically faster because each value is calculated only once.


---

Example 3: API Data Memoization

Suppose you fetch user data.

Without cache:

async function getUser(id) {
  const response =
    await fetch(`/users/${id}`);

  return response.json();
}

Calls:

getUser(1);
getUser(1);
getUser(1);

Result:

3 API requests


---

Memoized version:

const cache = {};

async function getUser(id) {
  if (cache[id]) {
    return cache[id];
  }

  const response =
    await fetch(`/users/${id}`);

  const user =
    await response.json();

  cache[id] = user;

  return user;
}

Now:

getUser(1);
getUser(1);
getUser(1);

Result:

1 API request
2 cache reads


---

Generic Memoize Function

A reusable memoization utility:

function memoize(fn) {
  const cache = {};

  return function (...args) {
    const key =
      JSON.stringify(args);

    if (key in cache) {
      return cache[key];
    }

    const result =
      fn(...args);

    cache[key] = result;

    return result;
  };
}

Usage:

const add = memoize(
  (a, b) => a + b
);

console.log(add(2, 3));
console.log(add(2, 3));

First call:

Calculate

Second call:

Cache hit


---

Memoization in React

React uses memoization extensively to improve rendering performance.

useMemo

Imagine filtering 10,000 users.

Without memoization:

const activeUsers =
  users.filter(
    user => user.active
  );

Every render executes the filter again.


---

Using useMemo:

const activeUsers = useMemo(() => {
  return users.filter(
    user => user.active
  );
}, [users]);

Flow:

Render
 ↓
Did users change?
 ↓
No
 ↓
Use cached result

Only recalculates when users changes.


---

React.memo

Without:

Parent renders
↓
Child renders

every time.


---

With:

const UserCard =
  React.memo(function UserCard(props) {
    return <div>{props.name}</div>;
  });

Flow:

Parent renders
↓
Props unchanged
↓
Skip child render

This is component-level memoization.


---

When Should You Use Memoization?

Good candidates:

Expensive Calculations

calculateTax(data)
generateReport(data)

Large Array Operations

users.filter(...)
users.sort(...)
users.reduce(...)

Recursive Algorithms

Fibonacci
Tree traversal
Graph search

React Rendering Optimization

useMemo
useCallback
React.memo


---

When NOT to Use Memoization

Don't memoize trivial operations:

a + b
x * y

Example:

const result = useMemo(
  () => a + b,
  [a, b]
);

This usually adds unnecessary complexity because the calculation is already cheap.


---

Benefits

Faster Execution

Avoid repeated calculations.

Reduced API Calls

Reuse fetched data.

Better UI Performance

Fewer renders and computations.

Improved User Experience

Faster page interactions.


---

Drawbacks

More Memory Usage

Cached values consume RAM.

1000 cached results
↓
More memory

Stale Data

Cached data may become outdated.

Server updates
↓
Old cache remains

Cache Management Complexity

You may need:

TTL (expiration)

Cache invalidation

Size limits



---

Memoization vs Caching

Many developers use the terms interchangeably, but there is a subtle difference:

Aspect	Memoization	Caching

Purpose	Store function results	Store any data
Scope	Usually function-level	Application-wide
Key	Function arguments	Custom keys
Example	fib(10) result	API response cache


Example:

memoize(square)

is memoization.

cache["user_1"] = user

is general caching.

Memoization is essentially a specialized form of caching focused on function outputs.
