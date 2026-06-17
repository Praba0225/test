In Angular, "caching" can happen at different layers:

1. Browser-level caching (HTTP cache)


2. Application-level caching (storing API responses in memory)


3. Service Worker caching (Progressive Web Apps)


4. State management caching (NgRx, Signals, etc.)


5. Route data caching (RouteReuseStrategy)


6. Observable caching (RxJS operators like shareReplay)


7. Persistent storage caching (localStorage, sessionStorage, IndexedDB)



Below is a detailed explanation of each strategy with examples.


---

1. HTTP Browser Caching

The browser stores API responses based on cache headers sent by the server.

How it works

Step 1: Client requests data

this.http.get('/api/products')

Step 2: Server sends cache headers

Cache-Control: max-age=3600
ETag: "abc123"

Step 3: Browser stores response

For the next request within 1 hour:

this.http.get('/api/products')

Browser may return cached data without contacting the server.

Benefits

Fastest strategy

No Angular code required

Reduces network traffic


Drawbacks

Controlled mainly by backend headers

Less control from Angular



---

2. In-Memory Service Caching

Store API responses inside Angular services.

How it works

Step 1: Create cache variable

@Injectable({
  providedIn: 'root'
})
export class ProductService {

  private productsCache: any[] | null = null;

  constructor(private http: HttpClient) {}

  getProducts() {

    if (this.productsCache) {
      return of(this.productsCache);
    }

    return this.http.get<any[]>('/api/products').pipe(
      tap(data => this.productsCache = data)
    );
  }
}

Step 2: First request

productService.getProducts();

Flow:

API Call
 ↓
Store in cache
 ↓
Return data

Step 3: Subsequent requests

Cache Exists?
   ↓ Yes
Return cached data

No API call occurs.

Benefits

Very simple

Good for lookup data


Drawbacks

Lost after page refresh



---

3. RxJS shareReplay Caching

One of the most common Angular caching strategies.

Problem

Without caching:

this.http.get('/api/users');

Every subscription triggers a new API call.

users$.subscribe();
users$.subscribe();
users$.subscribe();

Result:

API Call #1
API Call #2
API Call #3


---

Solution: shareReplay

@Injectable({
  providedIn: 'root'
})
export class UserService {

  users$ = this.http.get('/api/users').pipe(
    shareReplay(1)
  );

  constructor(private http: HttpClient) {}
}

First subscriber

this.userService.users$.subscribe();

API Request
 ↓
Response cached

Second subscriber

this.userService.users$.subscribe();

Uses cached response.

Result

One API call
Multiple consumers

Benefits

Elegant

Reactive

Most popular approach


Drawbacks

Need refresh mechanism.

refreshUsers() {
  this.users$ = this.http.get('/api/users')
    .pipe(shareReplay(1));
}


---

4. localStorage Caching

Cache survives browser refresh.

Step 1: Save data

localStorage.setItem(
  'products',
  JSON.stringify(products)
);


---

Step 2: Read data

const cachedData =
  localStorage.getItem('products');

if (cachedData) {
  return JSON.parse(cachedData);
}


---

Full Example

getProducts() {

  const cached =
    localStorage.getItem('products');

  if (cached) {
    return of(JSON.parse(cached));
  }

  return this.http.get('/api/products').pipe(
    tap(products => {
      localStorage.setItem(
        'products',
        JSON.stringify(products)
      );
    })
  );
}

Benefits

Survives refresh

Easy implementation


Drawbacks

Limited size (~5–10 MB)

Not secure



---

5. sessionStorage Caching

Similar to localStorage but removed when browser tab closes.

Store

sessionStorage.setItem(
  'user',
  JSON.stringify(user)
);

Read

const user =
  JSON.parse(sessionStorage.getItem('user')!);

Use Cases

Temporary user data

Multi-step forms

Shopping checkout flow



---

6. Service Worker Caching (PWA)

