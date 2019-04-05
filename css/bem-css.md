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

**Element**: styles that only apply to children of a block. Class name is a concatenation of the block name, two underscores and the element name. Examples:
- `.c-alert-box__close`
- `.c-button__icon`

**Modifier**: override or extend the base styles of a block or element with modifier styles. Class name is a concatenation of the block (or element) name, two hyphens and the modifier name. Examples:
- `.c-alert-box--success`
- `.c-button--expanded`

## BEM best practices

Don’t extend the block element with a modifier, without the unmodified block element also being present.

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
```css
.c-block--modifier .c-block__element { color: red; }
.c-block__element--modifier { color: red; }
```

Don't nest class names when using a preprocessor. Here are a few reasons why:

1. It prevents from being able to find the class names easily
2. It hinders developers understanding the context that they are working on
3. When reviewing a pull request, it requires extra effort to see the actual
   selector and to do a proper review

We _do_ this:

```css
.c-block { padding: 24px; }

.c-block--modifier { padding: 12px; }

.c-block__element { color: white; }

.c-block__element--modifier { color: black }
```

We _don't_ do this:

```css
.c-block {
    padding: 24px;

    &--modifier {
        padding: 12px;
    }

    &__element {
        color: white;

        &--modifier {
            color: black;
        }
    }
}
```
