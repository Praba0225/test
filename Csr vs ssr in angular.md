In Angular, CSR (Client-Side Rendering) and SSR (Server-Side Rendering) describe where your HTML is generated and rendered.


---

1. Client-Side Rendering (CSR)

In CSR, the server sends a minimal HTML page and JavaScript bundles to the browser. Angular then runs in the browser and builds the UI.

Flow

Browser Request
      ↓
Server sends:
- index.html
- Angular JS bundles
      ↓
Browser downloads JS
      ↓
Angular bootstraps
      ↓
UI gets rendered

Example

Server initially returns:

<body>
  <app-root></app-root>
</body>

After Angular loads:

<body>
  <app-root>
    <h1>Products</h1>
  </app-root>
</body>

Advantages

Simpler deployment.

Rich interactive applications.

Less work for the server.

Good for authenticated dashboards and admin panels.


Disadvantages

Slower first page load.

SEO can be weaker because content appears after JavaScript executes.

Users may see a blank page while JS downloads.



---

2. Server-Side Rendering (SSR)

In SSR, Angular runs on the server first and generates complete HTML before sending it to the browser.

Flow

Browser Request
      ↓
Angular runs on server
      ↓
Server generates HTML
      ↓
Browser receives ready HTML
      ↓
Angular hydrates the page

Example

Server directly sends:

<body>
  <app-root>
    <h1>Products</h1>
  </app-root>
</body>

The user immediately sees content.

After that, Angular attaches event handlers and becomes interactive (hydration).

Advantages

Faster First Contentful Paint (FCP).

Better SEO.

Better social media previews.

Improved perceived performance.


Disadvantages

More server resources.

More complex setup.

Some browser-only APIs (window, document, localStorage) need special handling.



---

Why Do We Need SSR?

Consider an e-commerce site.

CSR

Request page
↓
Download JS (2-3 MB)
↓
Execute JS
↓
Fetch products
↓
Render page

The user waits before seeing products.

SSR

Request page
↓
Server renders products
↓
HTML returned immediately
↓
User sees content
↓
Angular hydrates

Benefits:

Search engines can crawl product pages easily.

Faster perceived loading.

Better Core Web Vitals.


Common SSR use cases:

E-commerce websites

Blogs

Marketing websites

News portals

Public-facing pages


Common CSR use cases:

Admin dashboards

Internal tools

Highly interactive applications after login



---

How to Enable SSR in Angular

Angular provides SSR through Angular SSR (formerly Angular Universal).

Create a new SSR app

ng new my-app --ssr

Add SSR to an existing app

ng add @angular/ssr

This generates server-related files such as:

server.ts
main.server.ts
app.config.server.ts

Run SSR:

npm run serve:ssr

Build SSR:

npm run build


---

Hydration in Angular SSR

Without hydration:

Server renders HTML
↓
Browser destroys HTML
↓
Angular re-renders everything

With hydration:

Server renders HTML
↓
Browser reuses existing DOM
↓
Angular attaches events

Enable hydration:

bootstrapApplication(AppComponent, {
  providers: [
    provideClientHydration()
  ]
});

Benefits:

Faster startup.

Less DOM manipulation.

Better performance.



---

Using Both CSR and SSR Together

Modern Angular applications often use SSR + Hydration.

Example:

Initial page load:
SSR
↓
Fast HTML delivery
↓
Hydration
↓
CSR takes over

This gives:

Fast first paint

Good SEO

Full Angular interactivity


This is the recommended approach for most public-facing Angular applications.


---

Quick Comparison

Feature	CSR	SSR

Rendering location	Browser	Server
Initial load speed	Slower	Faster
SEO	Limited	Excellent
Server load	Low	Higher
User sees content	After JS loads	Immediately
Best for	Dashboards, internal apps	E-commerce, blogs, marketing sites


Rule of thumb

Use CSR for authenticated applications such as admin portals and dashboards.

Use SSR + Hydration for public pages where SEO and fast initial loading matter.

Many modern Angular apps use SSR for the first request and CSR afterward, getting the benefits of both approaches.