Angular provides built-in service worker support.

Step 1: Add PWA

ng add @angular/pwa

Creates:

ngsw-config.json


---

Step 2: Configure caching

{
  "assetGroups": [
    {
      "name": "app",
      "installMode": "prefetch",
      "resources": {
        "files": [
          "/index.html",
          "/*.css",
          "/*.js"
        ]
      }
    }
  ]
}


---

Step 3: Build

ng build --configuration production


---

How it works

User opens app
 ↓
Assets cached
 ↓
Offline available

Benefits

Offline support

Fast loading

Automatic asset caching



---

7. API Data Caching with Service Worker

Cache API responses too.

{
  "dataGroups": [
    {
      "name": "api-cache",
      "urls": [
        "/api/**"
      ],
      "cacheConfig": {
        "maxSize": 100,
        "maxAge": "1h",
        "strategy": "performance"
      }
    }
  ]
}


---

Strategy: Performance

Cache First
 ↓
If exists → Return cache
 ↓
Else → Network

Fastest response.


---

Strategy: Freshness

Network First
 ↓
Success → Return network
 ↓
Fail → Return cache

Best for frequently changing data.


---

8. RouteReuseStrategy

Cache entire component instances when navigating.

Problem

Navigate:

Products
 ↓
Details
 ↓
Products

Products component reloads every time.


---

Solution

Custom RouteReuseStrategy.

export class CustomReuseStrategy
  implements RouteReuseStrategy {

  storedRoutes = new Map();

  shouldDetach(route) {
    return true;
  }

  store(route, handle) {
    this.storedRoutes.set(route.routeConfig?.path, handle);
  }

  shouldAttach(route) {
    return this.storedRoutes.has(
      route.routeConfig?.path
    );
  }

  retrieve(route) {
    return this.storedRoutes.get(
      route.routeConfig?.path
    );
  }

  shouldReuseRoute(future, curr) {
    return future.routeConfig === curr.routeConfig;
  }
}

Benefits

Preserves scroll position

Preserves component state

Faster navigation



---

9. NgRx Store Caching

Store API responses in a centralized state.

Step 1

Load data once.

loadProducts()

↓

API

↓

Store


---

Step 2

Read from store.

this.store.select(selectProducts);

No API call.

Benefits

Scalable

Enterprise applications


Drawbacks

More setup



---

10. IndexedDB Caching

For large datasets.

Use libraries like:

npm install idb

Example:

import { openDB } from 'idb';

const db = await openDB('app-db', 1);

await db.put('products', data, 'all-products');

Read:

const data =
  await db.get('products', 'all-products');

Benefits

Hundreds of MBs possible

Offline capable


Ideal For

Large reports

Offline-first apps

Enterprise applications



---

Cache Invalidation Strategies

Caching is useful only if stale data is handled correctly.

Time-Based Expiration

{
  data: products,
  timestamp: Date.now()
}

Check:

const age =
  Date.now() - cache.timestamp;

if (age > 300000) {
  // refresh cache
}


---

Manual Refresh

refreshProducts() {
  this.cache = null;
}


---

Refresh After Mutation

addProduct(product) {
  return this.http.post('/api/products', product)
    .pipe(
      tap(() => this.cache = null)
    );
}


---

Which Strategy Should You Use?

Scenario	Recommended Strategy

Small API data	In-memory service cache
Multiple subscribers	shareReplay(1)
Survive refresh	localStorage
Session-specific data	sessionStorage
Offline support	Service Worker
Large datasets	IndexedDB
Enterprise apps	NgRx Store
Preserve page state	RouteReuseStrategy
Static assets	Browser + Service Worker cache


Common Real-World Combination

Many production Angular applications use:

Browser Cache
      +
shareReplay(1)
      +
localStorage
      +
Service Worker

This layered approach provides fast initial loads, fewer API calls, persistence across refreshes, and offline capability.
