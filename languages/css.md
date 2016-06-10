
# CSS Style Guide -- WIP


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

## General Principles

We currently write our CSS using two (unfortunately conflicting) design patterns; [BEM] for some teams, and [a hybrid of OOCSS and Atomic CSS] for others.

## The Rules

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
[bem]: https://github.com/springernature/frontend/languages/bem-css.md
[a hybrid of OOCSS and Atomic CSS]: https://github.com/springernature/frontend/languages/mosaic-css.md
[stylelint]: https://github.com/stylelint/stylelint
[debunked as a fallacy]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
[rems bug in chrome]: http://stackoverflow.com/questions/20099844/chrome-not-respecting-rem-font-size-on-body-tag
