# How we write CSS

Our approach to writing CSS aims to provide a framework for working that allows individual teams the flexibility to make project appropriate decisions within a company wide structure. By following a consistent approach across teams we aim to make it easier to move developers around and allow for the easy evolution of our approach within a large company.

We advocate a componentised approach that is designed for scale, is based on [SASS](http://sass-lang.com/) (using the [SCSS](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html) syntax), follows the [BEM Methodology](bem-css.md), and borrows elements from [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/), Utility Classes, and [ITCSS](http://itcss.io/).

Any CSS that we write should conform to our [house style](house-style.md).

## Architecture

The architecture is split into a series of **levels** with each level representing a folder that contains our SASS split out into different files. Where applicable, content can be organised into sub-folders.

We follow some of the principles of ITCSS - this means that the CSS is organised in specificity order and the SASS files should be included in the order denoted by this structure.

The lower the level number the more generic the styles, the higher the number the more explicit. As the levels increase, so does the specificity. If a level is not needed, it can be excluded. At a product level we may need to add levels into the stack.

### Summary

A summary of the different levels and their purpose:

#### Settings
Contains all **global** SASS variables ([see Sass naming](https://github.com/springernature/frontend-playbook/blob/main/css/how-we-write-css.md#sass-variable-naming)) for your project e.g. colors, fonts, media queries.

#### Functions
Contains all **global** SASS functions e.g. em calculation, unit stripping.

#### Mixins
Contains all **global** SASS mixins, this includes mixin definitions used in the **component** and **utility** levels.

#### Base
A Base rule is applied to an element using an element/type selector, a descendant selector, or a child selector, along with any pseudo-classes. Base styles are related to the basic styles of your product, like typography, reset and global elements like links. Use this level to include any (third-party) resets or normalization css.

#### Components
Components use classes to map to specific UI elements.

They should be **reusable** and independent of context.

They should be **modular**, which means they should have a single focus, and contain everything necessary to display that part of the UI.

They should be **isolated**, meaning they do not directly modify or depend on another component. This is more important than code reuse across components as this _could_ increase dependencies and tight coupling.

#### Utilities
Utilities are high-specificity, very explicit immutable classes that apply a single rule or a single piece of functionality. They are used as overrides, helper classes, and to quickly scaffold up simple page elements.

Utilities can be used by applying the class to an element, or by including the mixin within the other levels. They should be able to apply to any element and not be bound to any particular markup, and also be independent of any cosmetic styling or branding.

### Folder naming

It can be useful to use numbers at the start of your folder names so that the order of levels is preserved in your text editor. This is optional. Use numbers that allow for the easy insertion of new levels if needed e.g.

```
10-settings
20-functions
30-mixins
40-base
50-components
60-utilities
``` 

### Wider architecture

The way that CSS is written, and particularly the use of **levels**, is designed to fit into a wider componentised architecture. We aim to create shared components that can be used across products and across brands. These components can contain one or more of CSS, Javascript, and templates.

We can think of this architecture as comprising of three distinct groups - company, brand, product. **Company** level components are small self-contained snippets that are applicable to _any_ product and can be customisable to work within their context. If we are talking about CSS then an example might be a set of utilities - `float: left` is the same no matter the brand or product. At the **brand** level we have collections of brand specific components - CSS, Javascript and templates. When talking about CSS, this might include a header component that is specific to a particular brand, and applicable to all products within this brand. Components at this level may have dependencies on company level components. At the most specific level we have **products**. These will contain product specific CSS, Javascript and templating, as well as dependencies at the brand and company levels.

Decisions on what components to use should made **at the product level**. An individual product can decide to use certain company wide components, as well as pick and choose from brand level components (or include them all). This is where the levels are important as relates to CSS - we should be able to import from the company and brand groups at each of the levels, and combine the CSS with our own product CSS at each level, while knowing that specificity is controlled.

## Rules

We implement the following rules within each level:

#### 10 Settings
* Contains _only_ variable definitions

#### 20 Functions
* Contains _only_ function definitions

#### 30 Mixins
* Can include _private_ functions and variables (exist at this level)

#### 40 Base
* Should avoid class selectors where possible
* MUST NOT include _private_ functions and variables (exist at _this_ level)
* MUST NOT include _private_ mixins (exist at _this_ level)

#### 50 Components
* Should avoid type selectors where possible
* Can include _private_ functions and variables (exist at this level)
* Can include _private_ mixins (exist at _this_ level), not shared in the `30 Mixins` level
* Can include child elements
* Can include any associated mixins at the `30 Mixins` level

#### 60 Utilities
* MUST NOT include type selectors
* MUST NOT include _private_ functions and variables (exist at _this_ level)
* MUST NOT include _private_ mixins (exist at _this_ level)
* Should consist of a single class
* MUST NOT include child elements, except pseudo-classes
* Where there is more than one rule, an associated mixin should be provided at the `30 Mixins` level
* MUST NOT include any cosmetic styling (color, border, background, etc)

## HTML class naming

We follow these rules when writing class names:

* All classnames are lowercase
* All words are separated by a dash/hyphen
* BEM naming conventions are followed (read more about our [approach to writing BEM](bem-css.md))

## Sass variables

We follow these rules when writing Sass variable names:

* Variables should be prefixed with the component name, omitting the name of the toolkit
* Double hyphen should separate the component name prefix and the variable identifier

Example Sass variables for the component Global Card:
```Sass
// toolkits/global/packages/global-card/scss/10-settings

$card--gutter: 16px;
$card--font-family: inherit;
$card--font-size: 1.4rem;
$card--spacing: $card--gutter / 2;
$card--padding: $card--gutter;
$card--padding-x: 24px 0;
$card--background: transparent;
$card--title-spacing: $card--spacing;
$card--title-font-weight: $context--font-weight-normal;
```

If available use existing context Sass variables instead of hard coded values. For example, in the code above, `$context--font-weight-normal` was taken from the Global/Brand context instead of hard coding the value. It is good to assess what is available in the context before writing the Sass variables for your package.

### Namespaces

Every HTML class should be prefixed with a namespace according to the level to which it belongs:

* `c-` for components e.g. `c-button`
* `u-` for utilities e.g. `u-clearfix`

### Breakpoint Suffixes

HTML classes that have an impact only at specific screen sizes have a @breakpoint-name suffix. For example:

```html
<p class="u-text-center u-text-left@small">Center align until small breakpoint, then align left.</p>
```

## Components vs Utilities

The key differences between components and utilities are that utilities should be purely structural and contain no child elements, whereas components can combine both structural and cosmetic rules, and can make use of child and descendant selectors.

Components can be large or small, and map to particular UI elements. Components will often require a distinct set of markup, and might have associated javascript.

## Classes vs Mixins

By requiring that utilities have both a class and an associated `@mixin`, we are allowing simple UI elmements to be constructed by using a traditional OOCSS approach - by combining component and utility classes on html elements - or by using a more componentised approach that focuses on creating UI components that make extensive use of mixins.

We can think of it like a spectrum with a class based OOCSS/utility approach at one end, and a componentised approach at the other, with all projects sitting somewhere along that spectrum.

## Combining components

As stated before, our components should be **isolated**, meaning they should

> not directly modify or depend on another component. This is more important than code reuse across components as this _could_ increase dependencies and tight coupling.

We would like to avoid a situation where any component _depends_ on another component, but what about situations where components have to combine together. For example, imagine we have two components:

* `.c-header` that gives a header area a background colour, bottom border, and a logo floated left
* `.c-button` a set of 'call to action' button styles

Imagine we want a button component that sits semantically within our header, floated to the right. Because of the modular nature of our components, we should be able to use the component classes on the individual DOM elements without clashes. We can then use utility classes to float the button. Our components stay isolated but work together. If the positioning of the button within the header means that the _cosmetic_ styling of the button needs to change, then we either need to update the button component to cater for this variation, or if it has changed significantly, then this should be built into the header component and the button not used. We need to be in a position where updating the button component does not break the header component.

## Further reading

* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Managing CSS Projects with ITCSS](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)
* [The Role of Utility Classes in Scalable CSS](http://davidtheclark.com/on-utility-classes/)
* [Immutable CSS](https://csswizardry.com/2015/03/immutable-css/)
* [More Transparent UI Code with Namespaces](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
