# Graded Browser Support

## Our criteria for browser support

We follow the guidelines for graded browser support outlined by Nate Koechley at Yahoo:
[Yahoo Grade Browser Support guide](https://github.com/yui/yui3/wiki/Graded-Browser-Support)

| Tables        | Grade-A support | Grade-C support  |
| ------------- |:---------------:| ----------------:|
| Chrome        | latest stable   |                  |
| Edge          | latest stable   |                  |
| Firefox       | latest stable   |               <2 |
| IE            | 9, 10, 11       |               <9 |
| Opera         | latest stable   |              <10 |
| Safari        | latest stable, latest stable -1   |  <4.1 (desktop) |
| Webkit        | Android 4.&#8224; |  <3           |

## How we implement graded browser support

Our primary approach to graded browser support is the "cutting the mustard" progressive enhancement technique, based upon the principles developed by the BBC: [Cutting the Mustard](http://responsivenews.co.uk/post/18948466399/cutting-the-mustard).  However, user agent sniffing is still applied on some legacy projects.

We load a basic stylesheet to all users. This contains only [normalisation](https://necolas.github.io/normalize.css/) and a few small enhancements to the user-agent stylesheet.
To load the full experience only in modern browsers we implement logic in the media attribute of the `<link>` element that identifies the main stylesheet, loading the stylesheet only in browsers that recognise the properties of that media query.
This technique is documented here: [Cutting the Mustard with Media queries](https://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/).

We use the following link attribute to conditionally load our enhanced css:

```html
<link href="style.css" rel="stylesheet" media="only screen and (min-resolution: 0.1dpcm), only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0)">
```

We couple the loading of JavaScript to the loading of the enhanced css.
If the browser loads the CSS within the media query, then load the JavaScript.

To do this, we set a style in the enhanced css that won't affect the visual representation of the site, and then use JavaScript to check whether it has been applied.
If it has been applied, we know that the enhanced css has loaded and we can then load the JavaScript.

```css
body {
    clear: both;
}
```

```javascript
if (window.getComputedStyle && window.getComputedStyle(document.body).getPropertyValue('clear') === 'both') {
    // bootstrap the javascript application
}
```
