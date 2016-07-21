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

[complexity]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[eslint]: http://eslint.org/
[jshint]: http://jshint.com/

