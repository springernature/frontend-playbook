# BEM CSS

We use the **Block, Element, Modifier** methodology (commonly referred to as BEM) for CSS class naming. The main aim of the [BEM methodology](http://getbem.com/) is to speed up the development process and ease the teamwork of developers.

It is worth noting that we use a naming scheme based on BEM, but adapted by [Nicolas Gallagher](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/), and detailed in [this post](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) by Harry Roberts.

We namespace our CSS as detailed in our [how we write CSS](how-we-write-css.md) guide. For the purposes of the examples here, we will use the `component` namespace.

BEM naming follows this pattern:
```css
/* Block component */
.c-block {}

/* Element that depends upon the block */
.c-block__element {}

/* Modifier that changes the style of the block */
.c-block--modifier {}
```

## Naming style

All class names should be _lowercase-hyphenated_ - all lowercase, words separated by a hyphen.

We _don't_ do this:
```css
.c-alertBox
.c-AlertBox
.c-Alert-Box
```

We do this:
```css
.c-alert-box
```

## Examples

**Block**: Unique, meaningful names for a logical unit of style. Avoid excessive shorthand.

We _don't_ do this:
```css
.c-feature
.c-content
.c-btn
```

We do this:
```css
.c-alert-box
.c-button
```

**Element**: styles that only apply to children of a block. Elements can also be blocks themselves. Class name is a concatenation of the block name, two underscores and the element name. Examples:
- `.c-alert-box__close`
- `.c-button__icon`

**Modifier**: override or extend the base styles of a block or element with modifier styles. Class name is a concatenation of the block (or element) name, two hyphens and the modifier name. Examples:
- `.c-alert-box--success`
- `.c-button--expanded`

## BEM best practices

Don't `@extend` block modifiers with the block base, always require that the base/unmodified class is present

We _don't_ do this:
```html
<div class="c-my-block--modifier">
```

We do this:
```html
<div class="c-my-block c-my-block--modifier">
```

Don't create elements inside elements. If you find yourself needing this, consider converting your element into a block.

We _don't_ do this:
```css
.c-alert-box__close__button
```

Choose your modifiers wisely. These two rules have very different meaning:
```scss
.c-block--modifier .c-block__element { color: red; }
.c-block__element--modifier { color: red; }
```

## Nesting

If you are using a CSS pre-processor, excessive nesting can be avoided by using smart class naming (with the help of BEM). Avoid nesting selectors more than _3 levels_ deep, and prefer using nesting as a convenience to extend the parent selector over targeting nested elements. For example:

```scss
.c-block {
    padding: 24px;

    &--modifier {
        padding: 12px;
    }

    &__element {
        color: $white;
    }
}
```

Targeting a BEM element/modifier from within a nested block rule (see above) should be done with caution. If your selectors contain a large number of declarations then you should consider moving the element out of the nested rule to make them more readable, and easier to follow. Always adhere to the [KISS](https://en.wikipedia.org/wiki/KISS_principle) principle. You can target a modifier as follows, whilst keeping the element separate for better readability:

```scss
.c-block {
    &--modifier { // compiles to .block--modifier
        text-align: center;
    }
}
.c-block__element {
    color: red;

    &--modifier { // compiles to .block__element--modifier
        color: blue;
    }
}
```
