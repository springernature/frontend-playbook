# How we write CSS

Our approach to writing CSS aims to provide a framework for working that allows individual teams the flexibility to make project appropriate decisions within a company wide structure. By following a consistent approach across teams we aim to make it easier to move developers around and allow for the easy evolution of our approach within a large company.

We advocate a componentised approach that is designed for scale, is based on [SASS](http://sass-lang.com/) (using the [SCSS](http://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html) syntax), follows the [BEM Methodology](https://github.com/springernature/frontend-playbook/blob/master/practices/css/bem-css.md), and borrows elements from [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/), Utility Classes, and [ITCSS](http://itcss.io/).

Any CSS that we write should conform to our [house style](house-style.md).

## Architecture

The architecture is split into a series of **levels** with each level representing a folder that contains our SASS split out into different files. Where applicable content can be organised into sub folders.

We follow some of the principles of ITCSS - this means that the CSS is organised in specificity order and the SASS files should be included in the order denoted by this structure.

The lower the level number the more generic the styles, the higher the number the more explicit. As the levels increase, so does the specificity. If a level is not needed, it can be excluded. At a project level we may need to add levels into the stack.

### Summary

#### Settings
Contains all **global** SASS variables for your project e.g. colors, fonts, media queries.

#### Functions
Contains all **global** SASS functions e.g. em calculation, unit stripping.

#### Mixins
Contains all **global** SASS mixins, this includes mixin definitions used in the **pattern** and **utility** levels.

#### Base
A Base rule is applied to an element using an element/type selector, a descendant selector, or a child selector, along with any pseudo-classes. Base styles are related to the basic styles of your product, like typography, reset and global elements like links. Use this level to include any (third-party) resets or normalization css.

examples:
```scss
blockquote {}

a {
	&:hover {}
}

ul {
	> li {}
}
```

#### Components
Components use classes to map to specific UI elements. They should exist as stand-alone UI components and **never** depend on other components.

#### Patterns
Patterns use classes to apply a reusable design pattern. This level should include any pattern that does not bind itself to a particular UI element. Styles written here can include both structural and cosmetic rules, and apply branding.

#### Utilities
Utilities are high-specificity, very explicit classes that apply a single rule or a single piece of functionality. They are used as overrides, helper classes, and to quickly build up simple page elements.

Utilities can be used by applying the class to an element, or by including the mixin within the other levels. They should be able to apply to any element and not be bound to any particular markup, and also be independent of any cosmetic styling or branding.

### Folder naming

It can be useful to use numbers at the start of your folder names so that the order of levels is preserved in your text editor. This is optional. Use numbers that allow for the easy insertion of new levels if needed e.g.

```
10-settings
20-functions
30-mixins
40-base
50-components
60-patterns
70-utilities
```

### Wider architecture

The way that CSS is written, and particularly the use of **levels**, is designed to fit into a wider componentised architecture plan. We aim to create shared components that can be used across products and across brands. These components can contain one or more of CSS, Javascript, and templates.

We can think of this architecture as comprising of three distinct groups - company, brand, product. **Company** level components are small self-contained snippets that are applicable to _any_ product and can be customisable to work within their context. If we are talking about CSS then an example might be a set of utilities - `float: left` is the same no matter the brand or product. At the **brand** level we have collections of brand specific components - CSS, Javascript and templates. When talking about CSS, this might include a header component that is specific to a particular brand, and applicable to all products within this brand. Components at this level may have dependencies on company level components. At the most specific level we have **products**. These will contain product specific CSS, Javascript and templating, as well as dependencies at the brand and company levels.

Decisions on what components to use should made **at the product level**. An individual product can decide to use certain company wide components, as well as pick and choose from brand level components (or include them all). This is where the levels are important as relates to CSS - we should be able to import from the company and brand groups at each of the levels, and combine the CSS with our own product CSS at each level, while knowing that specificity is controlled.

## Rules

We implement the following rules to define the content at each level:

#### 10 Settings
* Contains _only_ variable definitions

#### 20 Functions
* Contains _only_ function definitions

#### 30 Mixins
* Can include _private_ functions and variables

#### 40 Base
* Should avoid type selectors where possible 
* MUST NOT include _private_ functions and variables (exist at _this_ level)
* MUST NOT include _private_ mixins (exist at _this_ level)

#### 50 Components
* Should avoid type selectors where possible
* Can include _private_ functions and variables
* Can include _private_ mixins (exist at _this_ level), not shared in the `30 Mixins` level
* Can use global mixins

#### 60 Patterns
* Should avoid type selectors where possible
* MUST NOT include _private_ functions and variables (exist at _this_ level)
* MUST NOT include _private_ mixins (exist at _this_ level)
* Where there is more than one rule, an associated `@mixin` should be provided at the `30 Mixins` level
* Can use global mixins
* Can include child elements

#### 70 Utilities
* MUST NOT include type selectors
* MUST NOT include _private_ functions and variables (exist at _this_ level)
* MUST NOT include _private_ mixins (exist at _this_ level)
* Should consist of a single class
* MUST NOT include child elements, except pseudo-classes
* Where there is more than one rule, an associated `@mixin` should be provided at the `30 Mixins` level
* MUST NOT use global mixins (other than it's own)
* MUST NOT include any cosmetic styling (color, border, background, etc)

## HTML class naming

We follow the following rules when writing class names:

* All classnames are lowercase
* All words are separated by a dash/hyphen
* BEM naming conventions are followed

You can read more about our [approach to writing BEM](bem-css.md).

### Namespaces

Every HTML class should be prefixed with a namespace according to the level to which it belongs:

* `c-` for components e.g. `c-button`
* `p-` for patterns e.g. `p-external-link`
* `u-` for utilities e.g. `u-clearfix`

### Breakpoint Suffixes

HTML classes that have an impact only at specific screen sizes have a @breakpoint-name suffix. For example:

```html
<p class="u-text-center u-text-left@small">Center align until small breakpoint, then align left.</p>
```

## Patterns vs Utilties vs Components

The key difference between patterns and utilties are that utilites should be purely structural and contain no child elements, whereas patterns can combine both structural and cosmetic rules, and can make use of child and descendent selectors.

The difference between patterns and components is that components are often larger and can map to particular UI elements. Components will often require a distinct set of markup, and might have associated javascript.

## A range of approaches

Hopefully the methodology we have described allows for a range of approaches within our defined framework. By requiring that both utilities and patterns **all** have both a class and an associated `@mixin`, we are allowing elmements to be constructed by using a traditional OOCSS approach - by breaking stuff down into smaller shared design patterns, then using them by building up classes on html elements, or by using a more componentised approach that focuses more on creating UI components that make extensive use of mixins to build themselves within the SASS.

It is perfectly possible that some projects will make heavy use of the pattern layer combined with utility classes whilst being light on components, where as some projects don't have so many reuseable design patterns and instead make extensive use of mixins and the components layer.

We can think of it like a spectrum with a class based OOCSS/utility approach at one end, and a componentised approach at the other, with all projects sitting somewhere along that spectrum.

## Combining components

We have already discussed how our components should be stand-alone and have no knowledge of their container, but what about situtions where a component has to change characteristics based on it's location within another component? For example, imagine we have two components:

* `.c-navigation` that styles a list of links inline with bullet points to represent page navigation
* `.c-header` that gives a header area a background colour, bottom border, and a logo floated left

In some instances we have pages where this is all that exists in the header (e.g. error pages), and we have some instances where we use the navigation styles outside of the header. But we also have pages where the navigation element exists inside the header floated to the right.

We know that components should have no knowledge of their container so we would **not** create a modifier class within the navigation component, but we can create a child element within our header component like this:

```scss
.c-header {
  .c-header__navigation {
    float: right;
  }
}
```

Now all we need to do is add the `c-navigation c-header__navigation` classes to the navigation element, keeping both components de-coupled. In this instance we can also achieve the same outcome by using utility classes, for example we could add `c-navigation u-pin-right` to the navigation element. In this instance this would be the simpler approach, but consider an example where there is not a single rule - maybe we want different behaviour at different media queries, and it becomes cleaner to use the first approach.

## Further reading

* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Managing CSS Projects with ITCSS](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)
* [The Role of Utility Classes in Scalable CSS](http://davidtheclark.com/on-utility-classes/)
* [Immutable CSS](https://csswizardry.com/2015/03/immutable-css/)
* [More Transparent UI Code with Namespaces](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
