What is Tree Shaking?

Tree shaking is a build optimization technique that removes unused code (dead code) from your application's final JavaScript bundle.

The name comes from the idea of shaking a tree so that dead leaves fall off, leaving only the code your application actually uses.


---

Why is Tree Shaking Important?

Suppose you import a library that contains 100 functions, but your application only uses 2 of them.

Without tree shaking:

Library
 ├── functionA
 ├── functionB
 ├── functionC
 ├── ...
 └── functionZ

All functions may end up in the final bundle.

With tree shaking:

Used:
 ├── functionA
 └── functionB

Removed:
 ├── functionC
 ├── functionD
 ├── ...
 └── functionZ

Result:

Smaller bundle size

Faster page load

Less JavaScript to parse and execute

Better performance



---

Example 1: Basic Tree Shaking

math.js

export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

export function multiply(a, b) {
  return a * b;
}

App.js

import { add } from "./math";

console.log(add(5, 3));

Production Build

The bundler sees:

subtract()
multiply()

are never used.

Final bundle becomes roughly:

function add(a, b) {
  return a + b;
}

console.log(add(5, 3));

Unused functions are removed.


---

How Tree Shaking Works

Tree shaking relies on ES Modules (ESM).

Good (ES Modules)

export const add = () => {};
export const subtract = () => {};

import { add } from "./math";

The bundler knows exactly which exports are used.


---

Bad (CommonJS)

module.exports = {
  add,
  subtract,
};

const math = require("./math");

With CommonJS, it's harder for bundlers to determine unused code, so tree shaking may not work effectively.


---

Example 2: React Component Tree Shaking

components.js

export function Header() {
  return <h1>Header</h1>;
}

export function Footer() {
  return <footer>Footer</footer>;
}

export function Sidebar() {
  return <aside>Sidebar</aside>;
}

App.jsx

import { Header } from "./components";

function App() {
  return <Header />;
}

During production build:

Footer
Sidebar

can be removed if they are never used.


---

Tree Shaking in React Projects

Modern React tools support tree shaking automatically:

Webpack

Vite

Rollup

Parcel


For example:

npm run build

creates an optimized production bundle where unused exports are removed.


---

Example 3: Importing Entire Library vs Specific Import

Bad

import _ from "lodash";

This may include much more code than needed.

Better

import debounce from "lodash/debounce";

or

import { debounce } from "lodash-es";

Only the required functionality is included.


---

Common Reasons Tree Shaking Fails

1. Using CommonJS

const utils = require("./utils");

Prefer:

import { formatDate } from "./utils";


---

2. Side Effects

utils.js

console.log("App started");

export function helper() {}

Because the file has a side effect (console.log), the bundler may keep it.


---

3. Importing Everything

import * as utils from "./utils";

The bundler may have less opportunity to remove unused parts.

Prefer:

import { formatDate } from "./utils";


---

How to Verify Tree Shaking

Build your project:

npm run build

Analyze the bundle using tools such as:

[Webpack Bundle Analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer?utm_source=chatgpt.com)

[Source Map Explorer](https://github.com/danvk/source-map-explorer?utm_source=chatgpt.com)


These tools show which modules are included in the final bundle and their sizes.


---

React Interview Answer (Short Version)

> Tree shaking is a build optimization technique that removes unused JavaScript code from the final bundle. It works primarily with ES module imports and exports. Bundlers such as Webpack, Vite, and Rollup analyze the dependency graph and eliminate code that is imported but never used, resulting in smaller bundles and better application performance.
