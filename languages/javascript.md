JavaScript Style Guide
======================

This document outlines the way we write JavaScript. It's a living styleguide – it will grow as our practices do.

Projects should use both [JSHint] and [ESLint] to enforce these rules. 

- [General Principles](#general-principles)
  - [Write code for humans](#code-for-humans)
  - [Optimise for reading](#optimise-for-reading)
  - [Write modules over monoliths](#modules-over-monoliths)
  - [KISS](#keep-it-simple)
  - [Performant Code](#performant-code)
- [Code Style](#code-style)
  - [Indentation](#indentation)
  - [White Space](#white-space)
  - [Semi-Colons](#semi-colons)
  - [Variables](#variables)
- [Client-Side JavaScript Architecture](#client-side-javascript-architecture)
  - [Directory Structure](#directory-structure)
    - [Components Directory](#components-directory)
    - [Polyfills Directory](#polyfills-directory)
    - [Vendor Directory](#vendor-directory)
    - [Utils Directory](#utils-directory)


General Principles
------------------


### Code For Humans

Your JavaScript should always be optimised for readability first, someone is going to have to maintain your code. Most of the rules in this style guide are here to help enforce this.

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


### Optimise For Reading

Code is written once and read many times, using abbreviations or single-character variables saves time in the short term but there's an overhead every time somebody has to read that code.

Reading code is difficult enough at the best of times. Don't make it harder; it's better to have RSI in your over-worked fingers than for all your colleagues to hate you.


### Modules Over Monoliths

Wherever possible, you should try to think in smaller single-purpose modules and functions. This encourages reuse and helps to [keep complexity down](#complexity).

If code is generic and reusable you should aim to break it into a separate module which can be managed through npm or included in a project's `vendor` directory. We advocate open sourcing of these kinds of modules, and it's a good idea to have open sourcing in mind no matter what you're writing.

Often you'll find that the code you're writing is catered for by a third-party module. Whenever possible, install a dependency rather than reinventing the wheel.

### Keep it simple

We adhere to the [KISS] principle. Unnecessarily complex/obtuse code completely goes against our rule of coding for humans. It's difficult to understand, slows us down, and reduces maintainability. Don't do it.

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
    var mod = number % 2;
    return (mod !== 0);
}
```

```js
// We don't do this
foo ^= bar; bar ^= foo; foo ^= bar;

// We do this
var tempVar = foo;
foo = bar;
bar = tempVar;
```

### Performant Code

We should always try to write fast code, but not if it makes the code difficult to understand. It's inefficient to optimise in favour of performance unless evidence shows that you really _need_ to do that.

If you're writing a small library with a single simple purpose, and you really _really_ need to do it, then it makes sense; in a project with more than one contributor, there's frequently more "cost" than "benefit".

Code Style
---------


### Indentation

We indent our JavaScript using single tabs, not spaces. You can convert characters automatically in most editors, and you're advised to do this.

Follow the [BSD-KNF] indentation style.

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

### White Space

We use white space liberally to help keep code readable. You're encouraged to use newlines to break up long functions into logical chunks.

You should also remove trailing white space from lines of code. Your editor should be able to either remove this or highlight it when present.

### Semi-Colons

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

We define variables with multiple `var` statements and trust our developers to understand [hoisting]. We generally discourage defining variables inside loops or blocks.

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
let foo = 'bar';
const BAR = 'baz';
```

In ES2015 we _don't_ do this:

```js
var foo = 'bar';
var BAR_CONSTANT = 'baz';
```

You can also use destructuring assignment with objects and arrays. These don't have to be multi-line, but there must be spaces after the commas:

```js
let {foo, bar} = getFooAndBar();
let [baz, qux] = getBazAndQux();
```

Client-Side JavaScript Architecture
-----------------------------------


### Directory Structure

Client-Side JavaScript normally lives in `resources/js` in our projects, unless the back-end you're using dictates a different directory.  We should try to stick as closely to this as possible though.

Within this directory, you should always use the following structure. We'll go into more detail as to what these directories are for shortly:

```
<root>
  ├── components
  ├── polyfills
  ├── utils
  └── vendor
```

File names in these directories should be lower-case, with words separated by dashes.

#### Components Directory

The `components` directory is used to house JavaScript that couples to the DOM. There are several conditions that need to be met for a file to live in here:

  - It must bind to the DOM
  - It must add behaviour to and/or manipulates the DOM
  - It must expose itself on the global `SN.Component` object

An example component might be an auto-complete, tab group, or loading spinner.

#### Polyfills Directory

The `polyfills` directory contains JavaScript that polyfills browser behaviour for older clients. JavaScript in this directory must meet these conditions:

  - It must _not_ override native browser functionality
  - It must match native browser functionality exactly (where possible)
  - It can be either third-party, or written in-house

An example polyfill might add `requestAnimationFrame` for any grade-A browsers which don't support it.

#### Vendor Directory

The `vendor` directory is where third-party code lives. It's also where we add code which is written in-house but managed and versioned elsewhere, e.g. as an open source project.

If the code fits the requirements outlined by the `polyfills` directory, it should go there instead of in the `vendor` directory.

JavaScript in this directory must meet these conditions:

  - It must be maintained outside of the project, e.g. as an open-source library
  - It's file name must contain the version of the code
  - It must include a link to the original source code in a comment
  - It must _not_ be modified within the project

An example vendor library might be jQuery, which would live in a file named `jquery-2.1.4.js`.

#### Utils Directory

The `utils` directory is used to house JavaScript written for the project that doesn't fit into the rules for the `components` directory. Utilities still have some conditions of their own:

  - It must _not_ bind to the DOM
  - It must _not_ add behaviour to and/or manipulate the DOM
  - It must _not_ be destructive – arguments passed in cannot be modified
  - It must expose itself on the global `SN.util` object
  - It can expose functions and/or prototypal classes

An example utility might be a function to make a string title-case.


[KISS]: https://en.wikipedia.org/wiki/KISS_principle
[complexity]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[eslint]: http://eslint.org/
[jshint]: http://jshint.com/
[hoisting]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting

