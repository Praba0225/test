A Service Worker is a special JavaScript file that runs separately from your web page, in the browser background, and acts as a programmable network proxy between your web app and the internet.

Think of it as a middleware layer inside the browser:

User
  ↓
Web Page (UI)
  ↓
Service Worker
  ↓
Network / Server

Because it sits between your application and the network, it can:

Intercept network requests

Cache files

Serve content offline

Enable push notifications

Perform background synchronization

Improve performance and reliability



---

Why Service Workers Exist

Before service workers:

Websites stopped working offline.

Developers had limited control over browser caching.

Background tasks were difficult.

Push notifications were mostly unavailable for websites.


Service workers solved these problems by giving web apps capabilities similar to native apps.


---

High-Level Architecture

A typical web application looks like:

index.html
app.js
styles.css

With a service worker:

Browser
│
├── Main Thread
│     ├── index.html
│     ├── React/Vue/Angular App
│     └── UI Logic
│
└── Service Worker Thread
      ├── Network interception
      ├── Cache management
      ├── Push notifications
      └── Background sync

The service worker runs in its own thread.

Important:

No DOM access

No window

No direct manipulation of page elements


It only handles browser APIs.


---

Lifecycle of a Service Worker

The lifecycle is one of the most important concepts.

There are three major stages:

Register
   ↓
Install
   ↓
Activate
   ↓
Fetch Events


---

Step 1: Registration

The page tells the browser to install a service worker.

if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js');
}

Browser downloads:

/sw.js

and starts installation.


---

What Happens Internally?

Browser stores:

Current Service Worker
New Service Worker

This allows safe updates without breaking active users.


---

Step 2: Install Event

Triggered once when the worker is first installed.

self.addEventListener('install', event => {
  console.log('Installed');
});

Usually used for caching assets.

Example:

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open('v1').then(cache => {
      return cache.addAll([
        '/',
        '/index.html',
        '/app.js',
        '/style.css'
      ]);
    })
  );
});

Browser downloads and stores these files.


---

Cache Storage

Service workers use the Cache Storage API.

Not the same as browser HTTP cache.

Cache Storage
│
├── v1
│    ├── index.html
│    ├── app.js
│    └── style.css
│
└── v2

Access:

caches.open('v1')

Store:

cache.put(request, response)

Read:

cache.match(request)

Delete:

caches.delete('v1')


---

Step 3: Activate Event

Runs after installation.

self.addEventListener('activate', event => {
  console.log('Activated');
});

Usually used to clean old caches.

Example:

self.addEventListener('activate', event => {
  event.waitUntil(
    caches.keys().then(keys => {
      return Promise.all(
        keys.map(key => {
          if (key !== 'v2') {
            return caches.delete(key);
          }
        })
      );
    })
  );
});


---

Why Install and Activate Are Separate

Suppose:

Current users -> SW v1
New deployment -> SW v2

You don't want active users suddenly switched.

Browser:

Install v2
Wait
All tabs closed
Activate v2

This ensures safe upgrades.


---

Service Worker Scope

Registration:

navigator.serviceWorker.register('/sw.js');

Scope:

/

Worker controls:

/
├── index.html
├── about
├── dashboard

If registered:

navigator.serviceWorker.register('/app/sw.js');

Scope becomes:

