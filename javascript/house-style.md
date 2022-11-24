# JavaScript style guide

This document outlines the way we write JavaScript. It's a living style guide – it will grow as our practices do.

* [General principles](#general-principles)
  * [Progressively enhance](#progressively-enhance)
  * [Code for humans](#code-for-humans)
  * [Modules over monoliths](#modules-over-monoliths)
  * [Keep it simple](#keep-it-simple)
  * [Performant code](#performant-code)
* [Code style](#code-style)
  * [Linting](#linting)
  * [Comments](#comments)
  * [Asynchronicity](#asynchronicity)
    * [Things to consider](#things-to-consider)
    * [Tips](#tips)
      * [Awaiting multiple promises](#awaiting-multiple-promises)
      * [Multiple awaits in a one-liner](#multiple-awaits-in-a-one-liner)
      * [Arrow function syntax with await](#arrow-function-syntax-with-await)
      * [Fallback to promises](#fallback-to-promises)
    * [Further reading](#further-reading)
  * [Indentation](#indentation)
  * [White space](#white-space)
  * [Variables](#variables)
    * [Defining variables](#defining-variables)
    * [Use of var](#use-of-var)
  * [Functions](#functions)
    * [Pure functions](#pure-functions)
  * [Operators](#operators)
  * [Loops](#loops)
  * [Strict mode](#strict-mode)
* [Client-side JavaScript architecture](#client-side-javascript-architecture)
  * [Module architecture](#module-architecture)
    * [Configuration](#configuration)
    * [Imports](#imports)
  * [Events](#events)
    * [Events for related modules](#events-for-related-modules)
    * [Events for unrelated modules](#events-for-unrelated-modules)
  * [DOM binding](#dom-binding)
    * [Test hook attributes](#test-hook-attributes)
    * [Complex 2-way binding](#complex-2-way-binding)
    * [Client-side templating](#client-side-templating)
    * [Polyfills](#polyfills)
  * [Directory structure](#directory-structure)
    * [Components directory](#components-directory)
    * [Vendor directory](#vendor-directory)
    * [Utils directory](#utils-directory)
  * [Be careful when transpiling](#be-careful-when-transpiling)
    * [`for...of loops`, a common use case](#forof-loops-a-common-use-case)

## General principles

### Progressively enhance

JavaScript solutions must exist purely as a [progressive enhancement](../practices/progressive-enhancement.md) of existing functionality.

### Code for humans

Your JavaScript should always be optimised for readability first, as someone is going to have to maintain your code. Most of the rules in this style guide are here to help enforce this. See our [house style document](../practices/house-style.md) to understand the rationale behind enforcement of style.

Code should be self-documenting wherever possible. This means writing sensible method names and using variables which adequately describe the object in question. Assume no prior knowledge when somebody new starts to contribute to the codebase.

We _don't_ do this:

```js
function load(file, cb) {
    fs.readFile(file, function(e, config) {
        if (e) return cb(e);
        cb(null, process(config));
    });
}
```

We do this:

```js
function loadConfigFile(filePath, callback) {
    fs.readFile(filePath, function(error, fileContents) {
        if (error) {
            return callback(error);
        }
        const config = processConfig(fileContents);
        callback(null, config);
    });
}
```

### Modules over monoliths

Wherever possible, you should try to think in smaller single-purpose modules and functions. This encourages reuse and helps to [keep complexity down](https://en.wikipedia.org/wiki/Cyclomatic_complexity).

If code is generic and reusable you should aim to break it into a separate module which can be managed through npm or included in a project's `vendor` directory. We advocate open sourcing of these kinds of modules, and it's a good idea to have open sourcing in mind no matter what you're writing.

Often you'll find that the code you're writing is catered for by a third-party module. Whenever possible, install a dependency rather than reinventing the wheel.

### Keep it simple

We adhere to the [KISS](https://en.wikipedia.org/wiki/KISS_principle) principle. Unnecessarily complex/obtuse code completely goes against our rule of coding for humans. It's difficult to understand, slows us down, and reduces maintainability. Don't do it.

It is also important to remember that [duplication is far cheaper than the wrong abstraction](http://www.sandimetz.com/blog/2016/1/20/the-wrong-abstraction).

```js
// We don't do this
~~number;

// We do this
Math.floor(number);
```

```js
// We don't do this
function isOdd(number) {
    return !!(number & 1);
}

// We do this
function isOdd(number) {
    const mod = number % 2;
    return (mod !== 0);
}
```

```js
// We don't do this
foo ^= bar; bar ^= foo; foo ^= bar;

// We do this
const tempVar = foo;
foo = bar;
bar = tempVar;
```

### Performant code

We should always try to write fast code, but not if it makes the code difficult to understand. It's inefficient to optimise in favour of performance unless evidence shows that you really _need_ to do that.

If you're writing a small library with a single simple purpose, and you really _really_ need to do it, then it makes sense; in a project with more than one contributor, there's frequently more "cost" than "benefit".

Understanding [when to optimise](https://en.wikipedia.org/wiki/Program_optimization#When_to_optimize) is a valuable skill in software development.

## Code style

### Linting

Static analysis tools like linters can flag programming errors, bugs and stylistic errors, making your code more robust, readable and maintainable.

JavaScript code should be linted with [eslint](https://eslint.org/) using the [Springer Nature `eslint-config`](https://github.com/springernature/eslint-config-springernature). This configuration allows us to maintain consistency between different projects.

You can check the [README](https://github.com/springernature/eslint-config-springernature/blob/main/README.md) for details about installing and configuring the tools.

### Comments

Your JavaScript code should be self-documenting. Self-documenting code is easier to maintain, and simpler to read. Excessive comments can become out of sync with the usual code. Keep comments succinct & factual.

Where necessary, adjust the structure of your code to make it self-documenting, for example:

We do this:

```js
const isVisible = el.offsetWidth && el.offsetHeight;

if (isVisible) {}
```

We don't do this:

```js
if (el.offsetWidth && el.offsetHeight) {}
```

For code which is not self-documenting (e.g. magic numbers), leave a comment to explain intent & reasoning:

```js
// 42 is the only value the server can handle
fetch('https://example.com/?number=42')

// We must set items to null as a workaround for this bug: github.com/.....
window.items = null;
```

Do not explain code just because it uses new APIs, e.g.:

We don't do this:

```js
// Call a callback function in the next animation loop
requestAnimationFrame(() => {})
```

We don't do this:

```js

// Sets can filter out non-unique values for us
const uniqueIDs = new Set([1, 2, 1, 2]);
```

#### JS Doc

Although your JavaScript code should be self-documenting, it is highly
recommended to document your JavasScript application or library using the
Standardised [JS Doc](https://jsdoc.app/) format.

This format is leveraged by the Language Server Protocol (LSP), which is
supported in numerous editors and Integrated Development Environments (IDE)
nowadays.  
Thanks to LSP you get short lines of documentation right from the
invocation context. This helps you code quickly, while avoid obvious errors.

For functions for instance, you get:
- What it is intended to do
- The type, default value, and description of its parameters
- Which parameters are optional
- The function returned value type and description

Bonus: There are tools to generate a documentation website for your application
or library if it uses JS Doc.

A concrete and furnished example:

```js
/**
 * Get a list of books from given a library.
 *
 * @param {number} library - Id of the library.
 * @param {number} [limit=10] - Optional maximum of books expected to be returned, defaults to 10.
 * @param {object} [filters={}] - Optional filters, defaults to no filters.
 * @param {string} [filters.subject] - A string to match up the subject of the book.
 * @param {number} [filters.publicationyear] - Year the book was published.
 *
 * @returns {object[]} list of books from that library matching the optionally given filters.
 */
function getbooks(library, limit = 10, filters = {}) {
  // ...
}
```

### Asynchronicity

Many operations in JavaScript (both in the browser and Node.js) are asynchronous. If you need to access the result of an async operation, the API which you are using may offer the result to you through a callback that you provide.

Here is an example:

```js
ajax('https://example.com', response => {
    console.log(response)
});
```

If you need to execute another `ajax` request based on the result of the original, you might write code like this:

```js
ajax('https://example.com', response => {
    console.log(response); // { status: 200, url: 'https://...' }

    ajax(response.url, () => {
        console.log('Two ajax requests have completed')
    });
});
```

To avoid the journey to '[callback hell](http://callbackhell.com/)', you should aim to use [promise-based APIs](https://developers.google.com/web/fundamentals/getting-started/primers/promises). You can now convert the callback-based code to this:

```js
ajax('https://example.com').then(response => response.url).then(url => {
    ajax(url, () => {
        console.log('Two ajax requests have completed')
    });
})
```

Promises still use callbacks. To write synchronous-style code which performs asynchronous operations, you can use [async/await](https://twitter.com/addyosmani/status/756204943527129090). The above example can be rewritten to use `async/await`.

```js
const {url} = await ajax('https://example.com');
await ajax(url);
console.log('Two ajax requests have completed')
```

#### Things to consider

* `async/await` has limited [browser support](http://caniuse.com/#feat=async-functions), you might need to use a [transpiler](https://babeljs.io/docs/plugins/transform-async-to-generator/) to gain cross-browser support.
* You might ship a larger JavaScript payload to your users by converting an `async` function. Profile your website to evaluate if this is worth it.
* The `async` in `async/await` refers to the fact that the `await` keyword can only appear in a function prefixed with the `async` keyword.
* If the API you would like to `await` for does not offer a promise-based API, you can't `await` the API call. Consider [converting the API to use promises](https://www.npmjs.com/package/es6-promisify).

#### Tips

##### Awaiting multiple promises

You can `await` multiple promises:

```js
const [response1, response2] = await Promise.all([promise1, promise2]);
```

##### Multiple awaits in a one-liner

You can wrap the `await` + function call in parentheses to enable calls like this:

```js
await (await fetch('http://numbersapi.com/random/year?json')).json()
```

##### Arrow function syntax with await

You can use `async` functions with the arrow function syntax:

```js
[1, 2, 3].map(async num => {

})
```

##### Fallback to promises

This code snippet highlights two things:

* Since `async/await` uses promises, you can continue to use `then()` callbacks where it makes sense, for example outside of an `async` function.
* All `async` functions return promises. No matter what value you explicitly return, it will still be wrapped in a promise.

```js
async function five() {
    return Promise.resolve(5);
}

async function six() {
    return 1 + await five();
}

six().then(result => {
    console.log(result); // 6
});
```

#### Further reading

Practical code examples, including error handling examples, can be read here: [Async functions - making promises friendly](https://developers.google.com/web/fundamentals/getting-started/primers/async-functions)

### Indentation

Ensure indentation consistency is maintained with a tool such as [EditorConfig](http://editorconfig.org/). Using this tool, you can specify indentation settings for your codebase. Team members should then install the corresponding plugin for their editor. E.g. [atom-editorconfig](https://github.com/sindresorhus/atom-editorconfig#readme), [vscode-editor-config](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

Except in package.json files, we indent our JavaScript using single tabs, not spaces. You can convert characters automatically in most editors, and you're advised to do this.

Follow the [BSD-KNF](https://en.wikipedia.org/wiki/Indent_style#Variant:_BSD_KNF) indentation style.

We do this:

```js
if (foo) {
    console.log(foo);
} else {
    console.log(bar);
}
```

We _don't_ do this:

```js
if (foo)
{
    console.log(foo);
}
else
{
    console.log(bar);
}

if (foo) {
        console.log(foo);
} else {
        console.log(bar);
}
```

Some tools (like NPM or Snyk) have the ability to rewrite all or part of the `package.json` file. The majority of these tools expect the `package.json` file to be indented with two spaces. Please follow this convention in your `package.json` files to avoid irritating merges when the output of such a tool is part of a Pull Request.

### White space

We use white space liberally to help keep code readable. You're encouraged to use newlines to break up long functions into logical chunks.

You should also remove trailing white space from lines of code. Your editor should be able to either remove this or highlight it when present, for example, [atom-whitespace](https://github.com/atom/whitespace), [vscode-trailing-spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces).

### Variables

#### Defining variables

We define variables with multiple `const` and `let` statements.

We do this:

```js
const foo = 1;
const bar = 2;
```

```js
let foo = 1;
let bar = 2;
```

We _don't_ do this:

```js
const foo = 1,
      bar = 2;
```

```js
let foo = 1,
    bar = 2;
```

We use `let` only when a variable _explicitly_ [needs to be mutable](https://ada.is/blog/2015/07/13/immutable/):

We do this:

```js
let foo = 1;

if (foo) {
    foo += 1;
}
```

```js
const foo = [1,2];

if (bar) {
    foo.push(3);
}
```

We _don't_ do this:

```js
let foo = [1,2];

if (bar) {
    foo.push(3);
}
```

#### Use of var

If you have to use `var` instead of `const` and `let` (because your environment doesn't support ES2015 (Node.js 4.x/[Babel](https://babeljs.io/))), you need to understand [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting).
Avoid defining variables inside loops or blocks.

We do this:

```js
var foo = 1;
var bar = 2;

var baz;
if (foo === bar) {
    baz = 3;
}
```

We _don't_ do this:

```js
var foo = 1,
    bar = 2;

if (foo === bar) {
    var baz = 3;
}
```

### Functions

We use lowerCamelCase naming for functions, and functions should be named descriptively.

Functions are not allowed to be written on a single line – you must always follow our [indentation](#indentation) rules.

We do this:

```js
const loadConfig = function(filePaths, callback) {
    // ...
}

function loadConfig(filePaths, callback) {
    // ...
}
```

We _don't_ do this:

```js
const loadconfig = function(filePaths, callback) {
    // ...
}

function loadconfig(filePaths, callback) {
    // ...
}
```

#### Pure functions

Where possible, keep your [JavaScript functions pure](http://alistapart.com/article/making-your-javascript-pure).

We do this:

```js
function greet(greeting, subject) {
    return `${greeting}, ${subject}`;
}

greet('Hello', 'friend')
```

We _don't_ do this:

```js
const greeting = 'Hello';

function greet(subject) {
    return `${greeting}, ${subject}`;
}

greet('friend')
```

### Operators

We disallow the use of normal equal and not equal, requiring you to use the strict equivalents.

We do this:

```js
foo === bar;
foo !== bar;
```

We _don't_ do this:

```js
foo == bar;
foo != bar;
```

### Loops

In `for...in` loops, there must be a check with `hasOwnProperty`.

We do this:

```js
for (const prop in obj) {
    if (Object.prototype.hasOwnProperty.call(obj, prop)) {
        // ...
    }
}
```

We _don't_ do this:

```js
for (const prop in obj) {
    // ...
}
```

### Strict mode

You should assume that your code will fail, and take steps to handle those failures.

Where [ES5 and above is available and strict mode is implemented](http://kangax.github.io/compat-table/es5/), use strict mode: `'use strict';` This causes JavaScript to error early rather than allow malformed or incorrect code to run.

In Node.js, you can add `'use strict';` to the top of each of your source files.

In-browser you should not add your `'use strict';` to the top of the file; instead you should add it to either the file's [IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) or each defined function if an IIFE isn't present. This is because global strict mode in browsers can cause issues with third-party code.

We do this:

```js
(function () {
    'use strict';
    // ...
})();
```

Client-side JavaScript architecture
-----------------------------------

Write small, isolated & well tested JavaScript modules.

### Module architecture

The JavaScript in your application should consist of one or more entry points and "modules". For example, you might have a module which is only responsible for one of the following:

- An autocomplete module.
- A module which handles all analytics events.
- A module which implements sticky header functionality.

Your module should use named exports for all exports.

We do this:

```js
export {init};
```

We _don't_ do this:

```js
export default init;
```


Your module should expose an `init` method which is consumed by the entry point of your application:

```js
// my-module-1.js

import {otherModule} from './some-other-module-you-need';

function addEventListeners() {}

function init() {
    otherModule();
    addEventListeners();
}

export {init};
```

Your modules are to be _consumed_ by your entry point:

```js
// main.js

import {module1} from './my-module-1.js';
import {module2} from './my-module-2.js';
import {module3} from './my-module-3.js';

document.addEventListener('DOMContentLoaded', function(event) {
    module1.init();
    module2.init();
    module3.init();
});
```

This approach is:

- Easy to read and intuitive.
- Standards compliant (ES2015 module syntax - import and export).
- Adherent to clean code practices as the `main.js` file only becomes an orchestrator, and it is kept free of logic. It has one job, which is to invoke other smaller modules.
- Useful for unit testing as the small isoloated modules are easy to test.

#### Configuration

If you need to pass in configuration to a module, pass in an object:

```js
import {module1} from './my-module-1.js';

module1.init({
    url: 'https://...'
});
```

Your module code should handle configuration appropriately, and be resilient towards missing inputs:

```js
function module({url = 'https://...', animate = false}) {
    console.log(url, animate)
}

export {module};
```

#### Imports

You must export items to allow the consumer to import __only what is needed__. This helps prepare you for bundling techniques like tree-shaking.

We do this:

```js
import { flatten, merge } from 'lodash';
```

We don't do this:

```js
import _ from 'lodash';

const flatten = _.flatten;
const merge = _.merge;
```

### Events

Modules which are related to each other, and modules which are not, should communicate in different ways.

#### Events for related modules

Expose an API:

```js
// easings.js

function isValid(easing) {
    // Logic here
}

function get(easing) {
    // Logic here
}

export { get, isValid };
```

Then consume the API:

```js
// animations.js

import {easings} from './easings';

function init({element, easing}) {
    if (easings.isValid(easing)) {
        element.animate(easings.get(easing))
    } else {
        element.animate()
    }
}

export {init};
```

#### Events for unrelated modules

Use the [`createEvent` module](https://github.com/springernature/frontend-toolkits/tree/master/context/brand-context/default/js#createevent) from the Springer Nature Elements toolkit. This module functions as a namespaced wrapper around Javascript `customEvent`.

One limitation of using the existing infrastructure that Javascript provides — the ability to create an `Event` and consume using `addEventListener` — instead of a [PubSub](https://addyosmani.com/blog/understanding-the-publishsubscribe-pattern-for-greater-javascript-scalability/) style implementation, is that you have to hang the event handler off a `DOM Element` or the `window`.

In the case of two unrelated modules, this would mean that if `moduleA` publishes an event, then `moduleB` would have no knowledge of the DOM element that the event is bound to. This is solved by having your application manage event listeners, and keeping your modules fully isolated with no knowledge of other modules; for example:

```js
// Module A
// Relevant excerpt only
const event = createEvent('event', 'component', {
    detail: {
        hazcheeseburger: true
    }
});
moduleAelement.dispatchEvent(event);
```

```js
// Module B
// Relevant excerpt only
function doSomething(detail) {
    if (detail.hazcheeseburger) {
        // Do something
    }
}
```

```js
// Application
import {moduleA} from '@springernature/moduleA';
import {moduleB} from '@springernature/moduleB';

const moduleAelement = document.querySelector('[data-component-module-a]');
const moduleBelement = document.querySelector('[data-component-module-b]');

moduleA.init(moduleAelement);
moduleB.init(moduleBelement);

moduleAelement.addEventListener('component:event', function (event) {
    moduleB.doSomething(event.detail);
}, false);
```

### DOM binding

When it comes time to attach your [JavaScript module](#module-architecture) to a specific DOM element (or collection of elements), we favour the use of descriptive `data-component` attributes in the markup rather than using specific class names or ids.

We do this:

```html
<button class="c-button" data-component-collapse-activator="header-menu">Menu</button>
<nav class="c-header-menu u-hidden" data-component-collapse-target="header-menu">
    (etc.)
</nav>
```

We don't do this:

```html
<button class="c-button" data-component="collapse" data-target="header-menu">Menu</button>
<nav class="c-header-menu u-hidden" id="header-menu">
    (etc.)
</nav>
```

As demonstrated above, we use `data-component` attributes to label any elements that are being bound by the JavaScript. We structure the name of the attribute to include the component's name and where we feel necessary we follow with any words that help describe it's purpose. In the above example the component name is `collapse` and the words `activator` and `target` assist others in understanding what the attributes are being used for in the context of that component. This structure makes it easier for another person to understand an implementation by looking at the html alone and lessens the need for investigations whilst refactoring. We recommend that you carefully choose words that mean something to an outsider who has no pre-existing knowledge of the component's implementation.

Initialising a module can then be achieved simply by passing in one of more elements that match these selectors;

```js
const moduleInstances = document.querySelectorAll('[data-component-collapse-activator]');
if (moduleInstances.length > 0) {
    myCollapseModule.init(moduleInstances);
}
```

Alternatively for more complex modules that need to be bound to multiple DOM elements, it may make more sense to have the module itself contain a set of default selectors which can then be (optionally) overridden in the init call;

```js
function init(settings) {
    const defaults = {
        wrapper: '[data-component-complex-module]',
        close: '[data-component-complex-module-close]'
    };
    const selectors = Object.assign({}, defaults, settings)
}

export {init};
```

```js
myComplexModule.init({
    wrapper: '[data-component-renamed-complex-module]',
    close: '[data-component-renamed-complex-module-close]'
});
```

#### Test hook attributes

Implicity coupling markup and test code is brittle and to be avoided. This means avoiding the use of pre-existing classes and ID's as selectors in your test code. Instead, we prefer explicitly stating the coupling by using e.g. `data-test="component-name"` in your markup and `[data-test="component-name"]` as a selector in your test code.

In this way developers can refactor their CSS & templates safe in the knowledge they are not accidentally breaking any tests.

The downside to this is markup bloat &mdash; however internally we have solutions for dynamically removing these attributes so they are not served to the client.

#### Complex 2-way binding

If your project makes heavy use of DOM-manipulating JavaScript (and you can justify the performance penalty your users will pay for the download + execution of your script) then a JavaScript framework might make sense. Consider something small like [Preact](https://github.com/developit/preact). Using a JavaScript framework can handle DOM binding efficiently.

Bear in mind all solutions must form part of a robust, [progressively-enhanced]((../practices/progressive-enhancement.md)) solution.

For the majority of websites, especially those which may by viewed on low powered devices, you should minimise the JavaScript you send down the wire and implement DOM binding yourself. For simple use cases, manually cherry picking elements out of the DOM and reading/setting attributes on them is a reasonable approach.

#### Client-side templating

Client-side templating is typically to be avoided - e.g. in the example of an AJAX search response, render the HTML server-side and return an HTML fragment. It is much more efficient to use `innerHTML` than template a JSON response.

#### Polyfills

An example polyfill might add `requestAnimationFrame` for any grade-A browsers which don't support it.

If you utilise a Polyfill, the JavaScript must meet these conditions:

  - It must _not_ override native browser functionality
  - It must match native browser functionality exactly (where possible)
  - It can be either third-party, or written in-house
  - Must be installed via NPM (or dynamically via [polyfill.io](https://polyfill.io/v2/docs/), at your discretion).

Note that `polyfill.io` adds one additional blocking HTTP request, and if loading asynchronously one must be careful to manage the loading order of scripts.  So please consider the performance impact of using `polyfill.io` versus the maintenance overhead of bundling polyfills with your main application code.

If your project is JS-heavy you may wish to consider adding third-party code like polyfills, to a separate `vendor.js` bundle which is not part of your `main.js` entry point — the reasoning being the `vendor.js` bundle will change less frequently and is more likely to be cached by the client. If your visitors are unlikely to have primed caches, one bundle would probably be the better option.

### Directory structure

Client-Side JavaScript normally lives in `resources/js` in our projects, unless the back-end you're using dictates a different directory. Stick to this as closely as possible.

Within this directory, you should use the following structure.

```
<root>
  ├── components
  ├── utils
  └── vendor
  └── main.js
  └── vendor.js (optional)
```

File names in these directories should be lower-case, with words separated by dashes.

#### Components directory

The `components` directory is used to house JavaScript that couples to the DOM. There are several conditions that need to be met for a file to live in here:

  - It must bind to the DOM
  - It must add behaviour to and/or manipulates the DOM

An example component might be an autocomplete, tab group, or loading spinner.

#### Vendor directory

The `vendor` directory is where third-party code lives. You should only commit third party code to version control when you are unable to use a version from the NPM registry. Alternatively, code written in-house but managed and versioned elsewhere can live here, e.g. as an open source project.

JavaScript in this directory must meet these conditions:

  - It must be maintained outside of the project, e.g. as an open-source library
  - It's file name must contain the version of the code
  - It must include a link to the original source code in a comment
  - It must _not_ be modified within the project

#### Utils directory

The `utils` directory is used to house JavaScript written for the project that doesn't fit into the rules for the `components` directory. Utilities still have some conditions of their own:

  - It must _not_ bind to the DOM
  - It must _not_ add behaviour to and/or manipulate the DOM
  - It must _not_ be destructive – arguments passed in cannot be modified
  - It can expose functions and/or prototypal classes

An example utility might be a function to make a string title-case.

### Be careful when transpiling

As enticing as it can be to use modern Javascript syntax, it remains the
developers responsibility to ensure the developer experience does not negatively
impact the user experience, e.g. by decreasing performance.
Transpiling can easily increase the JavaScript bundle size, by incorporating
polyfills to for supported browsers.

There are two ways of avoiding an increase in bundle size:
1. Monitoring, with tools like [BabelREPL](https://babeljs.io/repl/), which show
   the size of your transpiled code.
2. Using "older" JavaScript syntax to achieve the same effect. An example of
   this is given below.

#### `for...of loops`, a common use case

We _don't_ do this:

```js
const list = document.querySelectorAll('input[type=checkbox]');
for (let checkbox of list) {
    // ..
}
```

We do this:

```js
const list = document.querySelectorAll('input[type=checkbox]');
Array.prototype.forEach.call(list, function (checkbox) {
    // ...
});
```

If you would run the above "We don't do this" snippet in [Babel REPL](https://babeljs.io/repl/),
using our [browserslist](https://github.com/springernature/frontend-playbook/blob/main/practices/graded-browser-support.md#browerslist),
it transpiles down to 23 lines, whereas the "We do this" snippet
transpiles down to 5 lines.  If you multiply this by the amount of
occurences of `for...of` in your code base, this can quickly get out of control.

Further reading:
- [Transpiled for-of Loops are Bad for the Client, by Dave Ruppert](https://daverupert.com/2017/10/for-of-loops-are-bad/).
- [Avoiding Babel’s Production Bloat](https://webreflection.medium.com/avoiding-babels-production-bloat-d53eea2e1cbf)
