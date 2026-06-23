Improving the performance of a React application is mainly about reducing unnecessary work: fewer re-renders, smaller bundles, faster data fetching, and efficient rendering of large UI elements.

Below is a step-by-step guide with examples.

1. Identify Performance Bottlenecks First

Before optimizing, measure performance.

React Developer Tools Profiler

Install React DevTools and use the Profiler tab.

function App() {
  return <Dashboard />;
}

Profile your application and identify:

Components rendering too often

Slow rendering components

Expensive calculations


What to Look For

Example:

<Dashboard />
  <UserList />
  <Chart />

If UserList renders every time Chart updates, that is unnecessary work.


---

2. Prevent Unnecessary Re-renders with React.memo

Problem

Parent re-renders cause child components to re-render.

function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
      <Child />
    </>
  );
}

function Child() {
  console.log("Child Rendered");
  return <div>Child Component</div>;
}

Every button click re-renders Child.

Solution

Use React.memo.

const Child = React.memo(() => {
  console.log("Child Rendered");
  return <div>Child Component</div>;
});

Result

Child only re-renders when its props change.


---

3. Use useCallback for Function Props

Problem

Functions are recreated every render.

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    console.log("clicked");
  };

  return <Child onClick={handleClick} />;
}

Even with React.memo, Child re-renders because handleClick is a new reference each time.

Solution

const handleClick = useCallback(() => {
  console.log("clicked");
}, []);

Full example:

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("clicked");
  }, []);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
      <Child onClick={handleClick} />
    </>
  );
}

Result

Child does not re-render unnecessarily.


---

4. Use useMemo for Expensive Calculations

Problem

Heavy calculations run on every render.

function ProductList({ products }) {

  const sortedProducts = products.sort(
    (a, b) => a.price - b.price
  );

  return (
    <div>
      {sortedProducts.map(p => (
        <p key={p.id}>{p.name}</p>
      ))}
    </div>
  );
}

Sorting runs every render.

Solution

const sortedProducts = useMemo(() => {
  return [...products].sort(
    (a, b) => a.price - b.price
  );
}, [products]);

Result

Sorting only happens when products changes.


---

5. Lazy Load Components

Large components increase initial load time.

Without Lazy Loading

import Dashboard from "./Dashboard";

Dashboard loads immediately.

With Lazy Loading

import React, { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Dashboard />
    </Suspense>
  );
}

Result

Dashboard loads only when needed.


---

6. Code Splitting

Split large bundles into smaller chunks.

Route-based Code Splitting

const Home = lazy(() => import("./Home"));
const Profile = lazy(() => import("./Profile"));
const Settings = lazy(() => import("./Settings"));

<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/profile" element={<Profile />} />
  <Route path="/settings" element={<Settings />} />
</Routes>

Result

Users download only the pages they visit.


---

7. Virtualize Large Lists

Problem

Rendering 10,000 rows.

{
  users.map(user => (
    <UserCard key={user.id} user={user} />
  ));
}

Very slow.

Solution

Use virtualization libraries.

Example using react-window:

import { FixedSizeList } from "react-window";

function Row({ index, style }) {
  return (
    <div style={style}>
      User {index}
    </div>
  );
}

<FixedSizeList
  height={500}
  width={500}
  itemCount={10000}
  itemSize={35}
>
  {Row}
</FixedSizeList>;

Result

Only visible rows are rendered.


---

8. Optimize State Management

Problem

Global state updates trigger many re-renders.

const AppContext = createContext();

Every context update can re-render all consumers.

Better Approach

Split contexts.

<UserContext.Provider>
  <ThemeContext.Provider>
    {children}
  </ThemeContext.Provider>
</UserContext.Provider>

Or use:

Redux Toolkit

Zustand

Jotai


to minimize unnecessary updates.


---

9. Debounce Search Inputs

Problem

API called on every keystroke.

<input onChange={handleSearch} />

Typing "react" triggers 5 API calls.

Solution

import debounce from "lodash.debounce";

const search = useCallback(
  debounce((value) => {
    fetchUsers(value);
  }, 500),
  []
);

<input
  onChange={(e) => search(e.target.value)}
/>

Result

Only one API call after typing stops.


---

10. Optimize Images

Bad

<img src="large-image.jpg" />

5MB image downloaded.

Better

<img
  src="image.webp"
  loading="lazy"
  alt="Product"
/>

Improvements

Use WebP/AVIF

Lazy loading

Responsive images


<img
  srcSet="
    small.webp 480w,
    medium.webp 800w,
    large.webp 1200w
  "
  sizes="100vw"
  alt="Product"
/>


---

11. Cache API Requests

Using libraries like:

TanStack Query (React Query)

SWR


Example:

const { data } = useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
});

Benefits:

Automatic caching

Background refetching

Reduced API calls



---

12. Avoid Inline Objects and Arrays

Problem

New object every render.

<Child style={{ color: "red" }} />

React sees a new object reference.

Better

const style = useMemo(
  () => ({ color: "red" }),
  []
);

<Child style={style} />;


---

13. Use Production Build

Development mode is slower.

Build

npm run build

or

yarn build

Benefits

Minification

Tree shaking

Dead code elimination



---

14. Use Key Correctly in Lists

Bad

{
  users.map((user, index) => (
    <User key={index} />
  ));
}

Good

{
  users.map((user) => (
    <User key={user.id} />
  ));
}

Stable keys help React update efficiently.


---

15. Memoize Derived Data Selectors

Bad

const activeUsers = users.filter(
  user => user.active
);

Runs every render.

Good

const activeUsers = useMemo(() => {
  return users.filter(
    user => user.active
  );
}, [users]);


---

Practical Optimization Workflow

When optimizing a real React application, follow this order:

Step 1

Measure performance using React Profiler.

Step 2

Find unnecessary re-renders.

Apply:

React.memo

useCallback

useMemo


Step 3

Reduce bundle size.

Apply:

Lazy loading

Code splitting

Tree shaking


Step 4

Optimize large datasets.

Apply:

Pagination

Virtualization

Infinite scrolling


Step 5

Optimize network requests.

Apply:

Caching

Debouncing

React Query/SWR


Step 6

Optimize assets.

Apply:

Image compression

Lazy loading

CDN delivery



---

Example: Real-World E-commerce Optimization

Suppose a product page is slow.

Issues

200 products rendered

Product sorting every render

Search API called every keystroke

3MB images


Fixes

1. Wrap ProductCard with React.memo.


2. Use useMemo for sorting/filtering.


3. Debounce search input.


4. Virtualize product list.


5. Lazy load review section.


6. Convert images to WebP.


7. Cache API responses with React Query.



Result

Typical improvements:

50–80% fewer renders

Faster page load

Reduced API traffic

Better Lighthouse score

Improved user experience


A key principle is: Don't optimize everything upfront. Profile first, identify the actual bottleneck, then apply targeted optimizations such as memoization, code splitting, virtualization, caching, and efficient state management.
