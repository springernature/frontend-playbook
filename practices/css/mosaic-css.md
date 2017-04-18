# Mosaic-style CSS

For Nature 'Mosaic' style layouts we write [Object Oriented CSS] with heavy use of 'atomic' utility classes. Object Oriented CSS (OOCSS) is a methodology for writing modularized, scalable, maintainable CSS. The aim with OOCSS is to separate structure from skin and container from content by identifying patterns and creating object classes.

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

We make use of a collection of single purpose styling classes (single responsibility for maximum reuse) that fits well with componentized templates. These classes and their associated styling are immutable, meaning you'd use the same classes across projects. In other words, the aim is to create a common "vocabulary" meant to style documents regardless of context or content.

An example of how to use utility classes would be with font sizes. We could write the following CSS classes that can then be used across any project to set your font-sizes:

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

We create utility classes to handle positioning (default position/float, standardizing margins) and common style elements such as colors, backgrounds and borders, such as in the example below:

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

Common styles and patterns can then be reused across projects, and for Nature content displayed in the mosaic style, our common shared CSS can be found in [shunter-mosaic] (private repo). We can then build on top of this within each project to add styles and patterns that are specific to that project.

### Class Names

Traditionally we have always been told to use semantic class names, that they should reflect the intended structure or meaning of the element it is applied to, as oppose to the presentation. However, this idea has been [debunked as a fallacy], as classes aren’t understood by machines (with microformats being a notable exception). Rather than worrying about creating semantic class names, we should be thinking about creating _sensible_ class names that offer flexibility and reusability. They should give meaning to an element to make it easier to understand and maintain for _developers_. We can do this by naming them based on their function (role) or based on their form (visual).

#### Functional Class Names
Use functional class names when the styling is based on their function or meaning. There is a strong connection between the class name, the styles it applies, and the reason the styles are being applied. Functional class names will always be used to describe OOCSS objects, as these are styles grouped together to carry out a particular function, and also for positioning utility classes. Some examples include:

```css
.pill-button {} /* OOCSS Object */

.tab-group {}  /* OOCSS Object */

.pin-left {} /*  positioning utility class */

.position-absolute {} /*  positioning utility class */
```

#### Presentational Class Names
Presentational class names describe the way an element looks. The name itself is describing the styles that are being applied. These classes are conducive to code reuse as they don't care what they are being used to style. This also comes with the benefit of scaling gracefully. As you're developing new components, you just need to add existing styles to your markup. Soon you will find that creating a new component requires no new CSS to be written, you are just applying existing styles to your HTML. Presentation class names are used for utility styling classes. Some examples include:

```css
.text-blue {}

.text14 {}

.lowercase {}

.background-gray {}

.padding10 {}
```

#### Naming Convention

All class names should be _lowercase-hyphenated_ - all lowercase, words separated by a hyphen. So ```.object-name``` and not ```.objectName``` or ```.ObjectName``` or ```.Object-Name```.

### The Classitis Tradeoff

One of the downsides of this approach is the bloating of the HTML with classes. Separating structure from skin and container from content results in more classes on elements than traditional methods. In the end it comes down to whether you would rather have DRY CSS or DRY HTML, and we came to the conclusion that DRY CSS using the object oriented methodology is preferable due to its maintainability - it may be easier to add/remove classes in your html when updating a component than it is to rewrite your CSS when something changes. On large sites the OOCSS approach produces significantly less CSS making it easier to maintain and adapt to change.

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

[object oriented css]: https://github.com/stubbornella/oocss/wiki/FAQ
[shunter]: https://github.com/nature/shunter
[shunter-mosaic]: https://github.com/springernature/shunter-mosaic 
