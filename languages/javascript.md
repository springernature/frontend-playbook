JavaScript Style Guide
======================

This document outlines the way we write JavaScript. It's a living styleguide – it will grow as our practices do.

Projects should use both [JSHint] and [ESLint] to enforce these rules. 


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

### KISS

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

[KISS]: https://en.wikipedia.org/wiki/KISS_principle
[complexity]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[eslint]: http://eslint.org/
[jshint]: http://jshint.com/

