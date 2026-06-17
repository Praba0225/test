Suspense is often misunderstood as a "loading component". It's actually a mechanism that allows React to pause rendering of part of the UI until some asynchronous work completes.

In lazy loading, that asynchronous work is usually downloading a JavaScript chunk.


---

What happens without Suspense?

Suppose you have:

const Dashboard = React.lazy(() =>
  import("./Dashboard")
);

function App() {
  return <Dashboard />;
}

When React tries to render Dashboard:

App Render
    ↓
Dashboard Component Needed
    ↓
Chunk Not Downloaded Yet
    ↓
React Cannot Render Component

React would throw an error because the component isn't available yet.

That's why React requires a Suspense boundary.


---

How Suspense Works

import { lazy, Suspense } from "react";

const Dashboard = lazy(() =>
  import("./Dashboard")
);

function App() {
  return (
    <Suspense fallback={<h2>Loading...</h2>}>
      <Dashboard />
    </Suspense>
  );
}


---

Internal Flow

Step 1: Initial Render

React starts rendering.

App
 └─ Dashboard


---

Step 2: Dashboard isn't loaded

React.lazy executes:

import("./Dashboard")

This returns a Promise.

Promise<pending>


---

Step 3: React "Suspends"

React sees:

Dashboard unavailable
Promise pending

React pauses rendering that subtree.

Dashboard
    ↓
Suspended


---

Step 4: Fallback is rendered

Instead of Dashboard:

fallback={<h2>Loading...</h2>}

is shown.

UI becomes:

<h2>Loading...</h2>


---

Step 5: Chunk Download Completes

Browser downloads:

dashboard.chunk.js

Promise resolves:

Promise<resolved>


---

Step 6: React Retries Render

React automatically tries again.

Dashboard Available
      ↓
Render Dashboard

Now UI becomes:

<h1>Dashboard Page</h1>


---

Visual Timeline

Page Load
    ↓
Render Dashboard
    ↓
Chunk Missing
    ↓
Suspend
    ↓
Show Fallback
    ↓
Download Chunk
    ↓
Promise Resolved
    ↓
Retry Render
    ↓
Show Dashboard


---

Real Example

Dashboard.jsx

export default function Dashboard() {
  return <h1>Dashboard Loaded</h1>;
}

App.jsx

import { lazy, Suspense } from "react";

const Dashboard = lazy(() =>
  import("./Dashboard")
);

export default function App() {
  return (
    <Suspense fallback={<p>Loading Dashboard...</p>}>
      <Dashboard />
    </Suspense>
  );
}


---

Nested Suspense Boundaries

You can have multiple boundaries.

<Suspense fallback={<p>Loading Page...</p>}>
  <Dashboard />

  <Suspense fallback={<p>Loading Chart...</p>}>
    <Chart />
  </Suspense>
</Suspense>

Flow:

Dashboard Loading
     ↓
Loading Page...

Dashboard Loaded
     ↓
Dashboard Visible

Chart Loading
     ↓
Loading Chart...

The whole page doesn't wait for the chart.


---

Route-Level Example

const Home = lazy(() => import("./Home"));
const Profile = lazy(() => import("./Profile"));

<Suspense fallback={<Spinner />}>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/profile" element={<Profile />} />
  </Routes>
</Suspense>


---

Visiting "/"

Download Home Chunk
Show Spinner
Render Home


---

Navigating to "/profile"

Download Profile Chunk
Show Spinner
Render Profile

Only the Profile code is fetched.


---

What React.lazy Actually Returns

This:

const Dashboard = lazy(() =>
  import("./Dashboard")
);

creates a special React component.

Internally it's similar to:

{
  $$typeof: Symbol(react.lazy),
  load: () => import("./Dashboard")
}

When React renders it:

Has module loaded?
      ↓
No
      ↓
Start import()
      ↓
Throw Promise
      ↓
Nearest Suspense catches it

The key idea is:

> React.lazy "throws" a Promise during rendering. Suspense catches that Promise and shows the fallback until the Promise resolves.




---

Why People Say "Suspense Catches a Promise"

Conceptually:

function Dashboard() {
  throw promise;
}

Not literally, but that's close to what React does internally.

Component Needs Data/Code
         ↓
Promise Pending
         ↓
Throw Promise
         ↓
Suspense Boundary Catches It
         ↓
Show Fallback
         ↓
Promise Resolves
         ↓
Retry Render


---

Suspense for Data Fetching (Beyond Lazy Loading)

Suspense is not limited to code splitting.

React can also suspend while waiting for data.

Example idea:

<Suspense fallback={<Spinner />}>
  <UserProfile />
</Suspense>

If UserProfile suspends because data is still loading:

Fetch User
     ↓
Promise Pending
     ↓
Suspend
     ↓
Show Spinner
     ↓
Data Arrives
     ↓
Render UserProfile

Libraries like TanStack Query can integrate with Suspense mode, although the most common use today is still lazy-loaded components.


---

Mental Model

Think of Suspense as a loading boundary:

Inside Boundary
      ↓
Anything Not Ready?
      ↓
Yes
      ↓
Show Fallback
      ↓
Wait
      ↓
Ready
      ↓
Render Actual UI

For lazy loading:

Not Ready = JS chunk not downloaded

For data fetching:

Not Ready = API response not received

The important distinction is:

React.lazy() creates a component that loads asynchronously.

Suspense provides the UI to show while React waits for that asynchronous work to finish. Without Suspense, React has nowhere to render the loading state for a suspended component.
