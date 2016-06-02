
CSS Style Guide -- WIP
===============

This document aspires to outline the way we write CSS/SASS, and is based at the moment on the existing [Nature runbook]. This is just a first pass, and is likely to be incomplete (and wrong) in places.  It's a living styleguide – it will grow and adapt as our practices do.

Projects should use [StyleLint] to enforce these rules. You can find the config file in the [config directory](config).

- [General Principles](#general-principles)
  - [Class Names](#class-names)
  - [The Classitis Tradeoff](#the-classitis-tradeoff)
  - [Font Sizing](#font-sizing)
  - [Javascript Hooks](#javascript-hooks)
- [The Rules](#the-rules)
  - [Indentation](#indentation)
  - [At Rules](#at-rules)
  - [Blocks](#blocks)
  - [Colors](#colors)
  - [Comments](#comments)
  - [Declarations](#declarations)
  - [Functions](#functions)
  - [Media Features](#media-features)
  - [Numbers](#numbers)
  - [Rules](#rules)
  - [Selectors](#selectors)
  - [Value Lists](#value-lists)
  - [General](#general)
  - [Single Line CSS](#single-line-css)

General Principles
------------------

We write our CSS using a hybrid of [Object Oriented CSS] and [Atomic CSS].

Atomic CSS is a collection of single purpose styling classes (single responsibility for maximum reuse) that fits well with componentized templates. Atomic classes and their associated styling are immutable, meaning you'd use the same classes whatever the project you're working on or the team you're working with. In other words, Atomic CSS is a common "vocabulary" meant to style documents regardless of context or content.

An example of how to use atomic classes would be with font sizes. We could write the following CSS classes that can then be used across any project to set your font-sizes:

```css
.text11 {
    font-size: 1.1rem;
}

.text13 {
    font-size: 1.3rem;
}

.text14 {
    font-size: 1.4rem;
}
```

Object Oriented CSS (OOCSS) is another methodology for writing modularized, scalable, maintainable CSS. the aim with OOCSS is to separate structure from skin and container from content by identifying patterns and creating object classes.

By separating structure from skin we mean positioning (position, float, margin, etc.) from styling (background, color, border, etc.). In practice, this means to not mix structure/positioning properties with skin/styling properties on the same class. This way our “skinning” properties can be reused on a variety of elements, preventing property duplication in our CSS.

By separating container from content we allow the re-use of elements and classes no matter where you are in the DOM. A styled element should never be dependent on where it’s at in a page. In the following example the style of a heading element is bound to either the sidebar or header DOM element:

```css
#sidebar h3 {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 10px;
    color: #777;
}

#header h3 {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 10px;
    color: #069;
}
```

You can see that we repeat the font-family and the font-size. If we remove the bindings and abstract the common styles into reusable object classes, we can use these two heading styles anywhere in our code:

```css
h3 {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 10px;
}

.color-gray {
    color: #777;
}

.color-blue {
    color: #069;
}
```

There is a lot of crossover between OOCSS and Atomic CSS. We create atomic classes to handle positioning (default position/float, standardizing margins) and common style elements such as colors, backgrounds and borders, such as in the example below:

```css
.position-absolute {
    position: absolute;
}

.pin-left {
    float: left;
}

.ma0 {
    margin: 0;
}

.ma10 {
    margin: 10px;
}

.ma20 {
    margin: 20px;
}

.text-orange {
    color: #cc4b14;
}

.border-gray {
    border-style: solid;
    border-width: 0;
    border-color: #999;
}

.border-all-1 {
    border-width: 1px;
}

.background-gray {
    background-color: #999;
}
```

Once we have our base classes we can start to look for patterns in the design and create reusable object modules. These are classes that can be used to style a particular object that is used across a site such as a button. A real world example from a Shunter project would be what we call a pill button. It has the following styles:

```css
.pill-button {
    padding: 6px 20px;
    background-color: #fff;
    border: 4px solid #bcd2dc;
    border-radius: 20px;
    font-size: 1.4rem;
    line-height: 1.4;
    font-weight: bold;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```

Notice that following the rules of separating structure and skin, we are only including the style attributes, this means that this pattern can be reused across the site and positioned in different ways. For example we could have one instance where this button is floated left and one where it is floated right, as in the example below:

```html
<a href="/" class="pill-button pin-left">left aligned button</a>
<a href="/" class="pill-button pin-right">right aligned button</a>
```

Common styles and patterns can then be reused across projects, and for Nature content displayed in the mosaic style, our common shared CSS can be found in [shunter-mosaic]. We can then build on top of this within each project to add styles and patterns that are specific to that project.

### Class Names

Traditionally we have always been told to use semantic class names, that they should reflect the intended structure or meaning of the element it is applied to, as oppose to the presentation. However, this idea has been [debunked as a fallacy], as classes aren’t understood by machines (with microformats beign a notable exception). Rather than worrying about creating semantic class names, we should be thinking about creating _sensible_ class names that offer flexibility and reusability. They should give meaning to an element to make it easier to understand and maintain for _developers_. We can do this by naming them based on their function (role) or based on their form (visual).

#### Functional Class Names
Use functional class names when the styling is based on their function or meaning. There is a strong connection between the class name, the styles it applies, and the reason the styles are being applied. Functional class names will always be used to describe OOCSS objects, as these are styles grouped together to carry out a particular function, and also for atomic positioning classes. Some examples include:

```css
.pill-button {} /* OOCSS Object */

.tab-group {}  /* OOCSS Object */

.pin-left {} /* Atomic positioning class */

.position-absolute {} /* Atomic positioning class */
```

#### Presentational Class Names
Presentational class names describe the way an element looks. The name itself is describing the styles that are being applied. These classes are conducive to code reuse as they don't care what they are being used to style. This also comes with the benefit of scaling gracefully. As you're developing new components, you just need to add existing styles to your markup. Soon you will find that creating a new component requires no new css to be written, you are just applying existing styles to your HTML. Presentation class names are used for atomic styling classes. Some examples include:

```css
.text-blue {}

.text14 {}

.lowercase {}

.background-gray {}

.padding10 {}
```

#### Naming Convention

All class names should be train-case - all lowercase, words separated by a hyphen. So ```.object-name``` and not ```.objectName``` or ```.ObjectName``` or ```.Object-Name```.

### The Classitis Tradeoff

One of the downsides of this approach is the bloating of the HTML with classes. Separating structure from skin and container from content results in more classes on elements than traditional methods. In the end it comes down to whether you would rather have DRY CSS or DRY HTML, and we came to the conclusion that DRY CSS using the object oriented methodology is preferable due to its maintainability - it is much easier to add/remove classes in your html when updating a component than it is to rewrite your CSS when something changes. On large sites the OOCSS approach produces significantly less CSS making it easier to maintain and adapt to change.

### Font Sizing

All font sizes MUST be specified using rems only with a pixel fall back. Do not use percentages, ems or pixels alone. When using Shunter the px fallback is added automatically. In order for rems to be easily calculated you should have the following in your css:

```css
html {
    font-size: 62.5%;
}

body {
    font-size: 1.7em;
}
```

The font size on the html element resets the base font size to ```10px```, allowing the rem value to be the pixel value divided by 10 - so ```11px``` would be ```1.1rem```. The use of ```font-size: 1.7em``` on the body fixes a [rems bug in chrome].

### Javascript Hooks

Using some form of JavaScript-specific classes can help to reduce the risk that changes to components will break any JavaScript that is also applied. We used to take the approach of using certain classes only for JavaScript hooks – ```js-*``` – and not to hang any presentation off them. This has been dropped in favour of using Data Attributes.

Use ```data-component="name-of-component"``` as the javascript hook, as it will match up with code in the ```js/components``` folders. For sub-elements then use ```data-role="name-of-role"```, so you end up with component elements and roles within that component.

The Rules
---------

### Indentation

We indent our css using single tabs, not spaces. You can convert characters automatically in most editors, and you're advised to do this.

### At Rules

Always require an empty line before @rules except within a blockless group.

We _don't_ do this:

```css
a {} @media {}

a {}
@media {}
```

```css
@import url(x.css);

@import url(y.css);

@media print {}
```

We do this:

```css
a {}

@media {}
```

```css
@import url(x.css);
@import url(y.css);

@media print {}
```

### Blocks

There MUST be a newline after the closing brace.  
There MUST be a newline before the closing brace in multi-line blocks.  
There MUST be a single space before the closing brace in single-line blocks.  
There MUST be a newline after the opening brace in multi-line blocks.  
There MUST be a single space after the opening brace in single-line blocks.  
There MUST be a single space before the opening brace.  
Blocks MUST NOT be empty.

We _don't_ do this:

```css
a { color: pink; }b { color: red; }

a {
color: pink;}

a { color: pink;}

a{color: pink;
}

a {color: pink; }

a{ color: pink; }

a { }
```

We do this:

```css
a { color: pink; }

b {
    color: red;
    top: 0;
}
```

### Colors

Hex colors should be lowercase.  
We should use short notation for hex colors.  
Disallow invalid hex colors.

We _don't_ do this:

```css
a { color: #FFF; }

a { color: #ffffff; }

a { color: #00; }
```

We do this:

```css
a { color: #000; }

a { color: #fff; }

a { color: #a4a4a4; }
```

### Comments

There MUST be an empty line before comments _except_ for comments that are nested and the first child of their parent node.

We _don't_ do this:

```css
a {}
/* comment */

a {

  /* comment */
  color: pink;
}
```

We do this:

```css
a {}

/* comment */

b {}

a {
    /* comment */
    color: pink;
}
```

### Declarations

There MUST NOT be whitespace after the bang.  
There MUST be a single space before the bang.  
There MUST be a newline after the semicolon in multi-line rules.  
There MUST be a single space after the semicolon in single-line declaration blocks.  
There MUST NOT be whitespace before the semicolons.  
Limit the number of declarations within a single line declaration block to 1.  
There MUST be a newline after the colon if the declaration's value is multi-line.  
There MUST be a single space after the colon if the declaration's value is single-line.  
There MUST NOT be whitespace before the colon.

We _don't_ do this:

```css
a { color: pink ! important; }

a {
    color: pink; top: 0;
}

a { color: pink ; }

a { color:pink; }

a { color: pink; top: 0; }

a { color : pink }

a {
    box-shadow: 0 0 0 1px #5b9dd9,
        0 0 2px 1px rgba(30, 140, 190, 0.8);
}
```

We do this:

```css
a { color: pink !important; }

a { color: pink; }

a {
    color: pink;
    top: 0;
}

a {
    box-shadow:
        0 0 0 1px #5b9dd9,
        0 0 2px 1px rgba(30, 140, 190, 0.8);
}
```

### Functions

Disallow an unspaced operator within calc functions.  
There MUST be a newline after the commas in multi-line functions.  
There MUST be a single space after the commas in single-line functions.  
There MUST NOT be whitespace before the commas.  
There MUST be a newline inside the parentheses of multi-line functions.  
There MUST NOT be a whitespace inside the parentheses of single-line functions.  
There MUST be whitespace after the function.

We _don't_ do this:

```css
a { top: calc(1px+2px); }

a { top: calc(1px+ 2px); }

a { transform: translate(1,1) }

a { transform: translate(1 ,1) }

a { transform: translate(1
  ,1) }

a { transform: translate( 1, 1 ) }

a { transform: translate(1, 1 ) }

a { transform: translate(1, 1)scale(3); }
```

We do this:

```css
a { top: calc(1px + 2px); }

a { top: calc(calc(1em * 2) / 3); }

a { transform: translate(1, 1) }

a {
  transform: translate(1,
    1)
}

a { transform: translate(1, 1) scale(3); }

a {
  transform:
    translate(1, 1)
    scale(3);
}
```

### Media Features

There MUST be a single space after the colon.  
There MUST NOT be whitespace before the colon.  
There MUST be a single space after the range operator.  
There MUST be a single space before the range operator.  
There MUST be a newline after the commas in multi-line media query lists.  
There MUST be a single space after the commas in single-line media query lists.  
There MUST NOT be whitepace before the commas.  
There MUST NOT be whitespace on the inside the parentheses.

We _don't_ do this:

```css
@media (max-width:600px) {}

@media (max-width :600px) {}

@media (max-width : 600px) {}

@media (max-width>=600px) {}

@media (max-width >=600px) {}

@media (max-width>= 600px) {}

@media screen and (color),projection and (color) {}

@media screen and (color) ,projection and (color) {}

@media screen and (color)
, projection and (color) {}

@media ( max-width: 300px ) {}
```

We do this:

```css
@media (max-width: 600px) {}

@media (max-width >= 600px) {}

@media screen and (color), projection and (color) {}
```

### Numbers

There MUST be a leading zero.  
Disallow trailing zeros within numbers.  
Disallow units for zero lengths.

We _don't_ do this:

```css
a { line-height: .5; }

a { transform: translate(2px, .4px); }

a { top: 1.0px }

a { top: 1.01000px }

a { top: 0px }

a { top: 0.000em }
```

We do this:

```css
a { line-height: 0.5; }

a { transform: translate(2px, 0.4px); }

a { top: 1px }

a { top: 1.01px }

a { top: 0 } /* no unit */

a { transition-delay: 0s; } /* dimension */

a { top: 2in; }

a { top: 1.001vh }
```

### Rules

Disallow shorthand properties that override related longhand properties.  
There MUST be an empty line before multi-line rules.  
There MUST be a trailing semicolon.

We _don't_ do this:

```css
a {
    padding-left: 10px;
    padding: 20px;
}

a {
    transition-property: opacity;
    transition: opacity 1s linear;
}

a {
    border-top-width: 1px;
    top: 0;
    bottom: 3px;
    border: 2px solid blue;
}

a { color: pink; }
b { color: pink; }

a { color: pink }
```

We do this:

```css
a {
    padding: 10px;
    padding-left: 20px;
}

a { transition-property: opacity; }

a { transition: opacity 1s linear; }

a {
    transition-property: opacity;
    -webkit-transition: opacity 1s linear;
}

a { color: pink; }

b { color: pink; }

a { color: pink; }
```

### Selectors

There MUST be a single space after the combinators.  
There MUST be a single space before the combinators.  
There MUST be a newline after the commas.  
There MUST NOT be whitespace before the commas.

We _don't_ do this:

```css
a +b { color: pink; }

a+ b { color: pink; }

a>b { color: pink; }

a, b { color: pink; }

a ,b { color: pink; }

a
, b { color: pink; }

a
,
b { color: pink; }
```

We do this:

```css
a + b { color: pink; }

a,
b { color: pink; }
```

### Value Lists

There MUST be a newline after the commas in multi-line value lists.  
There MUST be a single space after the commas in single-line value lists.  
There MUST NOT be whitespace before the commas.

We _don't_ do this:

```css
a { background-size: 0
    , 0; }

a { background-size: 0,0; }

a { background-size: 0 ,0; }

a { background-size: 0 ,
      0; }
```

We do this:

```css
a { background-size: 0, 0; }

a { background-size: 0,
      0; }
```

### General

Limit the number of adjacent empty lines to 1.  
Disallow end-of-line whitespace.  
Strings MUST be wrapped with single quotes.  
Disallow missing end-of-file newlines in non-empty files.

We _don't_ do this:

```css
a { color: pink; }


b { color: pink; }

a { color: pink; }·

a { color: pink; }····

a { content: "x"; }

a[id="foo"] { color: pink; }
```

We do this:

```css
a { color: pink; }

b { color: pink; }

a { content: 'x'; }

a[id='foo'] { color: pink; }

a { color: pink; }
\n
/** ↑
 * This newline */
```

### Single Line CSS

A quick note on single line CSS. We allow single line CSS when there is only one declaration, but we shouldn't always use it. We only ever use single line CSS when there are groups of multiple CSS classes with one declaration, for example spacing, to aid legibility. In this case we also do not require a space between classes. So we would use it in the following example:

```css
.ma0 { margin: 0; }
.ma1 { margin: 1px; }
.ma2 { margin: 2px; }
.ma4 { margin: 4px; }
.ma6 { margin: 6px; }
.ma10 { margin: 10px; }
.ma15 { margin: 15px; }
.ma20 { margin: 20px; }
.ma30 { margin: 30px; }
.ma40 { margin: 40px; }
.ma50 { margin: 50px; }
.ma70 { margin: 70px; }
```

But in the following example we would not use it:

```css
.nowrap {
    white-space: nowrap;
}

.prewrap {
    word-wrap: break-word;
    white-space: pre-wrap;
}

.overflow-ellipsis {
    text-overflow: ellipsis;
}
```

[Nature runbook]: https://github.com/nature/playbook
[shunter]: https://github.com/nature/shunter
[shunter-mosaic]: https://github.com/nature/shunter-mosaic
[object oriented css]: https://github.com/stubbornella/oocss/wiki/FAQ
[atomic css]: http://acss.io/frequently-asked-questions.html#what-is-atomic-css-
[stylelint]: https://github.com/stylelint/stylelint
[debunked as a fallacy]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
[rems bug in chrome]: http://stackoverflow.com/questions/20099844/chrome-not-respecting-rem-font-size-on-body-tag