/app/*

Only those pages are controlled.


---

Fetch Event

This is the heart of service workers.

Whenever the page requests something:

fetch('/api/users')

the service worker can intercept it.

self.addEventListener('fetch', event => {
  console.log(event.request.url);
});

Flow:

Page
 ↓
Fetch Event
 ↓
Cache?
 ↓
Network?
 ↓
Response


---

Returning Cached Responses

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
  );
});

If found in cache:

Return cache

No network request.


---

Cache First Strategy

Popular for static assets.

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        return response || fetch(event.request);
      })
  );
});

Flow:

Cache
 ↓
Hit → Return
 ↓
Miss
 ↓
Network

Fastest strategy.


---

Network First Strategy

Good for APIs.

self.addEventListener('fetch', event => {
  event.respondWith(
    fetch(event.request)
      .catch(() => caches.match(event.request))
  );
});

Flow:

Network
 ↓
Success → Return
 ↓
Failure
 ↓
Cache

Ensures fresh data.


---

Stale While Revalidate

Used heavily by modern PWAs.

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(cached => {

        const fetchPromise = fetch(event.request)
          .then(networkResponse => {

            caches.open('v1').then(cache => {
              cache.put(event.request, networkResponse.clone());
            });

            return networkResponse;
          });

        return cached || fetchPromise;
      })
  );
});

Flow:

Cache → Immediate response

Background:
Network → Update cache

Best user experience.


---

Offline Support

Without service worker:

No Internet
 ↓
Request Fails

With service worker:

No Internet
 ↓
Cache
 ↓
Page Works

Example:

event.respondWith(
  caches.match(event.request)
    .then(response => {
      return response || fetch(event.request);
    })
);


---

Offline Fallback Page

self.addEventListener('fetch', event => {
  event.respondWith(
    fetch(event.request)
      .catch(() => caches.match('/offline.html'))
  );
});

If internet is unavailable:

offline.html

is served.


---

Push Notifications

Service workers can receive messages even when the site is closed.

self.addEventListener('push', event => {
  self.registration.showNotification(
    'New Message',
    {
      body: 'You received a new message.'
    }
  );
});

Server sends:

Push Service
 ↓
Browser
 ↓
Service Worker
 ↓
Notification


---

Notification Click Handling

self.addEventListener('notificationclick', event => {
  event.notification.close();

  event.waitUntil(
    clients.openWindow('/messages')
  );
});

Clicking notification opens page.


---

Background Sync

Suppose user submits a form offline.

Without sync:

Request fails
Data lost

With sync:

Queue request
Wait for internet
Send automatically

Example:

self.addEventListener('sync', event => {
  if (event.tag === 'send-message') {
    event.waitUntil(sendPendingMessages());
  }
});


---

Service Worker Update Process

Browser periodically checks:

sw.js

If changed:

Download new version
Install
Wait
Activate

Old version remains active until safe replacement.


---

Service Worker States

installing
   ↓
installed
   ↓
activating
   ↓
activated
   ↓
redundant

You can inspect:

navigator.serviceWorker.ready

or DevTools.


---

Communication Between Page and Service Worker

Page:

navigator.serviceWorker.controller.postMessage({
  type: 'PING'
});

Worker:

self.addEventListener('message', event => {
  console.log(event.data);
});

Used for:

cache updates

notifications

sync status

app events



---

Security Requirements

Service workers require HTTPS.

Allowed:

https://example.com

Not allowed:

http://example.com

Exception:

http://localhost

for development.

Reason:

A service worker can intercept all network traffic, so browsers require a secure origin.


---

Common Use Cases

Progressive Web Apps (PWAs)

Offline support:

Twitter Lite
Pinterest
Uber Web

E-commerce

Cache:

product pages

images

JS bundles


News Apps

Cache articles.

Messaging Apps

push notifications

background sync



---

Common Mistakes

1. Forgetting Response Clone

Wrong:

cache.put(req, response);
return response;

Response body gets consumed.

Correct:

cache.put(req, response.clone());
return response;


---

2. Caching Everything

Bad:

cache.addAll(['*']);

Can fill storage quickly.


---

3. Never Versioning Cache

Bad:

cache.open('cache');

Good:

cache.open('cache-v3');


---

Real-World Request Flow

Imagine a user opens:

https://myapp.com

Flow:

1. Browser loads page

2. Registers service worker

3. Service worker installs

4. Assets cached

5. Service worker activates

6. User requests app.js

7. Fetch event fires

8. Service worker checks cache

9. Cache hit

10. Returns cached app.js

11. Page loads instantly

Later:

Internet disconnected
 ↓
User reloads page
 ↓
Service worker serves cached files
 ↓
App still works


---

Mental Model

The simplest way to think about a service worker is:

> A service worker is a background JavaScript process that acts as a programmable proxy between your web application and the network. It intercepts requests, manages caches, enables offline experiences, handles push notifications, and performs background tasks independently of the web page.



The four concepts to master are:

1. Registration – telling the browser about the worker.


2. Install – pre-cache assets.


3. Activate – clean up and take control.


4. Fetch – intercept requests and decide whether to use cache, network, or both.



Once you understand those four stages, the rest of service worker functionality (offline apps, PWAs, push notifications, background sync, caching strategies, updates) becomes much easier to reason about.
