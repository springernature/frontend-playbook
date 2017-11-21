# JavaScript style guide

This document outlines the way we write JavaScript. It's a living styleguide – it will grow as our practices do.

- [General principles](#general-principles)
  - [Progressively enhance](#progressively-enhance)
  - [Write code for humans](#code-for-humans)
  - [Write modules over monoliths](#modules-over-monoliths)
  - [KISS](#keep-it-simple)
  - [Performant code](#performant-code)
- [Code style](#code-style)
  - [Linting](#linting)
  - [Comments](#comments)
  - [Asynchronicity](#asynchronicity)
  - [Indentation](#indentation)
  - [White space](#white-space)
  - [Semi-colons](#semi-colons)
  - [Variables](#variables)
  - [Functions](#functions)
  - [Classes](#classes)
  - [Operators](#operators)
  - [Blocks](#blocks)
    - [Conditionals](#conditionals)
    - [Loops](#loops)
    - [Error handling](#error-handling)
  - [Strict mode](#strict-mode)
- [Client-side JavaScript architecture](#client-side-javascript-architecture)
  - [Module architecture](#module-architecture)
    - [Configuration](#configuration)
    - [Imports](#imports)
  - [Events](#events)
    - [Events for related modules](#events-for-related-modules)
    - [Events for unrelated modules](#events-for-unrelated-modules)
  - [DOM binding](#dom-binding)
  - [Polyfills](#polyfills)
  - [Directory structure](#directory-structure)
    - [Components directory](#components-directory)
    - [Vendor directory](#vendor-directory)
    - [Utils directory](#utils-directory)

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
        var config = processConfig(fileContents);
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

Code style
---------

### Linting

JavaScript code should be linted with the most recent version of [XO](https://github.com/sindresorhus/xo), using the default lint settings. XO uses [eslint](http://eslint.org/) under the hood.

If you are using ES2015+ syntax, XO provides [configuration](https://github.com/sindresorhus/xo#esnext) to enforce relevant rules. Add this in your `package.json` to enable it:

```js
"xo": {
  "esnext": true
}
```

Consider the following scenario: Assume the `semicolon` rule is `on`, if you omit a semicolon from your JavaScript code, it is suggested the following actions occur:

1. Your code editor should inform you of this linting failure. There are [XO plugins](https://github.com/sindresorhus/xo#editor-plugins) for popular editors such as [Sublime Text](https://github.com/sindresorhus/SublimeLinter-contrib-xo) and [Atom](https://github.com/sindresorhus/atom-linter-xo).
2. Your local `watch` tasks, e.g. those run through Grunt, Gulp, Make etc. inform you of this error in your terminal. There are [XO plugins](https://github.com/sindresorhus/xo#build-system-plugins) for [Grunt](https://github.com/sindresorhus/grunt-xo), [Gulp](https://github.com/sindresorhus/gulp-xo) and the [CLI](https://github.com/sindresorhus/xo#install).
3. When you push code which fails to lint, your build pipeline should invoke XO as part of a build task. The job should then fail.

#### Automatically fixing code

You can use XO as a command line tool. Once you install it, XO can automatically fix _some_ linting failures. Given a file `file.js` which contains the following:

```js
const object = {
    foo:function(){}
}
```

You can run XO with the `fix` option: `xo --fix file.js`. The same file now contains this:

```js
const object = {
    foo: function () {}
};
```

#### Disabling rules

XO provides a sane set of [sensible defaults](https://github.com/sindresorhus/eslint-config-xo/blob/b61bee396a67e2ea8e2fd9ae34bad36c9143cb15/index.js#L16-L264), it is unnecessary to disable rules according to your personal preferences.

If you feel the need to disable a rule, you should:

- Understand why the rule exists in the first place. For example the [no-unassigned-import](https://github.com/benmosher/eslint-plugin-import/blob/bd0e5e3dd5781b125dc02971ddb011aaa554bf4f/docs/rules/no-unassigned-import.md) rule provides: a readable description + pass/fail code examples.
- Raise it with your team, providing a compelling reason to disable a rule.

To disable a rule, wrap the offending code in `eslint-disable` directives, for example:

```js
/* eslint-disable no-unassigned-import */
require('polyfill');
/* eslint-enable no-unassigned-import */
```

Do not switch rules off permanently in a project unless you have a strong reason for doing so. If you do have a strong reason, ensure you have discussed this with your team beforehand.

Switching off a rule _permanently_ can present some problems:
-  You introduce potential inconsistencies within a single project.
-  You become subject to JavaScript quirks which a linter would typically warn you of. (Does not apply to stylistic rules)
-  You forget to enable the rule again when the offending code is removed from the codebase.
-  You mask the original reason and context as to why the rule was disabled in the first place. (You can improve this point with comments)

#### Questions and answers

Q: XO is complaining about the following code:

```js
adsProvider.load();
```

It says `adsProvider` is not defined, but it's a global variable already present in the page. What should I do?

A: This breaks the [no-undef](http://eslint.org/docs/rules/no-undef) rule of ESLint. You must specify to ESLint that this is an expected global variable. Do not define this project-wide, but rather, be explicit about which file or files need it.

```js
/* global adsProvider */
```

Q: I just added XO into the build, now everything is failing the linting process.

A: If your codebase has never been linted before, you might find rules being broken in each file. Fixing large amounts of code to pass linting may not be possible to do in one go. As a team, consider adopting an approach to successfully lint each file you touch as part of regular feature development. During this period, alter your build task accordingly to only lint files which you know you have linted. E.g.

```js
gulp.task('lint', () =>
    gulp.src([
      'js/file1.js',
      'js/file2.js'
    ])
    .pipe(xo())
);
```

Q: XO is complaining about undefined variables in my JavaScript unit test code.

A: XO supports many [popular environment global variables](http://eslint.org/docs/user-guide/configuring#specifying-environments). Specify an environment of your choice to add the necessary global variables. Combine this with [Config Overrides](https://github.com/sindresorhus/xo#config-overrides) to ensure you don't apply one or many environments to your entire codebase accidentally.

Q: I transformed my code to adhere to XO, but now it is less readable.

A: Code linting should help improve your overall code quality. If you now have less readable code, consider if there is a [code smell](https://en.wikipedia.org/wiki/Code_smell) that is conducive to breaking a lint rule, if so, you might need to refactor your code.

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

#### Things to consider:

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

##### Arrow function sytax with await

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

Ensure indentation consistency is maintained with a tool such as [EditorConfig](http://editorconfig.org/). Using this tool, you can specify indentation settings for your codebase. Team members should then install the corresponding plugin for their editor. E.g. [atom-editorconfig](https://github.com/sindresorhus/atom-editorconfig#readme)

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

We use automated tools (like Snyk) to monitor the status of dependencies in our package.json files. The majority of these tools expect two spaces for indentation, not tabs. Follow this convention in your package.json files to avoid irritating merges when one of the tools raises an automatic Pull Request. 

### White space

We use white space liberally to help keep code readable. You're encouraged to use newlines to break up long functions into logical chunks.

You should also remove trailing white space from lines of code. Your editor should be able to either remove this or highlight it when present, for example, [atom-whitespace](https://github.com/atom/whitespace).

### Semi-colons

We require the use of semi-colons. The only statements that don't need to end with semi-colons are function declarations and blocks.

We do this:

```js
var foo = 1;

if (foo) {
    foo += 1;
}

function bar() {
    // ...
}

var baz = function() {
    // ...
};
```

We _don't_ do this:

```js
var foo = 1

if (foo) {
    foo += 1
};

function bar() {
    // ...
};

var baz = function() {
    // ...
}
```

### Variables

We define variables with multiple `var` statements and trust our developers to understand [hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting). We generally discourage defining variables inside loops or blocks.

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

If the environment you're running in supports ES2015 (Node.js 4.x/[Babel](https://babeljs.io/)) then you should not use `var` statements at all – you should be using `let` and `const`:

In ES2015 we do this:

```js
const foo = 'bar';
```

We use `let` only when a variable _explicitly_ [needs to be mutable](https://ada.is/blog/2015/07/13/immutable/):

```js
let foo = 'bar';
```

In ES2015 we _don't_ do this:

```js
var foo = 'bar';
```

You can also use destructuring assignment with objects and arrays. These don't have to be multi-line, but there must be spaces after the commas:

```js
let {foo, bar} = getFooAndBar();
let [baz, qux] = getBazAndQux();
```

### Functions

We use lowerCamelCase naming for functions, and functions should be named descriptively.

Functions are not allowed to be written on a single line – you must always follow our [indentation](#indentation) rules.

Whitespace in functions is different to in blocks: there must be no space between the function declaration and the opening arguments bracket.

We do this:

```js
var loadConfig = function(filePaths, callback) {
    // ...
}

function loadConfig(filePaths, callback) {
    // ...
}
```

We _don't_ do this:

```js
var loadConfig = function (filePaths, callback) {
    // ...
}

function loadConfig(filePaths, callback){ /* ... */ }
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

#### Arguments

Arguments must be separated from the preceding comma by a space, and there should be no padding whitespace at the start and end of the arguments.

We do this:

```js
var loadConfig = function(filePaths, callback) {
    // ...
}
```

We _don't_ do this:

```js
var loadConfig = function(filePaths,callback) {
    // ...
}
```

If the environment you're running in supports ES2015 (Node.js 4.x/[Babel](https://babeljs.io/)) then you can use rest and default arguments.

Default and rest arguments must follow the same spacing rules as other arguments and regular variable assignment.

We do this:

```js
var sayHello = function(person = 'World', ...others) {
    // ...
}
```

We _don't_ do this:

```js
var sayHello = function(person="world",...others) {
    // ...
}
```

### Classes

If the environment you're running in supports ES2015 (Node.js 4.x/[Babel](https://babeljs.io/)) then you can use classes. Classes and their methods must be indented in the same way as functions. Also methods should be spaced apart.

We do this:

```js
class Apple extends Fruit {
    constructor() {
        this.color = 'red';
    }

    peel() {
        // ...
    }
}
```

We _don't_ do this:

```js
class Apple extends Fruit{
    constructor(){ this.color = 'red'; }
    peel () {
        // ...
    }
}
```

### Operators

All operators must have padding whitespace on either side of them. The only exceptions are increment (`++`), decrement (`--`), unary negation (`-foo`), and unary plus (`+foo`).

We disallow the use of normal equal and not equal, requiring you to use the strict equivalents.

We do this:

```js
foo === bar;
foo !== bar;
foo += bar;
baz = 'hello ' + qux;
foo++;
```

We _don't_ do this:

```js
foo == bar;
foo != bar;
foo+=bar;
baz = 'hello '+qux;
foo ++;
```

### Blocks

All blocks must use curly braces and are not allowed to be written on a single line – see the [indentation](#indentation) rules.

Blocks must also have padding whitespace on both sides (unless it's at the start of a line).

If a block requires brackets, there must be padding whitespace between the brackets and the keyword as well as the opening curly brace.

#### Conditionals

In conditionals, `else` blocks must start on the same line as the end curly brace of the `if`.

We do this:

```js
if (foo) {
    foo += 1;
}

if (foo) {
    foo += 1;
} else {
    bar += 1;
}
```

We _don't_ do this:

```js
if(foo){
    foo += 1;
}

if (foo) { foo += 1; }

if (foo) return;

if (foo) {
    foo += 1;
}
else {
    bar += 1;
}
```

#### Loops

In `for` loops, there must be space after the semi-colons.

`for..in` loops must include a check with `hasOwnProperty`.

We do this:

```js
for (let i = 0; i < 10; i += 1) {
    // ...
}

for (const prop in obj) {
    if (obj.hasOwnProperty(prop)) {
        // ...
    }
}
```

We _don't_ do this:

```js
for (let i = 0;i < 10;i += 1) // ...

for (const prop in obj) {
    // ...
}
```

#### Error handling

`try/catch` blocks must be indented in the same way as conditionals, with `catch` starting on the same line as the end curly brace of the `try`.

We do this:

```js
try {
    foo += 1;
} catch (error) {
    console.log(error);
}
```

We _don't_ do this:

```js
try {
    foo += 1;
}
catch (error) {
    console.log(error);
}

try { foo += 1; }
catch (error) { console.log(error); }
```

### Strict mode

You should assume that your code will fail, and take steps to handle those failures.

Where [ES5 and above is available and strict mode is implemented](http://kangax.github.io/compat-table/es5/), use strict mode: `'use strict';` This causes JavaScript to error early rather than allow malformed or incorrect code to run.

In Node.js, you can add `'use strict';` to the top of each of your source files.

In-browser you should not add your `'use strict';` to the top of the file; instead you should add it to either the file's [IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/) or each defined function if an IIFE isn't present. This is because global strict mode in browsers can cause issues with third-party code.

Client-side JavaScript architecture
-----------------------------------

Write small, isolated & well tested JavaScript modules.

### Module Architecture

The JavaScript in your application should consist of one or more entry points and "modules". For example, you might have a module which is only responsible for one of the following:

- An autocomplete module.
- A module which handles all analytics events.
- A module which implements sticky header functionality.

Your module should expose an `init` method which is consumed by the entry point of your application:

```js
// my-module-1.js

import otherModule from './some-other-module-you-need';

function addEventListeners() {}

function init() {
   otherModule();
   addEventListeners();
}

exports default { init };
```

Your modules are to be _consumed_ by your entry point:

```js
// main.js

import module1 from './my-module-1.js';
import module2 from './my-module-2.js';
import module3 from './my-module-3.js';

document.addEventListener('DOMContentLoaded', function(event) {
  module1.init();
  module2.init();
  module3.init();
});
```

This approach is:

- Easy to read and intuitive.
- Standards compliant (ES2015 module syntax - import and exports).
- Adherent to clean code practices as the `main.js` file only becomes an orchestrator, and it is kept free of logic. It has one job, which is to invoke other smaller modules.
- Useful for unit testing as the small isoloated modules are easy to test.

#### Configuration

If you need to pass in configuration to a module, pass in an object:

```js
import module1 from './my-module-1.js';

module1.init({
  url: 'https://...'
});
```

Your module code should handle configuration appropriately, and be resilient towards missing inputs:

```js
function module({url = 'https://...', animate = false}) {
  console.log(url, animate)
}

exports default { init };
```

#### Imports

You must export items which allows the consumer to import __only what is needed__. This helps prepare you for bundling techniques like tree-shaking.

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

exports default { get, isValid };
```

Then consume the API:

```js
// animations.js

import easings from './easings';

function init({element, easing}) {
  if (easings.isValid(easing)) {
    element.animate(easings.get(easing))
  } else {
    element.animate()
  }
}

exports default { init };
```

#### Events for unrelated modules

Use a small Publish Subscribe implementation, like [PubSubJS](https://github.com/mroderick/PubSubJS):

```js
// analytics.js

import PubSub from 'pub-sub';

function beaconToAnalytics(event) {}

function init() {
  PubSub.subscribe('event:navigation', beaconToAnalytics)
}

exports default { init };
```

### DOM binding

When it comes time to attach your [JavaScript module](#module-architecture) to a specific DOM element (or collection of elements), we favour the use of descriptive `data-component` attributes in the markup rather than using specific class names or ids.

We do this:

```html
<nav class="c-popout-nav c-popout-nav--dark" data-component="popout">
  <button class="c-popout-nav__close" data-component="popout-close">Close</button>
  (etc.)
</nav>
```

We don't do this:

```html
<nav class="c-popout-nav c-popout-nav--dark" data-popout>...</nav>

<nav class="js-popout c-popout-nav c-popout-nav--dark">...</nav>

<nav id="popout" class="c-popout-nav c-popout-nav--dark">...</nav>
```

As demonstrated above, we use `data-component` attributes to label any elements that are being bound by the JavaScript.  In instances where other related elements can be inferred without using additional data attributes &mdash; for example a module which is expected to contain just a single input &mdash; then it may be acceptable to use other selectors such as type selectors, however care should be taken.

Initialising a module can then be achieved simply by passing in one of more elements that match these selectors;

```js
const moduleInstances = document.querySelectorAll('[data-component="simple-module"]');
if (moduleInstances.length > 0) {
    mySimpleModule.init(moduleInstances);
}
```

Alternatively for more complex modules that need to be bound to multiple DOM elements, it may make more sense to have the module itself contain a set of default selectors which can then be (optionally) overridden in the init call;

```js
function init(settings) {
    const defaults = {
        wrapper: '[data-component="complex-module"]',
        close: '[data-component="complex-module-close"]'
    };
    const selectors = Object.assign({}, defaults, settings)
}

module.exports = {init};
```
```js
myComplexModule.init({
      wrapper: '[data-component="renamed-complex-module"]',
      close: '[data-component="renamed-complex-module-close"]'
});
```


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

Note that `polyfill.io` adds one additional blocking HTTP request, and if loading asynchronously one must be careful to manage loading order of scripts.  For these reasons it is preferred to bundle polyfills with your main application code, despite the convenience.

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
