In React, Client-Side Rendering (CSR) and Server-Side Rendering (SSR) refer to where the HTML is generated before the user sees the page.


---

1. Client-Side Rendering (CSR)

In CSR, the server sends a minimal HTML file and JavaScript bundles. The browser downloads the JavaScript, React runs in the browser, and then generates the UI.

Flow

Browser Request
      ↓
Server returns:
index.html + JS bundle
      ↓
Browser downloads JS
      ↓
React renders UI
      ↓
User sees page

Example

Server response:

<body>
  <div id="root"></div>
  <script src="main.js"></script>
</body>

React renders inside #root:

import ReactDOM from "react-dom/client";
import App from "./App";

ReactDOM.createRoot(
  document.getElementById("root")
).render(<App />);

Typical CSR Frameworks

React with Vite

React with Create React App

Single Page Applications (SPAs)



---

2. Server-Side Rendering (SSR)

In SSR, React components are rendered into HTML on the server before being sent to the browser.

Flow

Browser Request
      ↓
Server runs React
      ↓
HTML generated
      ↓
Browser receives ready HTML
      ↓
User sees content immediately
      ↓
React hydrates page

Example

Server-side:

import ReactDOMServer from "react-dom/server";
import App from "./App";

const html = ReactDOMServer.renderToString(<App />);

Generated HTML:

<div>
  <h1>Welcome</h1>
  <p>Hello World</p>
</div>

Browser receives already-rendered HTML.


---

Why Do We Need CSR and SSR?

Different applications have different requirements.

CSR is useful when:

App is highly interactive

SEO is not important

Most content changes after login


Examples:

Admin dashboards

Internal tools

Project management apps

Chat applications


Examples:

Jira

Slack



---

SSR is useful when:

SEO is important

Faster first-page load is desired

Content should be visible immediately


Examples:

E-commerce sites

Blogs

News websites

Marketing pages


Examples:

[Amazon](https://www.amazon.com?utm_source=chatgpt.com)

[Flipkart](https://www.flipkart.com?utm_source=chatgpt.com)



---

Benefits of Client-Side Rendering

1. Better User Experience After Initial Load

After JavaScript loads:

Navigation is instant
No full page refresh

React updates only changed parts.

2. Reduced Server Load

Server mostly serves static files:

HTML
CSS
JS

No need to render every page request.

3. Rich Interactivity

Ideal for:

Real-time updates

Drag-and-drop

Complex state management



---

Drawbacks of CSR

Slow Initial Load

Browser must:

1. Download JS


2. Parse JS


3. Execute JS


4. Render UI



Users may see:

Loading...

before content appears.

SEO Issues

Search engines may not fully execute JavaScript.

Although modern search engines have improved, SSR is generally safer for SEO.


---

Benefits of Server-Side Rendering

1. Faster First Contentful Paint (FCP)

User receives HTML immediately:

<h1>Products</h1>

No waiting for React rendering.


---

2. Better SEO

Search engines receive complete HTML:

<h1>Best Laptops</h1>

Content is directly crawlable.


---

3. Better Social Sharing

When a page is shared:

Title

Description

Meta tags


are already present in the HTML.


---

Drawbacks of SSR

Higher Server Cost

Every request may require React rendering.

Request
   ↓
Server renders React
   ↓
Returns HTML

This increases CPU usage.


---

More Complexity

Need:

Node.js server

Data fetching on server

Hydration management



---

What is Hydration?

After SSR sends HTML, the page is visible but not interactive.

React then attaches event handlers in the browser.

Server HTML
      ↓
Browser displays page
      ↓
React attaches events
      ↓
Interactive page

Example:

<button onClick={handleClick}>
  Click Me
</button>

The button appears immediately from SSR, but becomes clickable after hydration.


---

How to Achieve CSR?

Using React + Vite

npm create vite@latest

Entry file:

ReactDOM.createRoot(root).render(<App />);

Everything renders in the browser.


---

How to Achieve SSR?

Using ReactDOMServer

import ReactDOMServer from "react-dom/server";

const html = ReactDOMServer.renderToString(
  <App />
);

Using Frameworks

The most common approach is:

[Next.js](https://nextjs.org?utm_source=chatgpt.com)

[Remix](https://remix.run?utm_source=chatgpt.com)


These frameworks handle:

Server rendering

Routing

Hydration

Data fetching



---

CSR vs SSR Comparison

Feature	CSR	SSR

Initial Load	Slower	Faster
SEO	Weak	Excellent
Server Cost	Low	Higher
Interactivity	Excellent	Excellent (after hydration)
First Content Paint	Slower	Faster
Complexity	Simple	More complex
Best For	Dashboards, SaaS apps	E-commerce, Blogs, Marketing



---

Modern React Approach

Modern React frameworks often use a hybrid approach.

For example, [Next.js](https://nextjs.org?utm_source=chatgpt.com) can:

SSR important pages for SEO

CSR interactive sections

Statically generate pages at build time (SSG)

Stream content progressively


This gives the benefits of both worlds:

Fast first load
+
Good SEO
+
Rich interactivity

That's why SSR frameworks like Next.js have become the preferred choice for many production React applications.
