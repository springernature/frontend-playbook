# CSS style guide

We namespace our CSS as detailed in our [how we write CSS](how-we-write-css.md) guide. For the purposes of the examples here, we will use the `component` namespace.

- [General Principles](#general-principles)
- [Code Style](#code-style)
  - [Linting](#linting)
- [Preprocessors](#preprocessors)
  - [Nesting](#nesting)

## General principles

We write our CSS using design patterns that aim to maximise maintainability and reuse; See our [house style document](../practices/house-style.md) to understand the rationale behind enforcement of style.

## Code style

Avoid using HTML tags in CSS selectors. And always prefer using a class over HTML tags (with some exceptions)

We _don't_ do this
```scss
div {}
div.c-modal {}
```

We do this:
```scss
.c-modal {}
```

Don't use [ids in selectors](http://csswizardry.com/2011/09/when-using-ids-can-be-a-pain-in-the-class/)

We _don't_ do this:
```scss
#header {}
```

We do this:
```scss
.c-header {}
```

Avoid using `margin-top`. Vertical margins [collapse](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing). Always prefer `padding-top` or `margin-bottom` on preceding elements

We _don't_ do this:
```scss
.c-list__item {
    margin-top: 10px;
}
```

We do this:
```scss
.c-list__item {
    padding-top: 10px;
}

/* or */

.c-list__item {
    margin-bottom: 10px;
}
```

Avoid shorthand properties, if you aren't setting all the values in the property. This applies to all properties with a shorthand: border, margin, padding, font, etc. Use your judgement on this, as there are exceptions.

We _don't_ do this:
```scss
.c-modal {
    // overrides other values encapsulated by the shorthand property.
    // In this case, background-image and its associative properties are set to “none”
    background: $white;
    border: 1px;
}
```

We do this:
```scss
.c-modal {
    background-color: $white;
    border-width: 1px;
}
```

Don't use `!important`. If you must, leave a comment, and prioritise resolving specificity issues before resorting to `!important`.

### Linting

Static analysis tools like linters can flag programming errors, bugs and stylistic errors, making your code more robust, readable and maintainable.

CSS code (not compiled) should be linted with [styleLint](https://github.com/stylelint/stylelint). You can find _an example_ config file in the [config directory](config).

SASS code should be linted with [sass-lint](https://github.com/sasstools/sass-lint) using the [Springer Nature 
`sasslint-config`](https://github.com/springernature/sasslint-config-springernature). This configuration allows us to maintain consistency between different projects.

You can check the [README](https://github.com/springernature/sasslint-config-springernature/blob/master/README.md) for details about installing and configuring the tools.

## Preprocessors

Our preferred CSS preprocessor is [SASS](http://sass-lang.com/) using the [SCSS syntax](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html).

### Nesting

Nesting selectors increases specificity, meaning that overriding any CSS set therein needs to be targeted with an even more specific selector. This quickly becomes a significant maintenance issue, which makes excessive nesting [a bad idea](http://www.sitepoint.com/beware-selector-nesting-sass/). It can easily be avoided by using smart class naming. Avoid nesting selectors more than **3 levels** deep, and prefer using nesting as a convenience to extend the parent selector over targeting nested elements.

If possible, try and avoid using nesting for anything other than:

**Pseudo selectors and state selectors**. We do this:
```scss
a {
    &:hover {
        text-decoration: underline;
    }
    &:focus {
        outline: 1px dashed #000;
    }
}

span {
    &::before {
        content: '\2022';
    }
}
```

**Items that semantically MUST sit within other items**. We do this:
```scss
ul {
    > li {
        display: inline;
    }
}

dl {
    > dt,
    > dd {
        display: inline-block;
    }
}

table {
    > tr {
        > th {
            background: #ccc;
        }
        > td {
            background: #eee;
        }
    }
}
```

**Javascript-only style enhancements**. We do this:
```scss
.c-class {
	display: block;

    .js & {
        display: flex;
    }
}
```
> _Read more about [how to add the `.js` class](../practices/javascript-styling.md)_

**Inline html tags within other elements**. We do this:
```scss
.c-class {
    span {}
    em {}
    small {}
    /* etc */
}
```

**Breakpoints**  
These should be nested within the relevant parent using `@include`.

One exception to these rules is targeting a BEM element from within a nested block rule. See the [BEM documentation](bem-css.md) for more information on BEM and nesting.
