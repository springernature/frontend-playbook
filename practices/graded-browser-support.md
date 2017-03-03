# Graded Browser Support

* [Our criteria for browser support](#our-criteria-for-browser-support)
* [How we implement graded browser support](#how-we-implement-graded-browser-support)


## Our criteria for browser support

We follow the guidelines for graded browser support outlined by Nate Koechley at Yahoo:
[Yahoo Grade Browser Support guide](https://github.com/yui/yui3/wiki/Graded-Browser-Support)

| Tables        | Grade-A support                 | Grade-C support |
| ------------- |:-------------------------------:| ---------------:|
| Chrome        | latest stable                   |                 |
| Edge          | latest stable                   |                 |
| Firefox       | latest stable                   |              <2 |
| IE            | 11                              |             <11 |
| Opera         | latest stable                   |             <10 |
| Safari        | latest stable, latest stable -1 |  <4.1 (desktop) |
| Webkit        | Android 4.&#8224;               |              <3 |

## How we implement graded browser support

Our primary approach to graded browser support is the "cutting the mustard" progressive enhancement technique, based upon the principles developed by the BBC: [Cutting the Mustard](http://responsivenews.co.uk/post/18948466399/cutting-the-mustard).  However, user agent sniffing is still applied on some legacy projects.

We load a basic stylesheet to all users. This contains only [normalisation](https://necolas.github.io/normalize.css/) and a few small enhancements to the user-agent stylesheet.
To load the full experience only in modern browsers we implement logic in the media attribute of the `<link>` element that identifies the main stylesheet, loading the stylesheet only in browsers that recognise the properties of that media query.
This technique is documented here: [Cutting the Mustard with Media queries](https://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/).

The media queries we use are based upon [CSS Only Mustard Cut](https://github.com/Fall-Back/CSS-Mustard-Cut), with a preference towards combining them into one rather than separating them out into multiple `<link>` elements.  Note that you **cannot** add line breaks to the media query if they are combined.

Note that while our graded browser support table specifies Internet Explorer 10 and below as grade-c, until an updated media query is found this approach renders IE10 as grade-a.

```html
<link rel="stylesheet" href="your-css.css" media="only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0), (-ms-high-contrast: none), only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)">
```

We couple the loading of JavaScript to the loading of the enhanced CSS.
If the browser loads the CSS within the media query, then load the JavaScript.

In order to check this, we use [window.matchMedia](https://developer.mozilla.org/en/docs/Web/API/Window/matchMedia).

```javascript
(function() {
    var linkEl = document.querySelector('link');
    if (window.matchMedia && window.matchMedia(linkEl.media)) {
        var script = document.createElement('script');
        script.src = 'your-script.js';
        script.async = true;
        document.body.appendChild(script);
    }
})();
```

The javascript code outlined above will fail in Internet Explorer if there is more than one link element. You can get around this by targeting the specific link element using a class or ID.
